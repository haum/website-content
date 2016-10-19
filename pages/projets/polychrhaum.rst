===========
PolychrHAUM
===========

:slug: polychrhaum

:projet_realisation: terminé-brightgreen
:projet_etat: fonctionnel-brightgreen

Qu'est ce que c'est?
====================

PolychrHAUM est à la fois le nom d'un appareil conçu au sein de l'association et de la bibliothèque
logicielle qui permet d'interagir avec celui-ci facilement.

L'appareil a pour unique but d'être hacké. Il s'agit d'un boîtier qui dispose de 150 LEDs multicolores
et deux boutons pour les utilisateurs. Même si la plateforme est simple et volontairement minimaliste,
il y a matière à imaginer des projets amusants.

Le premier projet réalisé sur cette plateforme est le 1DPong_, un jeu de raquette en une dimension.
A suivi HAUMTinsel_, une guirlande de fêtes connectée pilotable via Internet.

Le code
=======

Nous avons créé deux dépôts git pour héberger d'une part la `bibliothèque`_ et d'autre part les exemples_.
Cela permet en particulier de facilement importer la bibliothèque Arduino sans s'embarrasser des exemples
eux-mêmes.

Utilisation
===========

L'utilisation sera décrite à travers les exemples.

01_skeleton
-----------

L'exemple 1 est un squelette qui ne fait rien, sinon initialiser le programme.

``PolychrHAUM <150, PIN__LEDSTRIP_DATA> khroma;`` est la déclaration qui instancie un objet qui gèrera
l'appareil. Les broches sur lesquelles sont branchés les composants de l'appareil sont énumérées puis
associées à cet objet dans la fonction ``setup``. Dans cette fonction, nous déclarons aussi la fonction
à appeler lorsqu'un pas d'animation est requis et lançons l'initialisation de la bibliothèque.

Dans la fonction ``loop`` il est fait appel à ``khroma.loop_step()`` car cette fonction doit être
appelée le plus souvent possible.

Enfin nous voyons qu'il existe une fonction ``animate`` qui sera appelée par la bibliothèque à chaque
pas d'animation pour aisément cadencer les animations.

02_hellored
-----------

Cet exemple montre comment modifier la couleur des LEDs. Il reprend le squelette et modifie sa fonction
``animate``.

La modification de la couleur s'effectue par l'appel de la fonction ``khroma.leds.set_rgb`` qui prend en premier paramètre la position, puis la proportion de couleur RVB (Rouge, Vert, Bleu). La position est
comptée en nombre de LEDs depuis le milieu, tandis que les composantes de couleur s'expriment de 0 à 255, inclus.

Pour allumer toute la bande en rouge, il faut donc allumer chaque LED en rouge en faisant appel à la
fonction plusieurs fois. C'est pourquoi une boucle est utilisée pour balayer les positions allant de
``-hsize`` à ``+hsize`` puisque c'est le système de coordonnées utilisé.

03_bluetogreen
--------------

Cet exemple est identique au précédent dans ses fondements. Cette fois, la couleur n'est pas rouge, mais
un mélange de bleu et de vert via de la position de chaque LED. Cela crée un dégradé du bleu au
vert en passant par le cyan.

04_simple_animation
-------------------

Ajoutons un peu d'animation !

Dans cet exemple, la position des LED allumées change en fonction du temps. Pour cela, on utilise un
objet ``LinearAnimator`` de la bibliothèque qui simplifie énormément la gestion des animations malgré
sa propre simplicité d'implémentation.

Un ``LinearAnimator`` réalise une transition de 0 à 1, de 1 à 0, ou en boucle selon les options passées.
Dans notre cas, il est initialisé dans la fonction ``setup`` avec une durée de 3000ms (i.e. 3s) et un fonctionnement en boucle. 
Nous le démarrons aussi dès l'initialisation.

Dans la fonction ``animate`` nous commençons par appeler ``animator.animate();`` pour que l'animateur
effectue ses calculs. Nous pourrons ensuite utiliser la variable ``animatior`` dans les calculs eux-mêmes
sans se préoccuper de l'animation: la valeur changeant elle-même au cours du temps, les résultats
des calculs dépendants de l'animateur changeront au cours du temps eux-aussi.

Ici, nous multiplions sa valeur par la demie longueur du bandeau de LEDs (plus 1) pour déterminer une
position et allumons une LED en violet de chaque côté avec cette position. Les LEDs se baladent donc
vers le centre du bandeau en 3 secondes (si le potentiomètre de vitesse est en position "vitesse normale")

.. _1DPong: /pages/1dpong.html
.. _HAUMTinsel: /pages/haumtinsel.html
.. _bibliothèque: https://github.com/haum/polychrhaum
.. _exemples: https://github.com/haum/polychrhaum-examples
