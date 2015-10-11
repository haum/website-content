====================================
Guide pour réaliser ses propres PCBs
====================================

:date: 2015-10-10 23:00
:tags: hack
:category: hack
:slug: guide_pcb
:authors: MicroJoe
:summary: Tous les conseils pour réaliser soi-même des PCBs

Que vous soyez l’heureux possesseur d’une `PCBlastifieuse`_ ou non, ce guide à
pour but de détailler des différentes étapes de réalisation de circuits
imprimés en utilisant la méthode du transfert de toner.

Attention : ce guide évoque l’utilisation de produits chimiques qui sont
dangeureux et quit doivent être manipulés avec précaution. Vous êtes
responsables de vos faits et gestes lors de leur utilisation, le mieux étant de
se faire accompagner par des personnes ayant déjà utilisé ce procédé dans un
premier temps.


Conception du circuit
---------------------

Avant de pouvoir réaliser un PCB, il faut d’abord le concevoir. Le logiciel
libre `KiCAD`_ va vous permettre cela, en partant de la réalisation du schéma
électrique jusqu’à la création de la carte et la mise en place des éléments qui
la composent.

.. _KiCAD: http://kicad-pcb.org/

Si vous voulez utiliser une carte déjà réalisée par quelqu’un d’autre, assurez
vous qu’elle ne soit pas en négatif (technique utilisée pour la gravure avec
une autre méthode que celle présentée dans ce guide) et passez directement à
l’impression.

Impression du motif
-------------------

Il va falloir imprimer le motif du circuit sur un papier spécial qui va
permettre de transférer le toner de l’imprimante sur la plaque de cuivre
facilement.

Plusieurs types de papiers peuvent être utilisés, nottament le PNP Blue
(Peel'n'Pick) ou d’autres papiers spécialisés. Ceux-ci ont un côté imprimable
(papier) et l’autre non (plastique) qu’il faudra donc distinguer.

Voici la procédure à suivre :

 - Tout d’abord, imprimez le motif (en taille 1:1) sur une feuille de papier
   classique.

 - Ensuite, découpez un morceau de PNP Blue un peu plus grand quel a taille du
   motif et collez le sur la feuille que vous venez d’imprimer au niveau du
   motif avec du scotch facilement retirable (n’oubliez pas de placer le côté
   papier à l’extérieur.

 - En remettant la feuille dans le sens qui convient dans le bac, il suffit de
   relancer l’impression du motif pour que celui-ci soit cette fois ci déposé
   sur le bout de PNP Blue que l’on pourra détacher de la feuille par la suite.

Préparation de la plaque de cuivre
----------------------------------

Cette étape est cruciale car pour que le motif soit correctement transféré sur
la plaque de cuivre il faut que celle-ci soit très propre et sans impuretés.

 - Tout d’abord, afin d’enlever les éventuelles traces d’oxydation et autres
   saletés sur la plaque, il faut utiliser de la limaille de fer douce afin de
   frotter sur la plaque et enlever le gros des saletés.

 - Répéter cette étape autant de fois que nécessaire jusqu’à ce que le cuivre
   soit uniforme.

 - Une fois les poussières provoquées par la limaille soufflées de la plaque,
   imbiber un morceau d’essuie-tout d’acétone et frotter avec la partie
   cuivrée pour bien dégraisser la plaque.

 - Répéter cette étape jusqu’à ce que la feuille de d’essuie-tout soit propre
   même après avoir frotté vigoureusement celle-ci contre la plaque (ne pas
   hésiter à utiliser plusieurs feuilles pour toujours frotter avec quelque
   chose de propre, en utilisant de l’acétone à chaque fois).

La plaque est maintenant prête à recevoir le morceau de PNP Blue précédemment
imprimé.

 - Mettre le morceau de PNP contre la plaque de cuivre de façon à ce que le
   côté imprimé soit en contact avec la plaque.
 - Fixer le morceau de PNP pour bien qu’il appuie sur la plaque avec du scotch
   qui ne craint pas trop la température (éviter de recouvrir la surface du PNP
   contenant des pistes car le scotch va faire comme une sorte de bouclier
   thermique qui va gêner la fonte du toner).
 - Vérifier que le papier appuie bien uniformément sur la plaque (qu’il ne fait
   pas une genre de bosse une fois fixé sur la plaque car sinon le motif ne
   sera pas transféré).

Transfert du motif
------------------

Nous arrivons maintenant à l’étape la plus délicate de ce guide : le transfert
du motif du PNP vers la plaque de cuivre.

Nous allons considérer ici l’utilisation d’un appareil de type
`PCBlastifieuse`_ pour effectuer le transfert mais sachez qu’il est possible
(bien que pénible) de le faire à l’aide d’un fer à repasser classique.

 - Mettre l’appareil en route et attendre qu’il atteigne une température
   suffisamment élevée (au moins 180°C).
 - Passer la plaque plusieurs fois dans le « four », jusqu’à ce que le toner
   sur le PNP change d’apparence, manifestant le transfert du motif sur la
   plaque (attention, utilisez des gants ou un outil afin de ne pas vous brûler
   en manipulant la plaque).
 - Une fois le motif manifestement totalement transféré, passez la plaque au
   robinet sous de l’eau froide afin de refroidir le tout et de faire en sorte
   que le toner ne se décroche pas de la plaque.
 - Retirer très délicatement le film de PNP, les pistes doivent se retrouver
   sur le circuit et le PNP doit devenir transparent à ces endroits.

Si certains morceaux de piste n’ont pas été totalement transférés, il serait
possible de rattraper le coup en utilisant un marqueur permanent pour combler
certains passages ; par contre si seulement la moitié du motif se décolle ce
n’est pas la peine d’aller plus loin : renettoyez la plaque et réimprimez un
motif en tentant de savoir pourquoi le transfert a échoué (température trop
basse ? pas assez de passes pour permettre la fonte ? PNP qui ne touche pas
correctement la plaque ? plaque pas assez refroidie ? retirage trop brusque du
PNP ?).

Dissolution du cuivre
---------------------

Après l’étape délicate, nous attaquons l’étape la plus sujette à risques. En
effet, nous allons ici devoir manipuler des produits chimiques qui peuvent être
dangereux si on ne prend pas suffisamment de précautions.

Regroupez tout d’abord l’ensemble du matériel nécessaire à l’extérieur :

 - Bouteille d’eau oxygénée ;
 - Bouteille d’acide chlorhydrique ;
 - Récipient dans lequel la solution sera préparée et suffisamment grand pour
   pouvoir y poser la carte à plat ;
 - Une bouteille de récupération pour la solution usagée ;
 - Le futur PCB.

Puis équipez vous du matériel de protection nécessaire :

 - Blouse en coton ;
 - Gants de protection spécialisés contre le risque chimique (nitrile, …) ;
 - Lunettes de protection ;

Élimination de la solution
--------------------------

Une fois que le circuit a été rincé et mis de côté, il va falloir se
débarrasser de la solution ; rien ne sert de la conserver même si elle a peu
servi car elle va perdre ses propriétés au cours du temps. Pire même, elle va
dégager du gaz, ce qui pourrait faire exploser la bouteille dans laquelle elle
est stockée.

Elle est jetable dans les canalisations à condition de bien la diluer
auparavant pour ne pas faire de dégâts :

 - Verser la solution dans une bouteille de 1,5 L.
 - Compléter la bouteille avec de l’eau.
 - Verser le contenu de la bouteille dans un évier.

On peut ensuite rincer le reste de notre matériel :

 - Rincer les outils, récipiants, gants, etc..
 - Rincer l’évier une fois que tout le reste a été nettoyé.

Conclusion
----------

Vous avez maintenant toutes les clés en main pour réaliser vos propres PCBs
(mais pas forcément des PCBs propres par contre, ça viendra avec la pratique).

.. _PCBlastifieuse: /pages/pcblastifieuse.html
