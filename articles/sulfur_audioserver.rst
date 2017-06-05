================================
Sulfur comme carte son en réseau
================================

:date: 2017-06-05 11:06
:tags: hack
:category: hack
:slug: sulfur_audioserver
:authors: JackDesBwa
:summary: Transformer sulfur en serveur audio

Sulfur est une carte raspberry-pi qui nous sert vaillamment de serveur de musique
depuis de nombreuses années au hackerspace. Aujourd'hui, ajoutons lui une
fonction supplémentaire : un serveur pour envoyer le son de son ordinateur
directement sur les enceintes du local.

Installation de pulseaudio
==========================

Pulseaudio est un logiciel de gestion du son répandu sous Linux. Il réalise une
surcouche au dessus de la plateforme ALSA qui gère en particulier la couche
matérielle. Pour ce qui nous intéresse, pulseaudio ajoutera la possibilité
d'envoyer du flux à travers le réseau et pour faciliter l'utilisation, nous
mettrons en place une diffusion zeroconf.

Sur sulfur, installons pulseaudio et avahi :
*sudo apt-get install pulseaudio pulseaudio-module-zeroconf avahi-daemon*
Puis dans */etc/default/pulseaudio*, nous passons la configuration
*PULSEAUDIO_SYSTEM_START* à 1. Enfin, dans */etc/pulse/system.pa* nous
ajoutons :

::

  ### Network server
  load-module module-native-protocol-tcp auth-ip-acl=127.0.0.1;192.168.0.0/16 auth-anonymous=1
  load-module module-zeroconf-publish

Maintenant, redémarrons sulfur et... il publie bien un serveur audio !

::

  $ avahi-browse -alr | grep "PulseAudio Sound Server"
  +  wlan0 IPv4 pulse@sulfur                                  PulseAudio Sound Server local
  =  wlan0 IPv4 pulse@sulfur                                  PulseAudio Sound Server local

À faire : Éviter de démarrer pulseaudio en mode système

Utilisation
===========

Sur le PC, si les modules TCP et zeroconf ne sont pas chargés, il est possible
de les charger à chaud dans PulseAudio :

::

  pactl load-module module-native-protocol-tcp
  pactl load-module module-zeroconf-discover

Maintenant, sulfur apparaît dans *pavucontrol* ou autre gestionnaire de son
compatible avec pulseaudio. Il suffit de choisir cette sortie et le son du PC
est joué dans le local !

Latences réseau
===============

Au HAUM, on se connecte la plupart du temps en WiFi, par conséquent la latence
varie beaucoup, ce qui n'est pas compatible avec du streaming audio. Pour
s'affranchir des effets audio désagréables, nous allons augmenter la taille des
tampons audio, c'est à dire la quatité que le système de son charge avant le
jouer (ainsi, il y toujours des données d'avance à envoyer à la carte son)

Dans le fichier */etc/pulse/daemon.conf* modifions quelques réglages :

::

  high-priority = yes
  default-fragments = 8
  default-fragment-size-msec = 50

À tester sur le long terme...
