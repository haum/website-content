==========================================
Insoler des cyanotypes à l'imprimante mSLA
==========================================

:date: 2026-01-22 19:25
:tags: hack
:category: hack
:slug: cyanotype_msla
:authors: JackDesBwa
:summary: Hacker une imprimante mSLA pour insoler des cyanotypes


Cyanotype
---------

Connaissez-vous le cyanotype ? Il s'agit d'une méthode photographique facile
d'accès, à la chimie simple à manipuler sans danger et surtout au rendu très
caractéristique avec ses tons bleutés.

La solution chimique, préalablement enduite sur un support et séchée à l'abri de
la lumière, est exposée aux ultraviolets, puis lavée à l'eau claire. Les parties
insolées forment un bleu de Prusse stable qui teinte le support tandis que le
reste de la partie photosensible n'ayant pas reçu les UV est évacuée au rinçage.
L'image apparaît donc en négatif, avec les parties exposées plus foncées.

Usuellement, cette technique est utilisée pour faire des herbiers en exposant un
papier sensibilisé à travers les végétaux dont l'ombre s'imprime sur la feuille.
Ou en imprimant au préalable un négatif qui sera développé par contact, au
soleil ou sous une lampe à UVs. Mais comment pourraient faire des hackers ?


Le détournement
---------------

Imprimer un négatif, voire plusieurs empilés pour obtenir suffisamment
d'opacité, il faut bien admettre que c'est peu pratique et même un gâchis de
ressources si l'on ne tire pas des séries de la même image. À ce compte-là,
autant sortir l'image directement avec l'imprimante.

Là entre en jeu l'imprimante 3D mSLA, autrement appelée imprimante à résine,
car elle insole une résine photosensible qui durcit au contact des UVs. Et c'est
dans ce dernier mot que la liaison se fait : la machine dispose d'une source UV,
d'un système optique pour avoir un éclairement uniforme aux rayons parallèles,
d'un écran à haute définition pour masquer sélectivement les parties à protéger
des UVs, bref un peu tout ce qu'on aimerait utiliser pour insoler nos cyanotypes !

Malheureusement, les UVs générés par la machine ne sont pas optimaux pour la
chimie du cyanotype. Cependant en pratique, allonger le temps d'exposition
contrecarre la réaction plus lente avec ces UVs ci. Pour donner un ordre d'idée,
avec mon papier dont la solution a été enduite plusieurs mois avant ce test et
gardé au noir depuis, les temps choisis allaient de 4 minutes pour les valeurs
claires à 51 minutes pour les valeurs foncées.

La réelle difficulté est de trouver la méthode pour produire le bon fichier à
faire manger à la machine.

.. container:: aligncenter

        *Une grille d'étalonnage permet d'évaluer les temps nécessaires.*

        .. image :: /images/cyanotype_msla/grid.jpg 


UVtools
-------

Nous pourrions réaliser un modèle 3D spécialement créé pour qu'une fois découpé
en tranches par les logiciels habituels pour l'impression 3D, le rendu soit
celui voulu. Mais ce serait un maillage incroyablement dense et avec
potentiellement de la perte de résolution lors des conversions, voire une perte
volontaire en particulier pour ne pas faire tomber à genoux les processeurs et
la RAM lors des opérations. Mais soyons plus astucieux.

Dans mon cheminement pour ce projet, j'avais choisi une imprimante de chez
ELEGOO car elle acceptait un format de fichier documenté publiquement, et
j'avais même commencé à coder dans le but de produire un fichier spécialisé pour
cette tâche. Finalement, j'ai découvert l'outil `UVtools`_ qui permet de faire
beaucoup de choses en plus de ce que nous cherchons à faire ici et sur quasiment
toutes les imprimantes du marché.

Il s'agit d'un couteau suisse pour l'examen et la manipulation des fichiers
d'impression 3D mSLA. Il ne les crée pas lui-même depuis zéro, mais peut
analyser, changer de format, éditer les couches, etc. Dans notre cas, il servira
à remplacer les tranches d'un fichier créé par un autre logiciel par les
tranches de notre choix.


Préparation du fichier
----------------------

La première étape est de créer un fichier pour notre imprimante à l'aide d'un
logiciel de découpe traditionnel d'impression résine. Un simple cube fera
l'affaire puisqu'au final ses couches seront effacées. Nous pouvons aussi
récupérer un des fichiers exemple de la machine. À vrai dire, c'est tout un tas
de paramètres indépendants du modèle comme les dimensions de la machine qui
seront réellement utiles à UVtools.

Maintenant, importons le fichier généré dans UVtools. Après le temps de
chargement et surtout de décodage, nous pouvons aller dans le menu
`Actions > Remove layers` au-dessus du canevas, puis remplir le formulaire pour
effacer toutes les couches.

La création des couches appropriées pour l'insolation du cyanotype est facilitée
par un outil intégré `Tools > Lithophane`. Évidemment nous ne voulons pas créer
une `lithophanie`_ à proprement parler puisque nous n'utiliserons pas de résine,
mais les couches pour les produire s'avèrent avantageusement exactement les
mêmes que celles voulues ici.

Nous voulons en particulier cocher les options `Separate gayscale pixels` pour
avoir un masquage binaire jouant sur le temps d'exposition et non sur la
transparence du masquage présentant un contrôle plus incertain de la quantité
d'UVs délivrés et n'étant pas compatible avec toutes les machines, et
`One layer per threshold level` pour avoir autant de couches que nécessaire et
non comprimer la dynamique sur un nombre restreint de couches comme l'impose la
physique à une lithophanie.

Petite subtilité : si l'imprimante a des pixels non carrés, il faut appliquer 
une anamorphose au préalable à l'image qui sera donnée à l'outil car UVtools ne
gère pas cela automatiquement. Dans mon cas, les pixels étant de 19µm de large
pour 24µm de haut, j'ai étiré la largeur de l'image par un facteur 24/19.

L'inversion des couleurs (négatif) peut se faire dans l'image ou par une option
à cocher.

.. container:: aligncenter

        *Interface de UVtools pour générer des lithodphanies*

        .. image :: /images/cyanotype_msla/uvtools.webp


Insolation
----------

Plaçons le papier sensibilisé sur l'écran de l'appareil, bien à plat, et lançons
l'impression. L'imprimante se calibre, monte et descend le plateau (retiré) puis
se plaint de ne pas avoir détecté de résine. Heureusement ce modèle
d'imprimante permet de forcer la poursuite avec une boîte de dialogue sur
l'écran de contrôle. Un deuxième échec du nivellement automatique du plateau
apporte une alerte qu'il est également possible d'ignorer et ça y est,
l'insolation a lieu.

Voici en accéléré le motif qui est affiché sur l'écran, avec en blanc les zones
où les UVs vont atteindre le papier. Remarquez comme chaque pixel stoppe
l'insolation à des temps différents selon la valeur cible de l'image.

.. container:: aligncenter

  *Motif exposé (vidéo).
  Il s'agit d'une photographie du cloître de l'abbaye de Fontevraud en 2018.*

  .. raw:: html

    <video controls preload="none" width="800" height="480">
      <source src="/images/cyanotype_msla/insolation.mp4" type="video/mp4">
    </video>

Résultat
--------

Et voilà ce que ça donne :

.. container:: aligncenter

        .. image :: /images/cyanotype_msla/cyanotype.jpg

En bonus, une vue en détail de très très près, au niveau du toit de l'abbatiale
visible à travers la première arche dans sa partie droite. La résolution est
fortement limitée par les fibres du papier :

.. container:: aligncenter

        .. image :: /images/cyanotype_msla/detail.jpg


Et voilà, nous avons réussi à tirer un cyanotype à partir d'une photographie
numérique, sans passer par un négatif sur film transparent.


.. _UVtools: https://github.com/sn4k3/UVtools
.. _lithophanie: https://fr.wikipedia.org/wiki/Lithophanie
