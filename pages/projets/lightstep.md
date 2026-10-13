---
title: LightStep
slug: lightstep
realisation:
  label: en cours
  color: yellow
etat:
  label: en cours de réalisation
  color: yellow
---

LightStep est un projet visant à faire travailler ensemble les marches du PianoStairs et Luz (une lampe LED programmable).

Les marches ont été remises à neuf et testées spécialement pour ce projet.

> ![luminaire](https://photos.haum.org/small/lightstep/lightstep_002_25212375723_o.jpg)

## Electronique

L'idée est d'alimenter la lampe, qui elle même alimente une carte Arduino via la liaison SPI. L'arduino, relié aux marches d'une part, renvoie les *patterns* à afficher à la lampe (*via* ladite liaison).

## Logiciel

Enfin, l'écriture du logiciel sans [PolychrHAUM](/pages/polychrhaum.html) a été envisagée. L'idée est d'implémenter directement *via* FastLED les animations pour la lampe. Une série d'animations a déjà été identifiée et il faut maintenant les mettre en oeuvre.
