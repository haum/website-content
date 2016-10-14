==============
LaumioAnimator
==============

:slug: laumio-animator
:projet_realisation: à continuer -yellow
:projet_etat: fonctionnel -brightgreen

.. image:: /images/bannieres_projets/laumio-animator.1.jpg
	:alt: LaumioAnimator


Qu'est ce que c'est ?
=====================
LaumioAnimator, c'est un compositeur de partitions lumineuses développé en Qt/C++, pour accorder les laumios_ avec un morceau de musique. Ses sources sont disponibles sur le `dépôt Git dédié`_. Il a été brièvement utilisé pendant les `Siestes Teriaki`_ 2016.

.. _Laumios: /pages/laumios.html
.. _Siestes Teriaki: http://www.teriaki.fr/
.. _dépôt Git dédié: https://github.com/haum/laumio_animator/


LaumioAnimator en moins bref
============================
Le moteur d'animation
---------------------
Le coeur de LaumioAnimator réside dans son moteur d'animation, représenté par la classe **LaumioAnimation** (fichiers laumioanimation.h et laumioanimation.cpp). Celui-ci a, nécessairement dans l'ordre indiqué, besoin des informations suivantes :

- Au moins un objet **Laumio**, représenté par la classe Laumio (fichiers laumio.h laumio.cpp). Si l'adresse IPv4 d'un Laumio physique est spécifiée, et si ce Laumio et l'ordinateur utilisé sont sur le même réseau, alors la lampe réagira à la partition créée quand celle-ci sera jouée. S'il n'y a aucune adresse indiquée, le moteur ne fait que simuler la partition.
  
  L'attribut *m_laumios* de **LaumioAnimation** est un vecteur (un tableau dynamique) stockant des structures **LaumioInfo**. Chaque structure **LaumioInfo** contient le pointeur d'un objet **Laumio** et un vecteur des pointeurs vers des objets **Animation**. La méthode *LaumioAnimation::newLaumio()* se charge d'ajouter des **Laumio** au moteur.

- Au moins une animation, qui doit être un objet héritant de la classe abstraite **Animation**, et ce pour chaque objet **Laumio** pointé. Si aucune animation n'est indiquée, le moteur ne plante pas mais rien ne se passera.
  
  L'attribut *m_animationsStorage* est la liste de toutes les animations. Cet attribut est un vecteur stockant les pointeurs des objets **Animation** générés. Les pointeurs des animations sont aussi répartis dans *m_laumios* en fonction du **Laumio** auquels ils sont rattachés. La méthode *LaumioAnimation::newAnimation(int, QString)* se charge d'ajouter des animations au moteur.
  
  Une animation, dont on parlera plus précisément dans la section suivante, doit obligatoirement avoir un instant de début *fromStart*, une durée *duration*, un priorité *priority* et se définit par un "factoryName" qui est relié à la classe fille considérée.

- Eventuellement un fichier sonore, dont l'adresse est stockée sous forme de *QString* par l'attribut *m_audioSource* (voir la méthode *LaumioAnimation::set_audioSource()*).

Une fois la partition dûment complétée (même de manière minimaliste), le moteur est prêt à être utilisé, contrôlé par les méthodes *play(int)*, *pause()* et *stop()*. Le moteur est cadencé par un timer qui lui fait lancer l'animation à chaque tick. L'intervalle de temps est défini en dur à 100ms. Un calcul d'animation est aussi forcé au début et à la fin de chaque animation. Le moteur d'animation corrige aussi d'éventuels décalages liés aux temps de calcul en se confontant à l'horloge du système d'exploitation. 

 Actuellement, le moteur ne gère pas indépendamment toutes les leds d'un même Laumio. Celui-ci s'allume intégralement d'une seule couleur.


Les animations
--------------
Toutes les animations héritent de la méta-classe **Animation** . Toutes les animations ont nécessairement deux attributs indiquant en secondes le temps de début *fromStart* et la durée d'animation *duration*. A ceci s'ajoute la priorité *priority*, qui permet de superposer des animations (et évite ainsi certains problèmes de raccord) , la valeur de priorité la plus haute donnant... la priorité.  Les couleurs sont gérées en RGB ou spécifiées par des noms "standards".

Les animations disponibles et éprouvées sont les suivantes :

- Animation constante **ConstantColor** : Joue une couleur constante, définie par un attribut *color*.


- Animation progressive **ProgressiveColor** : fait varier la couleur de *firstColor* vers *lastColor*, en suivant une forme progressive *slopeSignal*. Actuellement, la seule forme progressive proposée (celle par défaut) est "linear", soit un progression affine entre les couleurs de début et de fin.


- Animation pulsatile **PulsingColor** : fait varier la couleur entre *lowerColor* et *upperColo*, en suivant une forme oscillante *pulseSignal*, de fréquence *frequency* et de retard *delay*. Actuellement, la seule forme oscillante disponible (celle par défaut) est "sinus".
  A noter que dans la définition de la classe, la couleur varie autour d'une moyenne *meanColor* avec une amplitude *varColor* et une pulsation *pulsation* en guise de fréquence.


- Animation pulsatile bornée **BoundedPulsingColor** : fait varier la couleur depuis un intervalle compris entre *firstLowerColor* et *firstUpperColor* vers un intervalle compris entre *lastLowerColor* et *firstLowerColor*. L'évolution de la borne haute *upperColor* (resp. *la borne basse lowerColor*) est donnée par une forme progressive *upperBoundSignal* (resp. *lowerBoundSignal*) entre *firstUpperColor* et *lastUpperColor* (resp. *firstLowerColor* et *lastLowerColor*). A chaque pas de temps, la couleur est choisie par une forme oscillante dont les paramètres d'amplitude et de moyenne sont calculés à partir des deux bornes, la forme *pulseSinal*, la fréquence *frequency* et le retard *delay* étant à spécifier.


L'interface
-----------
Gérer un Laumio
~~~~~~~~~~~~~~~~~
Pour ajouter un Laumio, il faut appuyer sur le bouton "New Laumio" à gauche dans le GUI.
Pour sélectionner un Laumio, il faut faire un clic gauche à proximité du nom de celui-ci. 
Pour supprimer celui-ci (et par la même toutes les animations qui lui sont rattachées), il faut actuellement faire un clic droit à proximité dudit Laumio.

La preview
~~~~~~~~~~
L'onglet de preview permet de nommer un Laumio sélectionné, de lui attribuer une adresse IP, et de le positionner précisément sur la map. Il est de même possible de contrôler les couleurs des leds de manière indépendante (la valeur 255 signifie "toutes les leds") et de lancer des animations prédéfinies. 

Cet onglet permet de différencier les laumios, notamment quand il s'agit ensuite de les positionner précisément dans une pièce.

.. container:: aligncenter

  .. image:: /images/laumioAnimator/laumioAnimator_preview.jpg
     :height: 360px
     :alt: LaumioAnimator "preview" tab

La map
~~~~~~
La map est un carré dont les coordonnées sont pour le moment comprises entre (0,0) et (1,1). L'origine est située en haut à gauche, le x augmentant en allant vers la droite et les y en descendant. Il est possible de déplacer les Laumios sur la map en glisser-déplacer pour représenter grossièrement la disposition d'une installation de Laumios.

.. container:: aligncenter

  .. image:: /images/laumioAnimator/laumioAnimator_map.jpg
     :height: 360px
     :alt: LaumioAnimator "map" tab


La timeline
~~~~~~~~~~~
La timeline représente la partition lumineuse, là où l'on va pouvoir composer ! Pour ajouter une animation à un Laumio (ou au canal associé, en réalité), il faut cliquer dans le canal directement aligné avec le nom du Laumio visé.

  - Un clic gauche dans le vide du canal va permettre d'ajouter une animation.
  - Un clic gauche dans une animation permet de modifier ses paramètres. 
  - Un clic droit sur une animation la supprime.
  - Les glisser-déplacer sont possibles pour changer le temps de début d'une animation dans un canal.
  - Un copier-coller est possible : ctrl+clic gauche sur une animation permet de la copier, ctrl+clic droit permet de la coller dans le canal pointé par le curseur.

.. container:: aligncenter

  .. image:: /images/laumioAnimator/laumioAnimator_timeline.jpg
     :height: 360px
     :alt: LaumioAnimator "timeline" tab

La lecture
~~~~~~~~~~
La lecture est permise par les boutons Play/Stop et Replay/Pause.

- Bouton Play/Stop :

  - Play permet de jouer une partition uniquement à partir du début.
  - Stop permet d'arrêter totalement une parition.
  
- Bouton Replay/Pause :

  - Replay permet de jouer une partition à partir d'un point spécifié. Ce point est un temps en millisecondes indiqué dans l'élément de contrôle à droite du bouton.
  - Pause permet d'arrêter la partition au point de lecture en cours.

La gestion complète de la lecture ne marche pour l'instant que quand un fichier audio est chargé. En effet, sans fichier audio, pas de barre de temps en haut de l'interface, pas de décompte du temps et pas de curseur de lecture sur les animations.

Le JSON
~~~~~~~
Le logiciel est capable de charger ou d'enregistrer des compositions via un fichier JSON, en s'appuyant sur les méthodes dédiées dans le moteur d'animation. Le chemin vers une source audio peut aussi être ajouté manuellement dans le JSON.
La structure générale du fichier généré est la suivante (avec l'exemple d'une seule animation constante noire de 2,5 secondes pour un laumio lambda) :

.. code-block:: javascript

  {
      "animations": [
          {
              "anims": [
                  {
                      "color": "#000000",
                      "duration": 2.5,
                      "fromStart": 0.0,
                      "priority": 5,
                      "type": "ConstantColor"
                  },
                  ...
              ],
              "laumio": {
                  "ip": "192.168.0.1",
                  "name": "Laumio",
                  "port": 6969,
                  "x": 0,
                  "y": 0.25
              }
          },
          ...
      ],
      "audioSource": "file:///tmp/audioSource.wav"
  }



Evolution du projet
===================
Les signaux
-----------
Les signaux sont l'évolution à venir pour créer un système complexe d'animations. Ceux-ci ne remettent pas en cause les animations déjà existantes mais offrent un moyen de les enrichir considérablement et de proposer des fonctions de calcul de couleur totalement configurables et inédites, dépendant uniquement de la créativité du développeur ou du copositeur.

Dans le principe, un signal est un objet utilisant le temps d'animation pour renvoyer une valeur entre 0 et 1, qu'il faudra ensuite utiliser dans une animation avec des paramètres de couleur. La particularité est qu'un signal peut être développé pour appeler plusieurs autres signaux et les mélanger. Il est donc facile d'imaginer une pléthore de signaux canoniques calculant d'une part des valeurs ou d'autre part associant des 

Le tout est importable ou exportable en JSON. Même si la notation devient potentiellement lourde avec un énorme enchaînement de signaux (sauf en améliorant la représentation dans le JSON) mais que l'on a la folie de vouloir écrire à la main la description du signal, il faut alors dérouler cet enchaînement en suivant le principe de la `notation polonaise`_.

.. _notation polonaise: https://fr.wikipedia.org/wiki/Notations_infix%C3%A9e,_pr%C3%A9fix%C3%A9e,_polonaise_et_postfix%C3%A9e

La pioche à idées
-----------------
Des idées, il y en a toujours à revendre... ou à laisser gratuitement à disposition. En voici quelques-unes pour qui voudrait aider sur LaumioAnimator mais ne saurait pas quoi faire !

- **Plus de facilité !** Ajouter une fonctionnalité de recherche de laumios connectés au réseau.
- **Plus de mémoire !** Ajouter une fonctionnlité d'enregistrement de la map avec les infos des Laumios.
- **Plus de simplicité !** Forker LaumioAnimator_ pour le rendre utilisable sur ordiphone et pour répondre à des besoins simples. 
- **Plus de complexité !** Gérer les animations des laumios led par led et non pas en remplissage intégral.

.. _LaumioAnimator: /pages/laumio-animator.html

