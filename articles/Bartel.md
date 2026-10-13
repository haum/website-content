---
title: Fabrication d'une borne d'arcade Raspberry nomade
slug: bartel_build
date: '2016-08-10T10:00:00'
authors:
- Marc
categories:
- hack
tags:
- hack
summary: Modification d'un minitel en console rétro à base de Raspberry Pi
---

Il y a 4 mois je me suis lancé dans la fabrication d'une petite borne nomade basée sur un Minitel de première génération:

![Minitel](http://s13.postimg.org/4mrr7w01z/minitel1_1.jpg)

## Le résultat

<img src="http://img4.hostingpics.net/pics/801152401.jpg" class="align-center" alt="Resulat 1" />

<img src="http://img4.hostingpics.net/pics/871202414.jpg" class="align-center" alt="Resulat 2" />

<img src="http://img4.hostingpics.net/pics/642689775.jpg" class="align-center" alt="Resulat 3" />

<img src="http://img4.hostingpics.net/pics/397377307.jpg" class="align-center" alt="Resulat 4" />

<img src="http://img4.hostingpics.net/pics/553136568.jpg" class="align-center" alt="Resulat 5" />

<img src="http://img4.hostingpics.net/pics/507907849.jpg" class="align-center" alt="Resulat 6" />

<img src="http://img4.hostingpics.net/pics/5468387710.jpg" class="align-center" alt="Resulat 7" />

<img src="http://img4.hostingpics.net/pics/8722898311.jpg" class="align-center" alt="Resulat 8" />

<img src="http://img4.hostingpics.net/pics/3716595512.jpg" class="align-center" alt="Resulat 9" />

<img src="http://img4.hostingpics.net/pics/3465689813.jpg" class="align-center" alt="Resulat 10" />

<img src="http://img4.hostingpics.net/pics/5838321314.jpg" class="align-center" alt="Resulat 11" />

<img src="http://img4.hostingpics.net/pics/1140588215.jpg" class="align-center" alt="Resulat 12" />

<img src="http://img4.hostingpics.net/pics/4393724916.jpg" class="align-center" alt="Resulat 13" />

<img src="http://img4.hostingpics.net/pics/9599368917.jpg" class="align-center" alt="Resulat 14" />

<img src="http://img4.hostingpics.net/pics/2426101318.jpg" class="align-center" alt="Resulat 15" />

<img src="http://img4.hostingpics.net/pics/7357938319.jpg" class="align-center" alt="Resulat 16" />

<img src="http://img4.hostingpics.net/pics/863985DSC02442.jpg" class="align-center" alt="Resulat 17" />

Cette idée ne vient pas de moi, j'ai été inspiré par les *posts* de **Ozone** et de **Glook** (forum.hyperfreespin.fr) ainsi que **minitel Astro** sur FaceBook. Je suis immédiatement tombé sous le charme.

## Les fonctionnalités

- chassis minitel 1
- écran LCD 1024\*768
- Joystick Sanwa
- 6 boutons multicolore seimitsu ps15 commandés chez smallcab
- 2 bouttons de start/select sur le pannel
- Theme super mario
- RPi 3
- retropie
- ampli 2.1 (TPA3116 50WX2 100W)
- speaker 2\*10W 52MM large voice speaker + basse 1\*50W 80mm
- Prise casque accessible en facade
- 27000mAh Li-Ion battery
- battery management system
- indicateur de batterie faible
- divers:
  - wifi
  - port USB accessible en externe
  - port SD card accessible

## La transformation

Le minitel lors de son achat :

<img src="http://img4.hostingpics.net/pics/20917220160428081622.jpg" class="align-center" alt="Minitel lors de l&#39;achat" />

Démontage et premiers choix: *"qu'est ce que je garde, qu'est-ce que je jette?"*

<img src="http://img4.hostingpics.net/pics/81409920160602134146.jpg" class="align-center" alt="Démontage 1" />

<img src="http://img4.hostingpics.net/pics/91983220160602140559.jpg" class="align-center" alt="Démontage 2" />

### Coque extérieure

Mise en peinture (cabine et support fabriqués pour l'occasion) :

<img src="http://img4.hostingpics.net/pics/82568020160618121956.jpg" class="align-center" alt="Peinture 1" />

<img src="http://img4.hostingpics.net/pics/72818420160618122000.jpg" class="align-center" alt="Peinture 2" />

Percage des grilles de haut parleur "Toad" :

<img src="http://img4.hostingpics.net/pics/15546120160612214251.jpg" class="align-center" alt="Percage 1" />

<img src="http://img4.hostingpics.net/pics/33454820160613090730.jpg" class="align-center" alt="Percage 2" />

Thermoformage de la vitre en plexi pour donner un aspect rétro :

<img src="http://img4.hostingpics.net/pics/86683720160602221938.jpg" class="align-center" alt="Thermoformage 1" />

<img src="http://img4.hostingpics.net/pics/84016220160602231927.jpg" class="align-center" alt="Thermoformage 2" />

### Batterie

J'ai pas mal brainstormé sur la partie batterie car je voulais absolument pouvoir jouer en nomade et ne pas me soucier de l'autonomie. Cette solution me coûte... 10€ car j'ai déja le chargeur, tout le reste est acheté sur ebay.cn. Les 18650 proviennent d'une recup massive de batterie d'ordinateur portable. Voici une slide qui explique le câblage que je vais tester (je décline toute responsabilité dans le cas ou quelqu'un ferait le meme câblage et que ca prendrait feu / explosion / electrocution ; ce sont des batteries au Li-Ion donc un certain nombre de règles non mentionnées ici doivent etre respectées) :

<img src="http://img15.hostingpics.net/pics/617205batteryschematicV3.jpg" class="align-center" alt="Cablage" />

Récup des accus 18650 depuis des batteries d'ordinateur portable (tous de même origine) :

<img src="http://img4.hostingpics.net/pics/86360920160502133856.jpg" class="align-center" alt="Accus" />

Tri des accus :

<img src="http://img4.hostingpics.net/pics/12724220160502215438.jpg" class="align-center" alt="Tri des accus" />

Test de la partie électronique pour gérer la batterie :

<img src="http://img4.hostingpics.net/pics/79632020160602132859.jpg" class="align-center" alt="Test électronique" />

<img src="http://img4.hostingpics.net/pics/75412820160530220823.jpg" class="align-center" alt="Test électronique" />

Re-assemblage de la batterie :

<img src="http://img15.hostingpics.net/pics/70562620160629165848.jpg" class="align-center" alt="Réassemblage de la batterie" />

<img src="http://img15.hostingpics.net/pics/61727120160629165907.jpg" class="align-center" alt="Réassemblage de la batterie" />

### Panneau arrière

Réalisation du panneau arrière :

<img src="http://img4.hostingpics.net/pics/95691720160624083503.jpg" class="align-center" alt="Panneau arrière" />

<img src="http://img4.hostingpics.net/pics/44891720160804225607.jpg" class="align-center" alt="Panneau arrière" />

De gauche à droite: port carte SD, USB, panel de réglage de l'écran (5 boutons & 1 LED), port de charge de la batterie, interrupteur de mise en service de la batterie, jack d'alimentation.

Installation du système sur une planche :

<img src="http://img4.hostingpics.net/pics/36189420160616135955.jpg" class="align-center" alt="Installation sur une planche" />

### Son

Pour le son voici mon ampli audio :

<img src="http://img15.hostingpics.net/pics/785184Audioamplifier.jpg" class="align-center" alt="Ampli audio" />

TPA3116 50wx2 +100 W 2.1 channel digital amplificateur

Je me suis un peu lâché là...

Mais c'est un classe D, je ne pense pas pouvoir l'exploiter à 15% mais au moins je me suis fait plaisir.

La molette d'origine est reutilisée pour régler le volume :

<img src="http://img4.hostingpics.net/pics/80082920160616133052.jpg" class="align-center" alt="Molette" />

<img src="http://img4.hostingpics.net/pics/95401420160616133059.jpg" class="align-center" alt="Molette" />

### Châssis intérieur

Assemblage dans le chassis :

<img src="http://img4.hostingpics.net/pics/18730920160729225029.jpg" class="align-center" alt="Chassis" />

<img src="http://img4.hostingpics.net/pics/26996920160729225035.jpg" class="align-center" alt="Chassis" />

<img src="http://img4.hostingpics.net/pics/30357520160729225048.jpg" class="align-center" alt="Chassis" />

<img src="http://img4.hostingpics.net/pics/29617120160729225052.jpg" class="align-center" alt="Chassis" />

Installation du caisson de basse (juste l'enceinte pour le moment) :

<img src="http://img4.hostingpics.net/pics/12843320160729231342.jpg" class="align-center" alt="Installation caisson de basse" />

### Bezel d'écran

Fraisage du support d'écran :

<img src="http://img4.hostingpics.net/pics/94862120160629210727.jpg" class="align-center" alt="Support écran" />

<img src="http://img4.hostingpics.net/pics/43522720160629210745.jpg" class="align-center" alt="Support écran" />

Installation à l'aide d'aimants :

<img src="http://img4.hostingpics.net/pics/27528620160630134129.jpg" class="align-center" alt="Installation aimant" />

Fraisage et installation du support en MDF (12mm) pour le panneau avant. Il est pris en sandwich entre le châssis et le panneau :

<img src="http://img4.hostingpics.net/pics/75345220160630135052.jpg" class="align-center" alt="Fraisage support" />

Quelques photos du projet à ce stade:

<img src="http://img15.hostingpics.net/pics/13658020160630123959.jpg" class="align-center" alt="Borne" />

<img src="http://img15.hostingpics.net/pics/28607920160630135052.jpg" class="align-center" alt="Borne" />

<img src="http://img4.hostingpics.net/pics/47952320160804225607.jpg" class="align-center" alt="Borne" />

<img src="http://img4.hostingpics.net/pics/30548420160630134105.jpg" class="align-center" alt="Borne" />

### Panneau avant

Usinage du panneau avant :

<img src="http://img4.hostingpics.net/pics/87534120160810183921.jpg" class="align-center" alt="Usinage panneau avant" />

<img src="http://img4.hostingpics.net/pics/54907420160810185332.jpg" class="align-center" alt="Usinage panneau avant" />

Pose du sticker à l'aide d'une petite table éclairante :

<img src="http://img4.hostingpics.net/thumbs/mini_81738720160810214637.jpg" class="align-center" alt="Pose sticker" />

Détourage :

<img src="http://img4.hostingpics.net/pics/64855920160810222538.jpg" class="align-center" alt="Détourage" />

Et pose du *hardware* (les boutons du panneau avant suivent un code couleur pour reproduire les boutons de la SNES) :

<img src="http://img4.hostingpics.net/pics/92542220160810224749.jpg" class="align-center" alt="Installation hardware" />

Câblage des boutons sur une nappe :

<img src="http://img4.hostingpics.net/pics/66060020160812001025.jpg" class="align-center" alt="Cablage boutons nappe" />

Raccordement de la nappe au RPi :

<img src="http://img4.hostingpics.net/pics/26727220160812001050.jpg" class="align-center" alt="Raccordement nappe RPi" />

On fait un peu de découpe dans le fond du châssis :

<img src="http://img4.hostingpics.net/pics/31471520160811224254.jpg" class="align-center" alt="Découpe chassis" />

Installation du panneau :

<img src="http://img4.hostingpics.net/pics/91146520160812001229.jpg" class="align-center" alt="Installation chassis" />

On remet l'ecran :

<img src="http://img4.hostingpics.net/pics/77609020160812001325.jpg" class="align-center" alt="Installation écran" />

Tout est en place !

**Build TERMINÉ !!**
