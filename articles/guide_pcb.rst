====================================
Guide pour réaliser ses propres PCBs
====================================

:date: 2015-10-12 19:25
:tags: hack
:category: hack
:slug: guide_pcb
:authors: MicroJoe, Marc
:summary: Tous les conseils pour réaliser soi-même des PCBs

Que vous soyez l’heureux possesseur d’une `PCBlastifieuse`_ ou non, ce guide à
pour but de détailler des différentes étapes de réalisation de circuits
imprimés en utilisant la méthode du transfert de toner.

**Attention : ce guide évoque l’utilisation de produits chimiques qui sont
dangeureux et qui doivent être manipulés avec précaution**.

Vous êtes responsables de vos faits et gestes lors de leur utilisation, le
mieux étant de se faire accompagner par des personnes ayant déjà utilisé ce
procédé dans un premier temps.

Liste des précautions
---------------------

Avant tout, merci de lire la liste de précautions à prendre et de bien la
retenir avant de vous lancer dans la moindre manipulation :

 - **Toujours verser de l'acide dans de l'eau** et pas l'inverse car il y a
   risque d'éclaboussure ("explosion").

 - L'acide chlorhydrique est dangereux, l’eau oxygénée encore plus (mains, yeux).
   **Ces produits sont à manier avec précaution et avec les protections
   adaptées** (gants, lunettes de protection). **Seule la personne équipée
   peut manipuler les bouteilles et ustensiles** (gouttes sur les bouteilles,
   reste de réactif sur les ustensiles pas encore nettoyés…)

 - **Attention à ne pas renverser de réactif**, que ce soit sur le sol ou pire
   sur des personnes, protégées ou non. **Celui qui manipule est responsable de
   ses maladresses**.

 - Ne pas fermer la bouteille d’eau oxygénée trop fort (risque d'explosion du
   fait de sa forte concentration).

 - **Le mélange acétone / eau oxygénée est très dangereux** : faites attention
   dans vos manipulations à ne pas combiner les deux et à toujours les stocker
   loin l’un de l’autre pour éviter tout risque d’explosion en cas de fuite ou
   de renversement.

 - **Travaillez dans un endroit aéré ou sous hotte aspirante**, il ne faut pas
   respirer les émanations résultantes de la réaction (elle produit du
   dichlore, un gaz jaune-vert plus dense que l’air qui possède une odeur
   suffocante désagréable et est qui est extrêmement toxique).


Conception du circuit
---------------------

Avant de pouvoir réaliser un PCB, il faut d’abord le concevoir. Le logiciel
libre `KiCAD`_ va vous permettre cela, en partant de la réalisation du schéma
électrique jusqu’à la création de la carte et la mise en place des éléments qui
la composent.

.. _KiCAD: http://kicad-pcb.org/

.. container:: aligncenter

    [flickr:id=22925193186]

Si vous voulez utiliser une carte déjà réalisée par quelqu’un d’autre, assurez
vous qu’elle ne soit pas en négatif (technique utilisée pour la gravure avec
une autre méthode que celle présentée dans ce guide) et passez directement à
l’impression.

Impression du motif
-------------------

Il va falloir imprimer le motif du circuit sur un papier spécial qui va
permettre de transférer le toner de l’imprimante sur la plaque de cuivre
facilement.

.. container:: aligncenter

    [flickr:id=22322864273] [flickr:id=22930589112]

Plusieurs types de papiers peuvent être utilisés, notament le PNP Blue
(Peel'n'Pick) ou d’autres papiers spécialisés. Ceux-ci ont un côté imprimable
(papier) et l’autre non (plastique) qu’il faudra donc distinguer.

Voici la procédure à suivre :

 - Tout d’abord, imprimez le motif (en taille 1:1) sur une feuille de papier
   classique.

 - Ensuite, découpez un morceau de PNP Blue un peu plus grand quel a taille du
   motif et collez le sur la feuille que vous venez d’imprimer au niveau du
   motif avec du scotch facilement retirable (n’oubliez pas de placer le côté
   papier à l’extérieur. L'ideal est du scotch de tapissier / scotch de masquage.

 - Le toner est déposé côté rugueux de la feuille de PNP.

 - En remettant la feuille dans le sens qui convient dans le bac, il suffit de
   relancer l’impression du motif pour que celui-ci soit cette fois ci déposé
   sur le bout de PNP Blue que l’on pourra détacher de la feuille par la suite.

Préparation de la plaque de cuivre
----------------------------------

Cette étape est cruciale car pour que le motif soit correctement transféré sur
la plaque de cuivre il faut que celle-ci soit très propre et sans impuretés.

 - Tout d’abord, afin d’enlever les éventuelles traces d’oxydation et autres
   saletés sur la plaque, il faut utiliser de la paille de fer douce afin de
   frotter sur la plaque et enlever le gros des saletés.

 - Répéter cette étape autant de fois que nécessaire jusqu’à ce que le cuivre
   soit uniforme.

 - Une fois les poussières provoquées par la paille de fer soufflées de la plaque,
   imbiber un morceau d’essuie-tout d’acétone et frotter avec la partie
   cuivrée pour bien dégraisser la plaque.

 - Répéter cette étape jusqu’à ce que la feuille de d’essuie-tout soit propre
   même après avoir frotté vigoureusement celle-ci contre la plaque (ne pas
   hésiter à utiliser plusieurs feuilles pour toujours frotter avec quelque
   chose de propre, en utilisant de l’acétone à chaque fois).

 - le brossage à la paille de fer peut etre remplacé par un poncage à l'eau et avec du papier de verre fin (600).

 - le brossage permet aussi de creer des aspérités sur le cuivre et va promouvoir l'adherence du toner sur celui-ci

 - afin de garantir un resultat parfait, on peut nettoyer la plaque juste avant tranfert avec de l'alcool isopropylique. Celui ci eliminera toute trace de doigt eventuel.

Voici le resultat sur une plaque qui est décapé avec un "tarnish remover" type mirror mais qui n'a pas été frotté:

 [flickr:id=25546035903]

La plaque est maintenant prête à recevoir le morceau de PNP Blue précédemment
imprimé.

.. container:: aligncenter

    [flickr:id=22930586852] [flickr:id=22321275904]

Étapes à suivre :

 - Mettre le morceau de PNP contre la plaque de cuivre de façon à ce que le
   côté imprimé soit en contact avec la plaque.
 - Fixer le morceau de PNP pour bien qu’il appuie sur la plaque avec du scotch
   qui ne craint pas trop la température (éviter de recouvrir la surface du PNP
   contenant des pistes car le scotch va faire comme une sorte de bouclier
   thermique qui va gêner la fonte du toner).
 - Du Kapton est idéal pour ce type de projet car il est fin et il resiste à la chaleur.
 - Vérifier que le papier appuie bien uniformément sur la plaque (qu’il ne fait
   pas une genre de bosse une fois fixé sur la plaque car sinon le motif ne
   sera pas transféré). Deux morceaux de scotch suffisent, un en haut et un en bas.

Alternative au PNP
------------------

Le PNP étant onéreux d'autres solutions sont également envisagables, cependant le résultat est nettement moins bon.
Pour 1€25 on peux se procurer 10 feuilles A4 de papier de transfert sur eBay.
Le toner est déposé côté lisse.
Voici le resultat obtenu pour un PCB avec des pistes de 0.5 mm - 1 mm de large:

.. container:: aligncenter

    [flickr:id=25543915594]

On remarque sur la photo que du toner manque par petits points sur le "thermal pad" du regulateur. En fait, c'est une lacune de ce papier. Sur des plans, le resultat est encore moins convaincant. Sur la photo suivante, on voit un transfert avec du PNP à gauche, papier jaune à droite:

.. container:: aligncenter

    [flickr:id=26148688695]

Il semblerait que le PNP depose en plus du toner une petite pelicule plastique qui protege encore mieux le toner lors de la gravure :

.. container:: aligncenter

    [flickr:id=25546035613]


Transfert du motif
------------------

Nous arrivons maintenant à l’étape la plus délicate de ce guide : le transfert
du motif du PNP vers la plaque de cuivre.

Nous allons considérer ici l’utilisation d’un appareil de type
`PCBlastifieuse`_ pour effectuer le transfert mais sachez qu’il est possible
(bien que pénible) de le faire à l’aide d’un fer à repasser classique.

.. container:: aligncenter

    [flickr:id=22918010446] [flickr:id=22525696458]

Étapes :

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

.. container:: aligncenter

    [flickr:id=22551834459] [flickr:id=22551831489]

Si certains morceaux de piste n’ont pas été totalement transférés, il serait
possible de rattraper le coup en utilisant un marqueur permanent pour combler
certains passages ; par contre si seulement la moitié du motif se décolle ce
n’est pas la peine d’aller plus loin : renettoyez la plaque et réimprimez un
motif en tentant de savoir pourquoi le transfert a échoué (température trop
basse ? pas assez de passes pour permettre la fonte ? PNP qui ne touche pas
correctement la plaque ? plaque pas assez refroidie ? retirage trop brusque du
PNP ?).

.. container:: aligncenter

    [flickr:id=22755974720] [flickr:id=22525681208]

Dissolution du cuivre
---------------------

Après l’étape délicate, nous attaquons l’étape la plus sujette à risques. En
effet, nous allons ici devoir manipuler des produits chimiques qui peuvent être
dangereux si on ne prend pas suffisamment de précautions.

Tout d’abord équipez vous du matériel de protection nécessaire :

 - Blouse en coton ;
 - Gants de protection spécialisés contre le risque chimique (nitrile, …) ;
 - Lunettes de protection ;

Ensuite regroupez l’ensemble du matériel nécessaire à l’extérieur :

 - Bouteille d’eau oxygénée ;
 - Bouteille d’acide chlorhydrique ;
 - Récipient dans lequel la solution sera préparée et suffisamment grand pour
   pouvoir y poser la carte à plat ;
 - Une bouteille de récupération pour la solution usagée ;
 - Le futur PCB.

Dans le récipient qui va accueillir la plaque, préparez la solution suivante en
prenant bien soin de verser l’acide dans l’eau et pas l’inverse :

 - 1/3 d’eau (de préférence distillée) ;
 - 1/3 d’acide chlorydhrique ;
 - 1/3 d’eau oxygénée.

.. container:: aligncenter

    [flickr:id=22955115671] [flickr:id=22321241694]

Arrive maintenant le moment de vérité : plongez la plaque à plat dans la
solution et éloignez vous du récipient car des émanations toxiques (dichlore)
vont être produites pendant la réaction.

.. container:: aligncenter

    [flickr:id=22917975576] [flickr:id=22930543702]

Une fois que la réaction est devenue moins violente, controlez à intervalles
régulier l’état de la plaque en la sortant de la solution avec des pincettes en
plastique afin de pouvoir l’examiner ; sortez définitivement la plaque de la
solution quand le cuivre non recouvert par le toner sur la plaque aura
totalement disparu.

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

.. container:: aligncenter

    [flickr:id=22329500133]

Étant donné la non-réutilisabilité de la solution, il parrait intéressant de
procéder à cette réalisation de PCBs par batchs de plusieurs plaques pour
éviter de gâcher trop de solution qui doit être active pour plusieurs plaques
(étant donné que l’on ne peut pas la stocker).

Il est important d’effectuer cet ensemble d’étapes dans la foulée, car le toner
n’est plus d’aussi bonne qualité si le PNP Blue est par exemple mis de côté
pendant une semaine après avoir été imprimé ou la solution gardée pour une
prochaine fois mais au final inutilisable.

N.B. : Ce guide n’est pas définitif, n’hésitez pas à le modifier afin de
rajouter des précisions, améliorer sa mise en page ou même l’illustrer !


Références :

 - http://www.instructables.com/id/Making-PCB-With-Heart-Toner-Transfer-Paper-and-Lam/step6/null/
 - http://www.instructables.com/id/Mostly-easy-PCB-manufacture/step5/Iron/
 - https://paulwanamaker.wordpress.com/perfect-single-or-double-sided-pcbs-with-the-toner-transfer-method/
 - http://bensdiy.blogspot.fr/2008/10/ralisation-de-circuits-imprims.html

.. _PCBlastifieuse: /pages/pcblastifieuse.html
