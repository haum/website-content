==========
HAUMelitta
==========

:slug: haumelitta


Qu'est ce que c'est?
====================

`HAUMelitta`_ (a.k.a la cafetière qui tweete) est un peu un emblème du HAUM. C'est bêtement une cafetière reliée à 
twitter via un raspberry pi, mais elle fait son effet :).

.. _HAUMelitta: https://twitter.com/HAUMelitta

Principe
========

La cafetière surveille le compte twitter associé et se met en marche ou s'arrête une fois les mots clés détectés.

Mise en Oeuvre
==============

Matériel
--------

La cafetière a été afublée d'un capteur de température au dessus de la cuve d'eau pour détecter quand le café est pret 
(quand la temperature de l'eau est suffisament haute).

En externe (pour eviter les problèmes liés à l'eau que peut contenir une cafetière, et pour pouvoir utiliser la cafetière 
sans le système), la Raspberry Pi 1 contient le code (en python3) et est reliée à une multiprise modifiée avec un relai 
pour activer ou non son déclenchement.

Logiciel
--------

Le logiciel utilisé pour Haumelitta est disponible sur notre dépôt git.

Installation
============

L'installation consiste juste à brancher la multiprise sur le réseau électrique, à mettre en place la Raspberry Pi 1 pour qu'elle 
soit connectée à Internet (et ait accès à Twitter), et à brancher la cafetière sur la multiprise à relai.
