=====================
À l'assaut des moirés
=====================

:date: 2017-09-15 22:42
:tags: projet_moire
:category: projets
:slug: premiers_moires
:authors: JackDesBwa


Depuis quelques semaines désormais, me voilà cherchant à percer les mystères
des `moirés`_, ces figures étranges qui naissent magiquement de la
superposition de motifs répétitifs. Après de nombreuses lectures, je constatai
ne pas y comprendre grand-chose et décidai donc de passer dare-dare à la
pratique en m'accrochant aux quelques bribes glanées ci et là.

D'après l'adage Shadoks, c'est « en essayant continuellement que l'on finit par
réussir » et les efforts fournis finirent par voir pointer de premiers
résultats à la fois inattendus et totalement étonnants ; ce qui ne manqua pas
de titiller la curiosité d'autres membres dont les idées n'ont pas tardé à
augmenter l'ampleur du projet.

Première réussite
-----------------

La première réussite vint de la formule suivante :

.. container:: aligncenter

   .. image:: /images/moire/formule1.png
      :alt: I(x, y) = cos^2 \left ( {2 \pi \over 10} \left [ {{ min\{(x-100)^2+(y-100)^2, 8100\} \over 800} \pm (x+y-200) }) \right ] \right )

Cette formule donne le pourcentage d'intensité de chaque pixel de coordonnée
(x,y) d'une image de 200 pixels de côté. Le symbole ± est là pour rappeler que
l'on emploiera la somme sur une image et la différence sur la seconde image.

Imbuvable ? Peut-être.

Il aura fallu tâtonner beaucoup avant de trouver ce résultat alambiqué. On y
reconnait ce qui ressemble (vaguement) à l'équation d'un cercle centré en
(100, 100), la trace d'une sorte de motif diagonal ainsi qu'une bonne grosse
fonction trigonométrique pour bien rigoler. Ça ressemble à du bricolage, et en
effet c'en est ; mais c'est surtout le premier résultat concret.

Ainsi, je m'attendais à voir des cercles concentriques légèrement déformés qui
se seraient vus rayés par une figure de moiré en superposant les deux images.
Que nenni, c'est l'inverse qui est apparu !

.. container:: aligncenter

   .. image:: /images/moire/figure1.png
      :alt: Deux grilles et leur supperposition formant le moiré

Note 1 : Sur la figure ci-dessus s'ajoute un effet de seuil qui a été introduit
en vectorisant l'image à base de cosinus.

Note 2 : Il se peut qu'une légère figure circulaire apparaisse sur le dessin des
grilles, car celui-ci peut entrer en interférence avec la matrice d'affichage de
votre écran.

Prototype
---------

Amusés par le résultat, certains membres proposèrent la drôle d'idée de découper
la grille dans une plaque de MDF. La forme étant déjà vectorisée, la
transformation en un fichier adapté à la découpeuse laser a été rapide et le
résultat tout à fait convainquant.

Nous venions de réaliser deux grilles légèrement ondulées - objets concrets que
nous pouvions manipuler avec nos mains - dont la superposition adéquate révèle un
motif en cercles concentriques latent ; deux morceaux de matière dont la
géométrie interfère dans le monde physique.

Observation directe, lightbox, lampe torche... nous avons vite commencé à jouer
avec notre nouvelle trouvaille à essayer de nouvelles manières de constater le
motif émergeant ou simplement à jouer avec les grilles pour voir ce qui pouvait
en ressortir. C'est une activité plaisante en elle-même, et à vrai dire, nous
aurions pu rester des heures à jouer avec ces deux simples grilles...
d'ailleurs, n'est-ce pas ce que nous avons fait ‽

.. container:: aligncenter

	.. image :: https://photos.haum.org/small/moire/p1070093_37075915742_o.jpg

Deux nouveaux motifs
--------------------

Je vous épargne les équations (bien plus complexes que la précédente) qui
ont permis de réaliser ces grilles-ci, car il n'est point nécessaire de
comprendre pour s'émerveiller devant les résultats. Admirez.

Note 1 : Votre navigateur doit supporter le format SVG et les animations pour
profiter pleinement de ces cas.

Note 2 : Vous pouvez télécharger le fichier SVG et l'ouvrir (par exemple avec
le logiciel libre Inkscape_) pour jouer avec les motifs, les superposer, voire
même les imprimer et ainsi constater sans ambiguïté qu'il n'y a aucun trucage.


.. container:: aligncenter

   .. raw:: html

      <object data="/images/moire/spirale.svg" type="image/svg+xml"></object>
      <object data="/images/moire/diode.svg" type="image/svg+xml"></object>

   Téléchargement: 1_, 2_

	.. image :: https://photos.haum.org/small/moire/p1070361_37075912802_o.jpg
	.. image :: https://photos.haum.org/small/moire/p1070358_36433433613_o.jpg


N'hésitez pas à consulter nos albums photo sur Flickr pour trouver d'autres
moirés que nous ferons certainement prochainement.

.. _`moirés`: https://fr.wikipedia.org/wiki/Moir%C3%A9_(physique)
.. _Inkscape: https://inkscape.org/fr/
.. _1: /images/moire/spirale.svg
.. _2: /images/moire/diode.svg
