=====================
A propos de LightStep
=====================

:date: 2015-12-13 23:00
:tags: lightstep
:category: projets
:slug: about-lightstep
:authors: HAUM
:summary: Avancée du projet et Idées

Alors que le projet avance petit à petit, les idées autour de LightStep fleurissent.
Après une refonte du code du projet, certaines nouvelles possibilités s'offrent ainsi à nous.

Les idées du tableau
====================

Dans une première `séance de réflexion`_, plusieurs idées concernant les animations et la manière de les déclencher
ont été émises. Voici donc une transcription du tableau :

Animations
----------

- arbre de Noël stylisé
- *dimmer*
- K2000
- remplissage
- cercle chromatique
- fusion de 2 couleurs
- arc-en-ciel
- scintillement

Interactions
------------

- plus de marches appuyées ⇒ plus de luminosité
- plus de marches appuyées ⇒ changement plus rapide
- une marche ⇒ un effet lumineux
- combinaisons de marches :

        - combinaisons d'effets
        - changement de mode

- influence du temps d'appui
- changement de mode automatique toutes les n minutes
- que ce passe-t-il quand rien n'est appuyé ?

        - effet
        - rien
        - témoin (*heartbeat*, respiration)

L'idée du jour
==============

La nouvelle idée se base sur le découplage entre couleur et animation.


Couleur
-------


.. image:: /images/lightstep/hue_shift.png
        :align: right

La couleur est choisie en combinant l'appui sur certaines marches avec un curseur qui tourne sur la roue de la teinte
(voir image). Ainsi la couleur tournante avance avec le temps et une série de marches permet de sélectionner une couleur
de base autour de cette couleur tournante.

L'appui sur une marche spéciale (par exemple derrière la caisse) provoque l'avance rapide de la couleur de base.

Animations
----------

L'appui sur les autres marches déclenche des animations qui reçoivent en entrée la couleur de base et qui tournent en
boucle jusqu'au relâchement de la touche. Ces animations doivent boucler en un temps court et ne peuvent pas être
coupées en cours de boucle.

L'appui sur certaines combinaisons de touches entraine le déclenchement d'animations « spéciales » qui elles sont plus
longues.


.. _séance de réflexion: /seance_20151206.html
