=================
Flasher son STM32
=================

:date: 2016-02-06 11:30
:tags: stm32
:category: tuto
:slug: stm32_flashing
:authors: JackDesBwa
:summary: Méthodes de flashage d’un STM32

Contexte
========

Nous en parlions entre nous depuis longtemps et voilà : nous avons dégagé du
temps pour commencer un vrai projet à base de STM32 (une famille de
microcontrôleurs). Puisque nous n’y connaissons pour le moment pas grand-chose,
il va falloir découvrir.

Voici donc quelques trouvailles sur une première étape primordiale : être
capables d’envoyer notre code dans le puceron. Notez que ces propos sont le
résultat d’expérimentations, et qu’ils pourraient donc être erronés ou
incomplets.

Il arrivera dans l’article que certaines commandes soient détaillées. Si le
niveau de détail n’est pas adapté à votre lecture, sachez que ces précisions ne
sont pas nécessaires pour comprendre comment flasher le STM32.

Code de test
============

Nous commencerons par un code au demeurant inutile, mais fort simple, qui ne
requiert pas d’accès spécifique au microcontrôleur. Après tout, nous cherchons
seulement à flasher un code, pas à utiliser les possibilités du morceau de
silicium.

Programme de test
-----------------

Tout d’abord, il est important de le dire : n’utilisez pas ce genre de code !

Cet exemple est outrageusement minimaliste et comporte une partie
particulièrement affreuse. Il a pour seul intérêt d’illustrer le propos de cet
article tout en étant exécutable sur une cible STM32 à condition de
s’accommoder des atrocités réalisées ici. Je passerai sous silence la
sorcellerie utilisée afin que vous ne soyez pas tenté d’imiter la formule
douteuse, qui d’ailleurs vous reviendrait en pleine figure dès que vous
essaieriez de réaliser quoi que ce soit de sérieux. Vraiment, n’utilisez pas
cette horreur en dehors de cet article.

Appelons ce fichier `useless.cpp`

::

	float measures[200];

	int main() {
		float y = 0.0f;

		for (float & m : measures) {
			y = 200 + (y - 200) * 0.951229424501f;
			m = y;
		}

		while (true);
	}

	/* Very ugly part */
	#define VECTOR __attribute__((section(".vector_table")))
	unsigned int vector_table_sp VECTOR = 0x20000400;
	int (*vectors_table_entry)() VECTOR = main;

Nous déclarons d’abord un tableau `measures` résidant en RAM qui récupèrera les
résultats de nos calculs. Dans la pile, nous utiliserons une variable `y`
initialisée à 0 qui servira d’accumulateur pour le calcul à suivre.

La ligne `for` qui suit est une syntaxe c++11 qui permet de parcourir chacun des
éléments du tableau dans une boucle. La variable `m` sera alors une référence
vers l’élément du tableau courant (pratique, non ?). Ainsi nous calculons
d’abord une formule spécifique sur laquelle nous reviendrons en fin d’article,
puis nous stockons le résultat dans l’élément courant du tableau.

En sortant de la boucle, nous avons un tableau rempli de valeurs et nous
bouclons sur nous-mêmes en guise de fin de programme, comme il est usage en
microcontrôleurs (même si en pratique il serait plus à propos de les envoyer
ronfler dans un mode de veille profond).

Pour finir, il y a un ensemble de graphies ésotériques qui ne seront pas
décrites pour les raisons déjà évoquées.

Script pour l’éditeur de lien
-----------------------------

Pour finir son travail, la chaîne de compilation réalise une édition de lien.
Il s’agit d’une étape pendant laquelle elle place chaque fonction et variable
statique en mémoire puis calcule les adresses pour réaliser les appels de
fonctions et autres accès mémoire. Pour cela, l’outil a besoin de connaître
l’organisation de la mémoire du microcontrôleur.


Nous définissons donc un script minimaliste (là encore, ne l’utilisez pas dans
un vrai projet) pour l’éditeur de lien qui indique que la cible dispose de 2kio
de flash accessible en lecture/exécution ainsi qu’une RAM de 1kio accessible en
lecture/écriture/exécution et nous précisons les adresses de ces mémoires. Il y
a aussi diverses instructions pour placer les données en RAM ou en flash selon
leur nature.

Le fichier s’appellera `useless.ld`

::

	MEMORY {
		FLASH (rx) : ORIGIN = 0x08000000, LENGTH = 2K
		RAM (rwx) : ORIGIN = 0x20000000 , LENGTH = 1K
	}
	SECTIONS {
		.text : {
			*(.vector_table)
			*(.text)
		} >FLASH
		.data : {
			*(.data)
		} >RAM
	}

Bien sûr, les tailles indiquées ne couvrent pas toute la mémoire, le point
d’entrée n’effectue pas les traitements habituels réalisés avant l’appel au
main (initialisation de la RAM, préparation du cœur...), et plus généralement
le script est trop minimaliste pour une application réelle, mais ce sera
suffisant pour notre test.

Compilation
-----------

Compilons notre magnifique programme avec la suite `arm-none-eabi-gcc` qui est
un cross-compilateur pour ARM EABI (bare-metal), c’est-à-dire pour les cœurs
ARM sans système d’exploitation. Cette suite de compilation est disponible dans
les paquets de certaines distributions Linux ou compilable le cas échéant. De
nombreuses ressources peuplent les internets à ce sujet.

Pour ne pas nous embarrasser avec de trop nombreuses options de compilation
pour le moment, nous choisirons seulement le standard c++14 (autant programmer
avec un langage rénové) avec `-std=c++14`, embarquerons les symboles pour le
débuggage avec `-g`, n’inclurons pas les fichiers de démarrage standards avec
`-nostartfiles` et nous précisons le type d’instructions ARM compactes avec
`-mthumb`. Il faut aussi indiquer le fichier cpp à compiler, le nom de sortie
avec l’option `-o` et enfin le script de liaison à utiliser avec l’option à
l’apparence barbare `-Wl,-script=useless.ld` qui signifie passer l’option
`-script=useless.ld` à l’éditeur de lien.

::

	$ arm-none-eabi-g++ -g -std=c++14 -nostartfiles -mthumb -Wl,-script=useless.ld -o useless.elf useless.cpp

Le fichier est bien créé pour l’architecture ARM 32bits :

::

	$ file useless.elf
	useless.elf: ELF 32-bit LSB executable, ARM, EABI5 version 1 (SYSV), statically linked, not stripped


Hardware
========

Il existe plusieurs manières de flasher les STM32. Nous supposerons que nous
cherchons une solution à frais réduits pouvant flasher un microcontrôleur nu
acheté dans le commerce, avec lequel nous aurions réalisé notre propre carte
personnalisée.

Nous isolons alors deux méthodes (parmi d’autres) :

- L’utilisation du bootloader hardware

- L’utilisation d’un émulateur

Bootloader hardware
-------------------

La plupart des STM32 sont équipés d’un bootloader hardware (non écrasable) qui
permet notamment de flasher la puce sans émulateur. Les périphériques utilisés
par le bootloader et la méthode d’entrée dans celui-ci sont résumés dans la note
d’application "AN2606: STM32 microcontroller system memory boot mode".

Une des cartes qui a servi de base à cet article est équipée d’un STM32F303 qui
dispose d’un bootloader USB. C’est de celui-ci que nous allons parler. Pour
qu’il démarre, il faut que la carte soit équipée d’un quartz avec un choix de
fréquences spécifiques détaillées dans la note d’application sus-citée et que
la broche boot0 soit à VDD à la mise sous tension.

Émulateur
---------

L’émulateur est un appareil qui permet de dialoguer avec le cœur à travers une
liaison de débug. En particulier, les STM32 étant à cœur ARM Cortex-M*, ils
disposent d’un bus SWD permettant d’accéder aux fonctions de programmation et
débuggage avec un nombre réduit de broches.

Pour utiliser l’émulateur sur une carte réalisée nous-mêmes, nous avons besoin
de sortir les broches SWDIO et SWCLK, ainsi que les signaux VDD, VSS et RST sur
un connecteur. C’est tout ?  Oui.

Il nous faut par ailleurs bien sûr acquérir un émulateur. Tout émulateur ARM
supportant le bus SWD fera l’affaire.  Par exemple, le STlinkV2 pourra se
trouver facilement à un très faible coût. Il est d’ailleurs embarqué sur les
cartes d’évaluation de ST.

Flashage par USB direct
=======================

Lorsque le STM32 dispose d’un bootloader USB d’usine, et que les conditions
décrites précédemment sont réunies, il est possible de flasher le
microcontrôleur avec un simple câble USB. Il s’agit d’une procédure séduisante
au premier abord, mais prenez le temps de lire la méthode avec émulateur, car
celle-ci offre de bien meilleurs avantages.

Présence de la cible
--------------------

Tout d’abord, vérifions que le microcontrôleur est bien passé en mode
bootloader : (il faut que les conditions évoquées précédemment soient réunies)

::

	$ lsusb | grep ST
	Bus 001 Device 057: ID 0483:df11 STMicroelectronics STM Device in DFU Mode

Nous utiliserons l’outil `dfu-util` présent dans toute bonne (et moins bonne)
distribution Linux, et disponible sur d’autres systèmes comme Mac OS X ou
Windows. Cet outil permet de flasher le programme à travers le bootloader DFU
lorsque celui-ci est présent dans les STM32.

Commençons par lister les périphériques vus par l’outil avec `dfu-util -l`:

::

	Found DFU: [0483:df11] ver=2200, devnum=1, cfg=1, intf=0, alt=1, name="@Option Bytes  /0x1FFFF800/01*016 e", serial="206438702037"
	Found DFU: [0483:df11] ver=2200, devnum=1, cfg=1, intf=0, alt=0, name="@Internal Flash  /0x08000000/128*0002Kg", serial="206438702037"

Nous voyons qu’il est possible de programmer la flash en `alt=0` et que
celle-ci commence à l’adresse 0x08000000. Cette information nous sera utile
dans la suite même si elle peut être retrouvée dans la datasheet.

Extraire le code binaire
------------------------

Il faut savoir que le fichier elf est un conteneur qui recueille de nombreuses
informations telles que des données pour le débuggage. Dans notre cas, nous
extrayons la seule partie binaire pouvant être exécutée par la cible à l’aide
de `objcopy`.

::

	$ arm-none-eabi-objcopy -O binary useless.elf useless.bin

Flashage
--------

Enfin flashons ceci avec dfu-util (testé avec la v0.8). Nous indiquons que nous
prenons l’alternative 0 avec le paramètre `-a`, que nous programmons à partir
de l’adresse 0x08000000 avec l’option `-s` (le suffixe `:leave` indique que
nous souhaitons ensuite booter) et que nous voulons envoyer le programme avec
l’option `-D` :

::

	$ dfu-util -a 0 -s 0x08000000:leave -D useless.bin

Attention, l’envoi est rapide.

Le problème désormais, c’est que notre programme simpliste n’interagit pas avec
le monde extérieur et travaille donc ardemment caché dans un labyrinthe de
signaux électroniques. Même si un programme réel a souvent des impacts
externes, il peut être intéressant de connaître ce qu’il se passe à l’intérieur
et c’est un avantage énorme de la solution avec émulateur.

Flasher avec OpenOCD
====================

Cette solution nécessite l’achat d’un émulateur dont le coût est aujourd’hui
faible. Dans notre exemple, nous utiliserons un STlinkV2 avec le logiciel
OpenOCD (Open On-Chip Debugger) qui s’accommode de nombreux émulateurs. Ce
programme vous permettra de déverminer vos créations en plus de les flasher sur
la carte cible.

Lancer le serveur
-----------------

Dans l’utilisation que nous en ferons, OpenOCD servira en particulier de pont
entre le débugger gdb et le hardware à proprement parler, afin de traduire
les commandes du débugger en actions sur le matériel à travers l’émulateur de
notre choix.

Il agit comme gdbserver en ouvrant un socket sur lequel gdb peut venir se
connecter et dialoguer en utilisant un protocole particulier et documenté qui
est loin de notre propos. En ce qui nous concerne, il faut donc en premier lieu
que nous lancions ce serveur en précisant le nom des fichiers de configuration.
Puisque l’émulateur et le cœur sont déjà connus d’OpenOCD, nous lui indiquerons
les deux fichiers de configuration congruents.

::

	$ openocd -f interface/stlink-v2.cfg -f target/stm32f3x.cfg

OpenOCD supporte différents protocoles, c’est pourquoi il ouvre plusieurs ports
en écoute. Dans notre cas, le 3333 nous intéresse car c’est celui utilisé pour
la liaison gdbserver.

Connexion
---------

Entrons dans le vif du sujet avec gdb en console pour commencer.

::

	$ arm-none-eabi-gdb useless.elf

Cela démarre gdb en préchargeant les informations de l’exécutable (notamment
celles de débuggage) dans son interface. Nous allons lui donner quelques
commandes pour qu’il se connecte à OpenOCD puis qu’il redémarre la cible en
l’arrêtant avant le début.

Avant cela, assurez-vous que la broche boot0 n’est plus reliée à VDD, sinon le
processeur va sauter dans le bootloader usine et non votre programme ; un sacré
casse-tête pour comprendre ce qu’il se passe !

::

	(gdb) target remote 127.0.0.1:3333
	Remote debugging using 127.0.0.1:3333
	0x080001fe in ?? ()
	(gdb) monitor reset halt
	adapter speed: 1000 kHz
	target state: halted
	target halted due to debug-request, current mode: Thread
	xPSR: 0x01000000 pc: 0x080003c8 msp: 0x20009ffc

Maintenant, le débugger a établi une connexion avec le processeur et contrôle
son exécution. Il est arrêté et prêt à suivre nos instructions. Nous
disposerons alors des facilités de déverminage que nous trouvons habituellement
sur PC telles que l’exécution pas-à-pas, les points d’arrêt, l’inspection de
mémoire, lecture des registres... Les considérations temporelles et la gestion
des interruptions, inhérentes dans le contexte des microcontrôleurs, viendront
cependant parfois bousculer ce confort.

À l’heure actuelle, OpenOCD n’a rien flashé.

Déverminage
-----------

Si vous avez déjà flashé ce même programme avec la méthode bootloader, ou avec
l’émulateur, amusons-nous à vérifier son exécution.

Il est important que la version du fichier elf et du programme en mémoire dans
le microcontrôleur soit rigoureusement la même. En fait, la cible ne connait
que les valeurs binaires qu’elle a en mémoire et ne fait aucun lien avec votre
programme humain. C’est le débugger qui traduira à la volée les informations
renvoyées par la cible en se référant au fichier elf qui lui a été fourni. En
cas d’incohérence, les informations que traduira gdb ne seront pas justes et
vous induiront facilement en erreur.

Commençons par insérer un breakpoint dans la fonction `main` puis lançons
l’éxécution avec l’instruction `continue`. Une fois arrêté, exécutons la
prochaine instruction avec `next` et affichons la valeur de la variable `y`
avec `print`. Nous utiliserons les formes abrégées, respectivement `b`, `c`,
`n` et `p`.

::

	(gdb) b main
	Breakpoint 1 at 0x800000e: file useless.cpp, line 4.
	(gdb) c
	Continuing.
	Note: automatically using hardware breakpoints for read-only addresses.

	Breakpoint 1, main () at useless.cpp:4
	4	        float y = 0.0f;
	(gdb) n
	6	        for (float & m : measures) {
	(gdb) p y
	$1 = 0

Parfait, nous pouvons nous arrêter dans le programme pour inspecter des valeur.

Il est toutefois parfois plus commode, et certainement plus convivial, de
disposer d’un logiciel graphique pour vous assister dans le déverminage. Fort
heureusement, l’outil gdb est supporté par de nombreux environnements
graphiques comme eclipse, nemiver, QtCreator, ddd et bien d’autres qui pourront
vous aider dans votre tâche.

Nous n’allons évidemment pas tous les passer en revue. L’important est de leur
indiquer que vous n’utiliserez pas gdb classique, mais le gdb de la chaîne de
compilation croisée, en l’occurrence `arm-none-eabi-gdb`.  Par exemple, ddd
attend l’option `--debugger`. Pour plus de commodités, nous lui indiquons aussi
de se connecter au moniteur et de redémarrer la cible pour nous avec
`--eval-command`.

::

	ddd --debugger arm-none-eabi-gdb --eval-command "target remote 127.0.0.1:3333" --eval-command "monitor reset halt" useless.elf

Ce debugger graphique nous permet par exemple de mettre un point d’arrêt sur la
boucle finale et afficher dans un graphique les valeurs du tableau `measures`.
Nous voyons alors que la formule employée était celle de la charge d’un
condensateur.

.. container:: aligncenter

	.. image:: /images/stm32_articles/flash_dddgraph.png
		:alt: Graphe DDD

Flasher
-------

Nul besoin de quitter le debugger pour programmer le microcontrôleur.

Dans un premier temps nous utilisions la commande `load` pour charger le
programme. Cependant, cette méthode ne fonctionnait pas à chaque fois. Après
investigation, il s’avère que la commande n’efface pas les secteurs avant de
programmer, ce qui est pourtant nécessaire avec la technologie de flash
employée dans les STM32.

Heureusement, il existe la commande `monitor program`, fournie par le moniteur
OpenOCD, qui réalise un effacement automatique avant d’écrire dans les secteurs
de la mémoire interne.

::

	(gdb) monitor program useless.elf
	adapter speed: 1000 kHz
	target state: halted
	target halted due to debug-request, current mode: Thread
	xPSR: 0x01000000 pc: 0x080003c8 msp: 0x20009ffc
	adapter speed: 8000 kHz
	** Programming Started **
	auto erase enabled
	target state: halted
	target halted due to breakpoint, current mode: Thread
	xPSR: 0x61000000 pc: 0x2000003a msp: 0x20009ffc
	wrote 2048 bytes from file useless.elf in 0.184147s (10.861 KiB/s)
	** Programming Finished **

Maintenant que le programme est dans sa mémoire interne, la carte peut vivre sa
vie sans vous.

Épilogue
========

Ce billet est loin d’être exhaustif et le programme est nullissime ; le but
était de présenter brièvement quelques outils pour flasher cette famille de
microcontrôleurs. Nous avons d’ailleurs eu l’occasion de faire un bref détour
vers le débuggage. Notez que les outils exposés ne sont pas spécifiques à la
famille STM32 (y compris l’émulateur employé). Ils supportent d’autres puces
qui peuvent donc être manipulées de manière similaire.

Il va falloir maintenant s’intéresser au logiciel à produire pour tirer parti
des nombreuses fonctionnalités des microcontrôleurs que nous manipulerons. Dans
ce domaine, les territoires à explorer sont vastes et ne manqueront pas de nous
surprendre.

