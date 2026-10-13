---
title: PCBlastifieuse
slug: pcblastifieuse
realisation:
  label: terminé
  color: brightgreen
etat:
  label: fondu (autodestruction)
  color: red
banner: /images/bannieres_projets/pcblastifieuse.1.jpg
---

## Qu'est ce que c'est ?

La PCBlastifieuse du HAUM est une plastifieuse A3 modifiée pour permettre de transférer le toner déposé par une imprimante laser sur un autre support que du papier.

## À quoi ça sert ?

Le principal objectif est de pouvoir l’utiliser dans un processus de fabrication maison de [circuits imprimés](https://fr.wikipedia.org/wiki/Circuit_imprim%C3%A9) (PCB en anglais) au HAUM. Néanmoins le transfert du toner peut s’effectuer sur tout support pouvant résister à la chaleur nécessaire à la fonte du toner (~ 200°C) et ayant le bon format pour rentrer dans la machine.

Voici quelques exemples d’utilisation de la PCBlastifieuse :

> - *Annotations* : apposer des dessins ou inscriptions sur une plaque, afin de repérer par exemple la position et le nom de ses composants électroniques ou encore simplement d’y estampiller un logo.
> - *Masque de gravure* : déposer une couche de protection délimitant des pistes électroniques afin d'immuniser temporairement ces zones de la plaque contre un traitement chimique (eau oxygénée + acide chlorhydrique) qui va retirer le cuivre non masqué.

## Matériel

Afin de réguler nous même l'allumage de l’élément chauffant de la plastifieuse, une carte Arduino ([code](https://github.com/haum/pcblastifieuse/)) couplée à un capteur de température et un relai allume ou éteint la résistance en fonction de la température mesurée.

<div class="container aligncenter">

![image](https://photos.haum.org/small/pcb/img_20150624_200308_18731859153_o.jpg)

</div>

Ce montage est placé en parallèle du montage d’origine de la machine, ce qui veut dire que si on ne branche pas l'Arduino alors la PCBlastifieuse fonctionnera en mode… plastifieuse !

Si vous souhaitez en apprendre plus sur la réalisation du hack, tout est détaillé dans [un article dédié](/hack_pcblastifieuse.html).
