================
Lampes orbitales
================

:slug: lampes-orbitales
:projet_realisation: v1 terminée -brightgreen
:projet_etat: fonctionnel -brightgreen

.. image:: /images/bannieres_projets/lampes-orbitales.1.jpg
	:alt: Lampes Orbitales

Qu'est ce que c'est ?
=====================

Les lampes orbitales sont l'association d'un pupitre interactif capable de
reconnaître des pastilles de couleur sur son plateau et de lampes connectées
prévues à cet effet.

.. container:: aligncenter

    [flickr:id=28834429884]

Ce projet a été mis en place pour les évènements suivants :

- `BienVenus sur Mars`_ 2016 (du 27 avril au 1er mai - `Photos <https://www.flickr.com/photos/126718549@N08/albums/72157667688278672>`__).
  C'est l'évènement pour lequel nous avons créé ce projet.
- `Les Siestes Teriaki`_ 2016 (les 27 et 28 août - `Photos <https://www.flickr.com/photos/126718549@N08/sets/72157671412072762>`__).

Cet article parle principalement du pupitre interactif et du logiciel de
reconnaissance des pastilles. Pour les lampes connectées, il faut aller voir les
Laumios_ !

.. _Laumios: /pages/Laumios.html
.. _BienVenus sur Mars: http://www.bienvenus-sur-mars.fr/
.. _Les Siestes Teriaki: http://www.teriaki.fr/

Le pupitre interactif
=====================

Le principe
-----------

Que faire avec du bois de palette, du verre, une webcam et des Laumios (entre autres choses) ? Sûrement plein de choses ! 

Mais nous, on en a fait un pupitre interactif ! Amusez-vous à bouger les pastilles sur sa vitre, enlevez-les, ajoutez-en, cumulez-en côte-à-côte... et regardez le résultat !

.. container:: aligncenter

    [flickr:id=29617446001]

Sur le principe, une webcam surveille le pupitre à la verticale de celui-ci. Un logiciel vient périodiquement faire de la reconnaissance de cercles de couleur sur l'image renvoyée par la webcam. Les couleurs reconnues sont alors mélangées et envoyées aux différents Laumios connectés, qui illumineront la pièce de mille couleurs.

Le pupitre
----------

Rien de particulier à dire sur le pupitre actuellement... Il est actuellement constitué de bois de palette, de tissu noir de récupération, d'une vitre en verre. Il s'accompagne d'une barre de support portant lampe et webcam, installable sur un trépied.

.. container:: aligncenter

    [flickr:id=29458564955]


Le logiciel
-----------

Le moteur de calcul
~~~~~~~~~~~~~~~~~~~

Le logiciel est actuellement disponible sur le `dépôt Github`_ des Laumios. Il s'agit d'un script python basé sur OpenCV pour la reconnaissance de formes.
Pour lancer le script, il suffit de lancer le script pupitre.py en tapant dans le terminal la ligne de commande suivante :

.. code-block:: bash

  python pupitre.py <webcam id>

Le webcam id n'est pas nécessaire, sauf si plusieurs webcams sont branchées et reconnues par le PC utilisé. La valeur par défaut est 0.


A chaque pas de temps, les cercles de couleur sont identifiés et traités par le script. Chaque cercle est défini par son centre et sa taille sur l'image traitée, la couleur est enregistrée en HSV (Teinte - Saturation - Valeur).

Les Laumios sont aussi considérés par le script. Ceux-ci sont placés virtuellement sur une carte adimensionnée (les valeurs des cordonnées x et y sont comprises entre 0 et 1), qui est mise en correspondance avec l'image renvoyée par la webcam.

A chaque point de couleur identifié est associé un profil de décroissance en fonction de la distance à ce point. Ce profil de décroissance s'applique à la composante Valeur de la couleur (variation entre noir à 0% et couleur pleine à 100%), mais aussi à la composante Saturation (variation entre une couleur "terne" à 0% et une couleru vive à 100%). La teinte est considérée comme une valeur d'angle (comprise entre 0% et 100% d'un tour complet).

Pour effectuer le mélange de couleurs sur un Laumio, tous les points de couleur sont appelés pour calculer au centre du Laumio considéré les valeurs HSV, considérant le profil de décroisance. Toutes les composantes Valeur sont sommées (et bornées entre 0 et 1). Pour les composantes Teinte et Saturation, il s'agit d'une somme vectorielle, la Saturation étant l'amplitude et la Teinte étant l'angle.


Le script de configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~

Ce qui n'a pas été dit précédemment, c'est que le moteur de calcul fait aussi tourner un petit serveur UDP qui le rend confgurable par un système local extérieur. Le script control_pupitre.py remplit cette fonction et se lance simplement avec la ligne de commande suivante :

.. code-block:: bash

  python control_pupitre.py

Le script demande alors à l'utilisateur les modifications à adopter pour un Laumio à choisir. Chaque Laumio représenté dans le script est configurable sur les paramètres suivants :

- Taper "1" to set position for the Laumio. The coordinates x and y are floats between 0 and 1, they represent the relative position of the Laumio on the webcam screen. the origin is set on the upper left corner.
- Taper "2" pour forcer le Laumio à une couleur RGB fixe
- Taper "3" pour libérer la couleur forcée
- Taper "4" pour donner l'IP du vrai Laumio correspondant
- Taper "q" pour quitter le script

Le script est suffisamment souple pour utiliser un fichier de configuration via la ligne de commande suivante :

.. code-block:: bash

  python control_pupitre.py < <configuration file>

Le contenu d'un fichier de configuration est par exemple le suivant (qui place le Laumio n'°1 au centre de la carte et le fixe à la couleur verte) :

.. code-block:: bash

  1
  1
  0.5
  0.5
  2
  1
  0
  255
  0
  q


Le résultat à l'écran
~~~~~~~~~~~~~~~~~~~~~

.. container:: aligncenter

    [flickr:id=28834342654]

.. container:: aligncenter

  .. image:: /images/laumioDesk/laumioDesk_screenshot.jpg
   :height: 280px
   :alt: Vue depuis une webcam 


.. _dépôt Github: https://github.com/haum/Laumio/tree/master/Pupitre


Evolution du projet
===================
La pioche à idées
-----------------
Des idées, il y en a toujours à revendre... ou à laisser gratuitement à disposition. En voici quelques-unes pour qui voudrait aider sur les Lampes Orbitales mais ne saurait pas quoi faire !

- **Plus de magie !** Améliorer l'éclairage et la sensibilité aux variations de lumière, continuer de travailler pour pouvoir filmer les languettes depuis sous le pupitre.
- **Plus de solidité !** Faire des pastilles en bois.
- **Plus de complexité !** Faire réagir le logiciel différemment selon la taille des pastilles, leur forme ou les symboles inscrits.
- **Plus de ludique !** Jeux de conquête ou collaboraitfs avec un second pupitre, mappage aléatoire changant...
- **Plus de musique !** Et si on faisait une table de mixage avec le pupitre ?
- **Plus d'interopérabilité !** Et si ce script python utilisait un fichier JSON pour charger les Laumios comme un grand ? Oh, et si on faisait en sorte que LaumioAnimator_ puisse le lire aussi ?
- **Plus de configurabilité !** Rendre configurables certaines variables codées en dur. Qui a parlé de fichiers de conf ?

.. _LaumioAnimator: /pages/Laumio-animator.html