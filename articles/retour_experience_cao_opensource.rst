========================================
CAO 3D opensource - Retours d’expérience
========================================

:date: 2025-04-12 18:30
:tags: 3d, cao, freecad, openscad, cadquery, build123d, python
:category: CAO
:slug: cao-3D-opensource-retours-d-experience
:authors: manu
:summary: Retours d’expérience sur quelques logiciels opensource de CAO 3D

Contexte
--------

Je transitionne depuis SolidWorks. C’est un super outil que j’utilisais
de manière professionnelle en bureau d’étude pour dessiner des ouvrages
métalliques.

Maintenant que j’ai quitté le milieu, je me suis mis à la recherche
d’outils opensource pour continuer à dessiner en 3D.

Principalement, je cherche un ou des outils permettant d’atteindre ces
buts:

- avoir un format ouvert et non limité à la version que j’utilise : le
  modèle de SolidWorks, c’est qu’un modèle créé avec SolidWorks 2015,
  enregistré dans SolidWorks 2016 (sans changement), n’est plus éditable
  dans SolidWorks 2015. Il faut donc avoir la même version pour
  collaborer et la licence n’est pas donnée (même s’il existe une
  licence “Maker” en abonnement, ce n’est pas pérenne)
- pouvoir versionner mes modèles avec Git ou un outil plus adapté.
  SolidWorks a un module “PDM” qui coûte un bras, et qui fonctionne bien
  en entreprise, mais je doute que ce soit possible d’en faire une
  instance quelque part.
- avoir un outil stable sur lequel je puisse compter.
- l’outil doit me permettre de réaliser des modèles modulaires et
  paramétriques.
- l’outil doit être disponible sous Linux

J’ai donc testé quelques logiciels opensource pour tenter de répondre à
ces besoins, réalisant quelque chose de similaire à
`Gridfinity <https://gridfinity.xyz/>`__. L’idée est de pouvoir, d’une
manière ou d’une autre donner un nombre de modules et de générer grille
et boîte. L’idée est simple, mais permet de valider les points suivants
:

- pouvoir faire des éléments distincts (des pièces, ou *parts*) et les
  réutiliser
- idéalement, pouvoir utiliser des éléments déjà existants et créer un
  assemblage avec
- pouvoir entrer des paramètres quelque part et voir le modèle s’adapter
- exporter le modèle fini pour le partager, l’importer dans d’autres
  outils ou juste bouffer de la place sur mon disque
- écrire un comparatif d’outils [STRIKEOUT:en prenant l’apéro
  tranquilou]

Dans ces comparatifs, je ne vais pas parler de l’interface du logiciel,
sauf si c’est tout à fait nécessaire.

FreeCAD (en v1)
---------------

J’ai découvert `FreeCAD <https://www.freecad.org/>`__ à l’époque où je
dessinais professionnellement avec Sketchup pour les rendus, donc
autours de 2012.

De temps à autre, j’y passais quelques heures pour voir comment le
logiciel évoluait, mais je n’ai jamais eu le courage de “faire le pas” :
trop compliqué. Et quand je suis passé à SolidWorks en 2014 : pas assez
intuitif, pas assez stable pour en faire mon outil de dessin.

La version 1, sortie en 2024, a gommé une bonne partie des soucis que
j’avais pu rencontrer sur mes derniers essais : référencer un élément
dans un autre est maintenant *gérable* : si l’élément d’origine change
et que la référence n’est plus possible, on ne finit pas avec un modèle
tout cassé, juste un modèle à reprendre : supprimer les anciennes
références et remplacer par des nouvelles.

**Les pour :**

- c’est proche de SolidWorks sur la manière de construire : on dessine
  des *esquisses* (dessins 2D, avec côtes contraintes) et on applique
  des opérations dessus.
- il y a un système de création d’assemblage, où l’on peut placer des
  pièces les une par rapport aux autres, en appliquant des contraintes.
- il y a un système de **modules**, permettant d’ajouter des
  fonctionnalités
- les formats d’exports sont variés (dont du STEP)
- il est possible d’importer pas mal de formats différents et de bosser
  avec (ex : prendre un STL comme base et faire une empreinte dedans)
- il y a un module de mise en plan pour, par exemple, générer des PDF
  pour revue, fabrication en ateliers ou de demandes de devis
- il est possible de nommer des cotes dans une *esquisse* et y faire
  référence ailleurs (autre esquisse, opération, …)
- il est possible de référencer des valeurs d’opérations (ex:
  ``extrusion1.Lenght``)
- il est possible d’écrire des macros en Python
- il y a des modules très intéressants (pour générer de la visserie, des
  filetages, des engrenages, etc…)
- il y a un module “feuille de calcul” (sans troller SolidWorks, là
  c’est intégré, pas besoin d’Office360 en sus). Il est possible de
  nommer les cellules et de les utiliser en référence dans les modèles.
  Il est aussi possible de l’utiliser comme liste de *variantes* d’une
  même pièce. C’est top pour centraliser le côté paramétrique

**Les contre :**

- au sein d’une même *esquisse*, il n’est pas possible d’utiliser une
  référence déclarée dans ce dernier. C’est ultra pénible, on se
  retrouve par exemple à faire 3 segments de lignes de même longueur
  plutôt que de pouvoir faire un ``la_cote / 3``.
- le résolveur de contraintes n’est pas parfait et il m’arrive
  régulièrement d’avoir à reprendre toute une pièce étape par étape,
  parce qu’un changement de paramètre a résulté en un point invalide (ex
  : un point à 20mm *à droite* de l’axe Y se retrouve à 20mm *à gauche*
  après recalcul). Il y a des astuces pour améliorer la situation, mais
  je trouve que c’est difficile à appréhender *avant* d’avoir le souci.
- éditer une *esquisse* de “début” de pièce fait que l’ensemble de la
  pièce est recalculée à chaque modification (sans quitter l’édition),
  rendant l’ensemble lent sur des pièces/assemblages de petite taille :
  bouger une côte ? Recalcul. Ajouter une ligne ? Recalcul. etc… Et ça,
  même si toutes les autres opérations sont désactivées.
- il n’est pas possible de piloter le logiciel en ligne de commande
  (*CLI*) : générer des variantes de pièce entraine une modification
  manuelle des paramètres (ou une sélection de variante), suivi d’un
  export manuel, et c’est pénible.
- j’ai rencontré pas mal de crashes, surtout en appliquant des
  contraintes sur des assemblages

Du coup, j’ai voulu passer à de la création de modèle basée sur du code.
Pour plusieurs raisons :

- Le code, c’est versionnable et ça ne prend pas de place
- Le code, c’est révisable (il existe des outils de comparaison de
  modèles 3D, qui coûtent certainement une blinde parce que c’est sur
  devis)
- Le code, c’est logiquement manipulable de l’extérieur : prendre un
  bout par-ci, composer avec ce machin-là
- Je m’attends, peut-être à tort, à une stabilité supérieure à celle
  d’un outil graphique où on clique partout pour dessiner sur ce que
  l’on voit (sans basher, c’est compliqué de faire un outil efficace,
  stable, simple *avec une UI*)

Donc : **OpenSCAD** !

OpenSCAD
--------

`OpenSCAD <https://openscad.org/>`__ est un outil de création de modèle
3D où on tape du code, utilisant la
`CSG <https://fr.wikipedia.org/wiki/G%C3%A9om%C3%A9trie_de_construction_de_solides>`__
: Géométrie de construction de solides.

L’idée de base, c’est d’appliquer des opérations simples sur des formes
simples pour en faire des modèles complexes.

Je suis une quiche en maths, donc je n’ai pas creusé sur un usage
avancé.

**Les pour :**

- la syntaxe est simple et compréhensible (OpenSCAD a son propre
  langage)
- l’éditeur de code est [STRIKEOUT:pourri] simple, mais OpenSCAD
  supporte le rechargement automatique : du coup, j’édite avec un autre
  éditeur qui me donne de l’auto-complétion, tout en gardant l’aperçu du
  résultat dans la fenêtre d’OpenSCAD
- l’apprentissage des commandes de base est facile : il y en a peu
- via la CLI, on peut exporter des modèles et des aperçus en png
- il est possible d’organiser son code en modules, c’est cool :)
- la communauté a créé `plein de
  librairies <https://openscad.org/libraries.html>`__ pour aider à la
  construction (ex : `BOSL2 <https://github.com/BelfrySCAD/BOSL2/>`__)
- c’est facile de débugger visuellement son code : un ``#`` devant une
  ligne et la forme associée apparait en rouge dans la prévisualisation
- FreeCAD est compatible : ouvrez un fichier OpenSCAD avec et il
  reconstruira au mieux le modèle

**Les contre :**

- on ne manipule que des formes primitives (cubes, sphères, cylindres,
  etc.). À moins d’utiliser des librairies, le moindre chanfrein demande
  un peu de réflexion et quelques lignes de code.
- pas de `B-Rep <https://fr.wikipedia.org/wiki/B-Rep>`__ pour l’export
  (donc, pas de STEP), uniquement des maillages (stl, obj, amf…)
- il n’est pas possible d’assigner des résultats à des variables (ex :
  générer une sphère et s’en re-servir). Donc au bout d’un moment, c’est
  lent
- le rendu peut être extrêmement lent sur des pièces qui ont un peu de
  manipulations.
- il n’y a pas de système de gestion de dépendence, donc suivant le
  moment où vous avez récupéré une librairie, vous n’aurez pas les mêmes
  résultats que le collègue qui a une autre version. À moins de la
  versionner (en entier, ou d’utiliser des *submodules* Git). Une
  tentative a été faite d’utiliser le service de RubyGems pour ça, mais
  même si sur le principe ça fonctionne, ça reste bancale (et pollue
  RubyGems avec des packages openscad)

Un bout de code OpenSCAD :

.. code:: openscad

   union(){
     translation = box_wall_thickness + assembly_play;
     // Base
     translate([translation , translation , 0])
       roundedCube(size=[slot_width, slot_width, slot_height], r=slot_radius, sidesonly=true);
     translate([0, 0, slot_height - box_wall_thickness])
       chamferedRoundedBox(
         x = box_width,
         y = box_width,
         z = box_wall_thickness,
         r = box_radius
       );
   }

Bon moi, je veux du Step :)

Donc: **CadQuery** !

CadQuery
--------

`CadQuery <https://cadquery.readthedocs.io/en/latest/>`__ (`dépôt
Git <https://github.com/CadQuery/cadquery>`__, c’est du Python. Donc
bah, on peut s’imaginer la facilité de gestion de dépendances, la
modularité, le partage de librairies, etc…

Par contre, c’est juste une librairie ; il faut un éditeur pour afficher
les aperçus : `cq-editor <https://github.com/CadQuery/CQ-editor>`__ ou
un `plugin pour
VSCode <https://marketplace.visualstudio.com/items?itemName=bernhard-42.ocp-cad-viewer>`__
(si vous utilisez VSCodium comme tout être humain sensé, c’est plus
pénible : vous allez devoir utiliser le `dépôt
Git <https://github.com/bernhard-42/vscode-ocp-cad-viewer>`__, et vous
débrouiller pour les dépendences. Mais c’est faisable)

Le moteur de rendu, c’est OpenCascade, comme pour FreeCAD, donc on parle
maintenant de `B-Rep <https://fr.wikipedia.org/wiki/B-Rep>`__, à la
différence d’OpenSCAD

Tous les exemples sont assortis d’une visualisation 3D, c’est top !

Coté syntaxe, le principe, c’est de chaîner ses méthodes, et pour le
coup, je ne trouve pas ça très naturel, donc j’ai arrêté très
rapidement.

Petits bouts de code quand même :

.. code:: py

   thickness = 0.5
   width = 2.0
   # Une plaque verticale de 2x2x0.5mm, avec un trou de 0.5mm centré
   result = Workplane("front").box(width, width, thickness).faces(">Z").hole(thickness)

.. code:: py

   # Un truc étrange, dans les exemples
   result = (
       cq.Workplane(origin=(20, 0, 0))
       .circle(2)
       .revolve(180, (-20, 0, 0), (-20, -1, 0))
       .center(-20, 0)
       .workplane()
       .rect(20, 4)
       .extrude("next")
   )

Mais **Build123d** alors !

Build123d
---------

`Build123d <https://build123d.readthedocs.io/>`__ (`dépôt
Git <https://github.com/gumyr/build123d>`__), c’est toujours dessiner en
3D, en python, mais avec deux approches : un mode *builder*, similaire à
OpenSCAD, et un mode *algebra*, plus proche de la programmation
procédurale.

Le moteur de rendu, c’est aussi OpenCascade, comme pour CadQuery et
FreeCAD, donc on fait aussi du B-Rep.

Pour le moment, je suis dans le process de terminer le modèle
“Gridfinity”, donc je n’ai pas encore fait de génération en CLI, mais à
priori, c’est possible.

**Les pour :**

- la doc est bien faite, assortie `d’exemples
  3D <https://build123d.readthedocs.io/en/latest/introductory_examples.html>`__,
  de rendus et de tutos
- vu qu’on code pour faire du B-Rep, on peut exporter (entre autres) du
  STEP \o/
- on peut faire des screenshots de qualité (leur doc en contient plein)
- je trouve la syntaxe sympa, et suivant le besoin, bosser avec un mode
  ou l’autre, c’est chouette
- le débug se fait plutôt facilement (pas aussi aisé qu’avec OpenSCAD,
  celà dit)
- on peut assigner des résultats à des variables pour éviter des
  re-calculs
- pour les préviews, il y a `un fork de
  cq-editor <https://github.com/jdegenstein/jmwright-CQ-Editor>`__ qui
  prend en charge les modèles Build123d en plus des modèles CadQuery
  (j’utilise, avec un éditeur à côté, comme pour OpenSCAD). Le “bundle”
  sur github inclut quelques librairies supplémentaires. Sinon, le
  `plugin
  VSCode <https://marketplace.visualstudio.com/items?itemName=bernhard-42.ocp-cad-viewer>`__
  pour CadQuery supporte aussi Build123d
- on peut écrire des tests (je ne me suis pas penché là-dessus, mais
  bon, un gros point en plus)
- Il y a des sélecteurs pour à peu près tout (vertices, arêtes, faces)
  et des méthodes pour réaliser des opérations dessus (yay ! des
  chanfreins *faciles* !)
- on peut partir avec des primitives et les manipuler, comme dans
  OpenSCAD
- on peut dessiner soi-même des lignes en spécifiant leurs points, puis
  appliquer des opérations dessus
- on peut importer des formats 2D et bosser dessus (j’ai vu passer des
  exemples avec du SVG)
- il est possible de créer des modèles avec CadQuery et les continuer
  avec build123D
- …

**Les contre :**

- le temps d’apprentissage est plus long qu’avec OpenSCAD, je jongle
  encore avec la doc et mon code
- j’ai pu noter des différences de comportement pour la même méthode,
  suivant qu’on soit en mode *builder* ou *algebra*
- comprendre pourquoi une opération n’est pas possible n’est pas
  toujours simple

Rien n’est parfait. Il y a certainement d’autres soucis ou points de
friction, mais pour le moment, *ça va* dans l’ensemble

Une plaque avec un trou, en mode *builder* :

.. code:: py

   length, width, thickness = 80.0, 60.0, 10.0
   center_hole_dia = 22.0

   with BuildPart() as ex2:
       Box(length, width, thickness)
       Cylinder(radius=center_hole_dia / 2, height=thickness, mode=Mode.SUBTRACT)

La même en mode *algebra* :

.. code:: py

   length, width, thickness = 80.0, 60.0, 10.0
   center_hole_dia = 22.0

   ex2 = Box(length, width, thickness)
   ex2 -= Cylinder(center_hole_dia / 2, height=thickness)

Autres
------

Il existe d’autres outils pour faire de la 3D paramétrique, j’ai pu
essayer un peu un plugin pour Blender : `CAD
Sketcher <https://www.cadsketcher.com/>`__. C’est prometteur si vous
êtes à l’aise avec Blender, et ce n’est pas mon cas.

`AstoCAD <https://www.astocad.com>`__ est un fork de FreeCAD, payant,
qui reverse ses correctifs et améliorations au projet après un certain
temps. C’est un abonnement à l’année, je n’ai donc pas essayé, trouvant
le prix trop élevé *juste pour tester*.

Je suis tombé sur `PartCAD <https://partcad.org/>`__
(`docs <https://partcad.readthedocs.io/>`__ et `dépôt
Git <https://github.com/partcad/partcad/>`__), un “standard de
documentation de produits manufacturables”, ce sera ma prochaine étape.

`Manyfold <https://manyfold.app>`__ est un service opensource en Ruby
(on Rails) de gestion et partage de modèles 3D. Une partie fédération
est en cours de développement avec ActivityPub.

Il y a aussi `SolveSpace <https://solvespace.com>`__ pour dessiner des
modèles paramétriques, qui m’a été remonté pendant l’écriture de
l’article.

Pour visualiser les fichiers 3D, j’utilise
`Mayo <https://github.com/fougue/mayo>`__ principalement, et
`MeshLab <https://www.meshlab.net/>`__ me permet de corriger des modèles
récupérés sur internet.

Et du coup ?
------------

Mon point de vue sur ces outils n’engage que moi, je pense qu’il faut
tester pour adopter.

J’utilise encore beaucoup FreeCAD, c’est un outil vraiment bien. Je m’en
sers principalement pour des modèles qui ne bougeront pas trop, ou pour
des modèles pour lesquelles dessiner des *esquisses* est encore
indispensable pour moi (gérer des splines de tête, c’est pas encore ça).

OpenSCAD, c’est top pour des petites pièces simples : en quelques lignes
on a un résultat.

Build123d, j’ai l’impression que c’est l’outil qui remplacera OpenSCAD
quand je serais à l’aise avec. L’export en STEP est vraiment un plus.

Résultats de l’exercice
-----------------------

FreeCAD
~~~~~~~

La feuille de calcul pour les paramètres :

.. image:: /images/retour_experience_cao_opensource/freecad_settings.png
        :align: center
	:alt: Feuille de calcul de FreeCAD

Prévisualisation FreeCAD avec les deux modèles :

.. image:: /images/retour_experience_cao_opensource/freecad_settings.png
        :align: center
	:alt: Modèle FreeCAD

.. _openscad-1:

OpenSCAD
~~~~~~~~

Grille 3x2 :

.. image:: /images/retour_experience_cao_opensource/openscad_grid.png
        :align: center
	:alt: Grille 3x2 réalisée avec OpenSCAD

Boite 2x2 :

.. image:: /images/retour_experience_cao_opensource/openscad_box.png
        :align: center
	:alt: Boite 2x2 réalisée avec OpenSCAD

.. _build123d-1:

Build123d
~~~~~~~~~

.. image:: /images/retour_experience_cao_opensource/build123d.png
        :align: center
	:alt: WIP avec Build123d
