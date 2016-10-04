===========
PianoStairs
===========

:slug: pianostairs

:projet_realisation: terminé-brightgreen
:projet_etat: démonté-yellow

Vous gravissez des escaliers et aujourd'hui ils font de la **musique**... Posée sur les
marches, une installation à la sauce HAUM transforme la cage d'escalier en un instrument
géant !

Composition
===========

Créé dans le cadre des **Siestes Teriaki 2014**, le PianoStairs est composé d'une
vingtaine de (sur)marches installées dans un escalier. Elles sont reliées à une carte
**Arduino Leonardo** qui peut dialoguer avec n'importe quel appareil MIDI. Dans notre cas,
le jeu des sons est géré par une **RaspberryPi** embarquant FluidSynth_ comme synthétiseur logiciel.
Un amplificateur et des enceintes complètent le système. Toute l'électronique est contenue dans une boîte discrète.

Reloaded
========

À l'occasion de l'emménagement dans nos nouveaux locaux (début 2016), nous avons voulu faire renaître le PianoStairs.
Mais en l'absence de documentation sur le projet, une équipe a recodé toute la partie logicielle.

Les nouvelles sources pour le code sont stockées `sur github`_.

Reproduire ?
============

Le projet peut être reproduit en suivant les étapes suivantes.

Fabrication des marches
-----------------------

Le concept global des marches est d'être un simple interrupteur qui résiste au poids des personnes.
Dans notre cas, les marches sont conçues grâce à une lame de parquet flottant, une feuille de matériau isolant (mousse) pour surélever, et des feuilles d'aluminium (scotch) pour faire les contacts.

Deux fils et des jumpers mâles permettent la connexion à la carte Arduino (via la nappe).

Mise en place de l'électronique
-------------------------------

L'électronique se base sur une alimentation ATX, une carte Arduino Leonardo et une nappe pour connecter les marches à la carte.

Les marches sont reliées à une des broches de l'Arduino d'un côté et d'un autre à la masse. Le contact est détecté lors du passage d'une broche (avec *pull up*) à la masse.
La connexion de chacune des marches à la masse se fait directement en modifiant la nappe IDE qui sert à la connexion.

L'alimentation ATX sert à redistribuer le 5V pour la RPi et l'Arduino.

La carte doit ensuite être flashée avec le firmware_ disponible sur le dépôt, il nécessite l'installation de la bibliothèque MidiUSB_.

Mise en place du synthétiseur logiciel
--------------------------------------

La RaspberryPi doit être préparée avec une Raspbian_ puis paramètrée en utilisant les lignes de commande suivantes ::

    $ sudo apt install git alsa-utils fluidsynth fluid-soundfont-gm
    $ git clone git@github.com:haum/PianoStairs.git
    $ cd PianoStairs/rpimidisynth
    $ make install
    $ sudo reboot

Après redémarrage, la Raspberry émettra un léger son puis attendra des trames MIDI pour les synthétiser.


.. _FluidSynth: http://fluidsynth.elementsofsound.org/
.. _sur github: https://github.com/haum/PianoStairs
.. _MidiUSB: https://www.arduino.cc/en/Reference/MIDIUSB
.. _firmware: https://github.com/haum/PianoStairs/blob/master/midistairs/midistairs.ino
.. _Raspbian: https://www.raspbian.org/
