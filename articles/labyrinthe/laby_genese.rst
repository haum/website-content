=============================
Génèse du labyrinthe Initiati
=============================

:date: 2017-03-07 22:30
:category: projets
:slug: laby_genese
:authors: JackDesBwa, Lode runner, Gras
:summary: Histoire du labyrinthe
:tags: projet_labyrinthe_initiati

Le labyrinthe du HAUM, vous connaissez. Mais connaissez-vous son histoire ?

Tout a commencé par ceci :

.. container:: aligncenter

   	.. image :: https://photos.haum.org/small/ggj2016/p001_24152983033_o.jpg

Labyrinthe originel
===================

Prémices
--------

Ainsi commence le labyrinthe : par un brainstorming à la `global game jam`_
2016. Le thème *rituals* nous a fait tourner en bourrique pendant de nombreuses
(et longues) heures, tant et si bien que nous cumulions près de 24h de réflexions
intenses quand les premières idées ont commencé à... esquisser un début d'embryon
de germe de jeu.

.. _`global game jam`: http://globalgamejam.org/

Prodrome
--------

Une fois la crise de la page(/nuit) blanche passée, il nous restait la moitié
du temps pour créer notre jeu. De nombreux essais-erreurs ont mené à la
réalisation d'un divertissement associant un plateau et des cartes à jouer.
Dans l'optique d'un chemin initiatique, nos lurons ont imaginé que les joueurs
dussent déplacer leurs personnages dans un dédale pour aller y quérir des
objets dans un ordre imposé par le rituel.

Le groupe s'est divisé pour mieux s'acquitter de la tâche : certains se sont
occupé des cartes, des règles, des flexagones (tout ceci mériterait
probablement un article en soi) et d'autres se sont secoué les méninges pour
produire le plateau. C'est ce dernier qui nous intéresse dans cet article.

Plus qu'un simple labyrinthe traditionnel, nous nous sommes lancés dans la
réalisation d'un labyrinthe à états. Il s'agit d'un dédale dans lequel la même
case peut avoir, selon le chemin d'accès, une localité différente dans l'espace
des solutions. Peut-être pourrait-on dire que dans ces labyrinthes, deux
personnes se rencontrant auront des perspectives différentes selon leur passé,
à moins qu'il ne se rencontrent pas, étant dans des branes de labyrinthes
distinctes.  En fait, c'est comme si le plateau était un labyrinthe plus grand
replié sur lui-même où les explorateurs traverseraient le multivers en
empruntant des trous de ver à foison.

Vous suivez ? Nous non plus.

Protocole
---------

Cessons cet imbroglio théorique et passons à la pratique avec la construction
de ce joli méli-mélo de couloirs.

Dans un premier temps, nous définissons la règle rituelle pour évoluer sur le
plateau : rouge, vert, bleu est l'ordre à suivre. Dans cette idée d'une
sempiternelle répétition, une forme générale en cercles concentriques s'est
imposée. Voilà le squelette de notre plateau que nous dessinons et imprimons
sans aucune fioriture.

Deux cerveaux particulièrement dérangés (ie. avec de bonnes doses de maths
dedans) s'attèlent à la lourde tâche de définir les passages autorisés et donc
la couleur de chacune des quelques 64 portes.

Dans un premier temps, il s'agit de définir une convention de nommage : chaque
case, chaque porte, chaque état dans lesquels un joueur peut se trouver est
nommé (avec un code générable et interprétable par un outil numérique). Par
exemple, les cases reçoivent un nom composé d'une lettre et d'un chiffre. La
lettre représente l'anneau sur lequel elle est et le chiffre est déterminé par
son azimut.

Mais pourquoi s'embêter à choisir de tels noms particulièrement inesthétiques ?
Pour laisser les ordinateurs calculer à notre place, pardi !

Maintenant, il est facile de générer la liste de tous les passages possibles
d'une case à l'autre, en y ajoutant l'état du joueur et même, soyons fous,
réaliser un graphe_ pour étudier les parcours possibles. Avec les mêmes données
de départ, nous pouvons aller jusqu'à dessiner le plateau sans nous embêter à
placer manuellement l'ensemble des portes. Nous pouvons alors passer bien  plus
de temps à soigner l'esthétique ou la complexité sous-jacente du labyrinthe.

Prototype
---------

Maintenant que nous avons les outils, il est temps de sortir notre plus grand
atout : les crayons de couleur !

Nous traçons quelques chemins et vérifions avec l'outil informatique quelles
nouvelles routes sont nées de l'enchevêtrement des sentiers. Il y a là une
grande complémentarité entre les cerveaux créatifs et l'informatique, dont le
retour implacable valide ou désavoue la folie exprimée.

Les documents de travail deviennent vite imcompréhensibles pour les profanes :

.. container:: aligncenter

   	.. image :: https://photos.haum.org/small/ggj2016/caa2co2xeaejazc_32987474855_o.jpg

.. _graphe: https://fr.wikipedia.org/wiki/Th%C3%A9orie_des_graphes

Proposition
-----------

Les heures passent, les cerveaux bouillonnent et finalement un jeu est produit.
Il est jouable (youhou !) et même visuellement sympathique, mais les
déplacements sur le plateau sont effectivement très difficiles à planifier.

Pour conclure cette première partie, voici la carte des déplacements générée
par l'ordinateur :

.. container:: aligncenter

	.. image :: https://photos.haum.org/small/ggj2016/caa342zwaaaanz3_32862394751_o.jpg


Labyrinthe original
===================

Dendrochronologie
-----------------

Tel l'arbre qui croît avec les années, notre labyrinthe voulait se faire plus
grand, pour faire un effet bœuf. L'échéance fatidique des 48h dépassée,
n'imaginons pas sa croissance échue parce qu'il était tard.

Cinq mois trois quarts après sa naissance, le sujet reprend vie. Nous
remarquons que la dernière couronne, privée de portes, pourrait en être
pleinement peuplée.

C'est parti, nous modifions le programme et la sentence tombe : il y aura
obligatoirement au moins une sortie. Qu'à cela ne tienne, profitons de
l'opportunité pour augmenter la richesse de l'expérience.

Ainsi, il y a une multitude d'entrées par lesquelles les gens peuvent
s'engouffrer dans le labyrinthe. Et une fois que le peuple y est, il lui faut
en sortir. Et pour ça, il y a bel et bien 36 solutions.

.. container:: aligncenter

    .. image:: https://raw.githubusercontent.com/haum/initiati/master/plateau.jpg
        :alt: Plateau du labyrinthe augmenté
        :width: 600

Démesure
--------

Mais ce n'était pas suffisant : la création pouvait encore s'étendre.

Et si l'on disséminait des dandys dedans ? Cette délicieuse idée débile d'un
dédale détonnant nous décida à le dessiner dare-dare dans des dimensions
démesurées. Dès lors, déterminés, nous dûmes édifier ladite dardière, un défi
diligemment dirigé.

Trève d'allitérations, vous trouverez la construction de ce labyrinthe géant
détaillée dans la page du projet_. Nous avons présenté celui-ci aux siestes
Teriaki 2016.

.. container:: aligncenter

	.. image :: https://photos.haum.org/small/teriaki2016/p1120571_29350204682_o.jpg

S'ensuivit un stupéfiant succès et sa suprême satisfaction.

.. container:: aligncenter

	.. image :: https://photos.haum.org/small/teriaki2016/p1120611_28836842273_o.jpg

.. _projet: /pages/labyrinthe.html
