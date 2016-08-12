===========================================
Build d'une borne d'arcade raspberry nomade
===========================================

:date: 2016-08-10 10:00
:tags: hack
:category: hack
:slug: bartel_build
:authors: Marc
:summary:
:status: draft

Il y a 4 mois je me suis lancé dans la fabrication d'une petite borne nomade basée sur un minitel de premiere generation:

.. image:: http://s13.postimg.org/4mrr7w01z/minitel1_1.jpg

Le résultat
-----------

.. image:: http://img4.hostingpics.net/pics/45407720160812023837.jpg

.. image:: http://img4.hostingpics.net/pics/16221120160812023853.jpg

.. image:: http://img4.hostingpics.net/pics/15665620160812023907.jpg

.. image:: http://img4.hostingpics.net/pics/39900320160812023919.jpg

.. image:: http://img4.hostingpics.net/pics/29754420160812023938.jpg

.. image:: http://img4.hostingpics.net/pics/36550520160812023948.jpg

Cette idée ne viens pas de moi, j'ai été insipiré par les post de Ozone et de Glook et aussi le mec de FB (minitel Astro).
Je suis immédiatement tombé sous le charme.

Les fonctionnalités
-------------------

- chassis minitel 1
- ecran LCD 1024*768
- Joystick Sanwa
- 10 boutons multicolore seimitsu ps15 commandés chez smallcab (6 de jeux+ 2 de start/select sur le pannel)
- Theme super mario
- RPi 3
- retropie
- ampli 2.1 (TPA3116 50WX2 100W)
- speaker 2*10W 52MM large voice speaker + basse 1*50W 80mm
- Prise casque accessible en facade
- 27000mAh Li-Ion battery
- battery management system
- Low Bat indicateur
- divers:

  - port USB accessible en externe
  - port SD card accessible

La transformation
-----------------

Le minitel lors de son achat:

.. image:: http://img4.hostingpics.net/pics/20917220160428081622.jpg

Demontage et premiers choix: "qu'est ce que je garde, qu'est-ce que je jette?"

.. image:: http://img4.hostingpics.net/pics/81409920160602134146.jpg

.. image:: http://img4.hostingpics.net/pics/91983220160602140559.jpg

Coque exterieur
***************

Mise en peinture (cabine et support fabriqués pour l'occasion):

.. image:: http://img4.hostingpics.net/pics/82568020160618121956.jpg

.. image:: http://img4.hostingpics.net/pics/72818420160618122000.jpg

Percage des grilles de haut parleur "toad":

.. image:: http://img4.hostingpics.net/pics/15546120160612214251.jpg
.. image:: http://img4.hostingpics.net/pics/33454820160613090730.jpg

Thermoformage de la vitre en plexi pour donner un aspect retro:

.. image:: http://img4.hostingpics.net/pics/86683720160602221938.jpg
.. image:: http://img4.hostingpics.net/pics/84016220160602231927.jpg

Batterie
********

J'ai pas mal brainstormé sur la partie batterie car je veux absolument pouvoir jouer en nomade et ne pas me soucier de l'autonomie.
Cette solution me coute.....10€ car j'ai déja le chargeur, tout le reste est acheté sur ebay.cn. Les 18650 proviennent d'une recup massive de batterie d'ordinateur portable.
Voici une slide qui explique le cablage que je vais tester (je decline toute responsabilité dans le cas ou quelqu'un ferais le meme cablage et que ca prendrais feu / explosion / electrocution, batteries au Li-Ion donc un certain nombre de regles non mentionnées ici doivent etre respecté):

.. image:: http://img15.hostingpics.net/pics/617205batteryschematicV3.jpg

Recup des accus 18650 depuis des batteries d'ordinateur portable (tous de meme origine):

.. image:: http://img4.hostingpics.net/pics/86360920160502133856.jpg

Tri des accus:

.. image:: http://img4.hostingpics.net/pics/12724220160502215438.jpg

Test de la partie electronique pour gérer la batterie:

.. image:: http://img4.hostingpics.net/pics/79632020160602132859.jpg

.. image:: http://img4.hostingpics.net/pics/75412820160530220823.jpg

Re-assemblage de la batterie:

.. image:: http://img15.hostingpics.net/pics/70562620160629165848.jpg

.. image:: http://img15.hostingpics.net/pics/61727120160629165907.jpg

Realisation du pannel arriere:

.. image:: http://img4.hostingpics.net/pics/95691720160624083503.jpg

.. image:: http://img4.hostingpics.net/pics/44891720160804225607.jpg

De gauche à droite: port sd card, USB, pannel de reglage de l'ecran (5 bouttons + LED), port de charge de la batterie, interrupteur de mise en service de la batterie, jack d'alim.

Installation du systeme sur une planche:

.. image:: http://img4.hostingpics.net/pics/36189420160616135955.jpg

Son
***

Pour le son voici mon ampli audio:

.. image:: http://img15.hostingpics.net/pics/785184Audioamplifier.jpg

TPA3116 50wx2 +100 W 2.1 channel digital amplificateur
Je me suis un peu laché là...
Mais c'est un classe D, je ne pense pas pouvoir l'exploiter à 15% mais au moins je me suis fais plaisir.  :lol:

La molette do'rigine est reutilisée pour régler le volume:

.. image:: http://img4.hostingpics.net/pics/80082920160616133052.jpg

.. image:: http://img4.hostingpics.net/pics/95401420160616133059.jpg

Châssis interieur
*****************

Assemblage dans le chassis:

.. image:: http://img4.hostingpics.net/pics/18730920160729225029.jpg

.. image:: http://img4.hostingpics.net/pics/26996920160729225035.jpg

.. image:: http://img4.hostingpics.net/pics/30357520160729225048.jpg

.. image:: http://img4.hostingpics.net/pics/29617120160729225052.jpg

Installation du caisson de basse (jsute l'enceinte pour le moment):

.. image:: http://img4.hostingpics.net/pics/12843320160729231342.jpg

Bezel d'ecran
*************

Fraisage du support d'ecran:

.. image:: http://img4.hostingpics.net/pics/94862120160629210727.jpg

.. image:: http://img4.hostingpics.net/pics/43522720160629210745.jpg

Installation à l'aide d'aimant:

.. image:: http://img4.hostingpics.net/pics/27528620160630134129.jpg

Fraisage et installation du support de pannel en MDF de 12mm prise en sandwich entre le chassis et le pannel:

.. image:: http://img4.hostingpics.net/pics/75345220160630135052.jpg

Quelques photos du projet à ce stade:

.. image:: http://img15.hostingpics.net/pics/13658020160630123959.jpg

.. image:: http://img15.hostingpics.net/pics/28607920160630135052.jpg

.. image:: http://img4.hostingpics.net/pics/47952320160804225607.jpg

.. image:: http://img4.hostingpics.net/pics/30548420160630134105.jpg

Pannel
******

Usinage du pannel:

.. image:: http://img4.hostingpics.net/pics/87534120160810183921.jpg

.. image:: http://img4.hostingpics.net/pics/54907420160810185332.jpg

Pose du sticker à l'aide d'une petite table eclairante:

.. image:: http://img4.hostingpics.net/thumbs/mini_81738720160810214637.jpg

Detourage:

.. image:: http://img4.hostingpics.net/pics/64855920160810222538.jpg

Et pose du hardware (Les boutons du pannel suivent un code couleur pour reproduire les boutons de la SNES)

.. image:: http://img4.hostingpics.net/pics/92542220160810224749.jpg

Cablage des boutons sur une nappe:

.. image:: http://img4.hostingpics.net/pics/66060020160812001025.jpg

Raccordement de la nappe au RPI:

.. image:: http://img4.hostingpics.net/pics/26727220160812001050.jpg

On fait un peu de decoupe dans le fond du chassis:

.. image:: http://img4.hostingpics.net/pics/31471520160811224254.jpg

Installation du pannel:

.. image:: http://img4.hostingpics.net/pics/91146520160812001229.jpg

On remet l'ecran:

.. image:: http://img4.hostingpics.net/pics/77609020160812001325.jpg

Tout est en place! Build TERMINEE!!
