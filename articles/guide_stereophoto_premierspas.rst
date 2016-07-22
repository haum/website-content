===================================
Premiers pas en stéréo photographie
===================================

:date: 2016-07-19 22:39
:tags: hack
:category: hack
:slug: guide_stereophoto_premierspas
:authors: JackDesBwa et LodeRunner
:summary: Premiers pas en stéréophotographie

Contexte
--------

Pour aller plus loin dans le domaine de la photographie, après le
lightpainting, nous nous sommes intéressés aux photographies
stéréoscopiques.

Il s'agit de pairs de clichés dont l'assembage minutieux révèle la
profondeur pour provoquer l'émerveillement. Ces images en relief offrent
une expérience visuelle immersive et époustouflante.

Cette page propose sans prétention un mini-tutoriel pour faire vos
premiers pas en la matière. Nous découvrons en même temps le procédé,
alors ne prenez pas tout au pied de la lettre et expérimentez (avec
nous).

Nous essaierons de compléter cette page au gré de nos découvertes.

Principe
--------

Nous ne nous attarderons pas ce soir sur le principe. Dans les grandes
lignes, il s'agit de présenter deux photographies adéquatement choisies
et légèrement différentes pour chaque œil. Ainsi, le cerveau reconstruit
le relief.

De nombreuses ressources détaillent le principe avec des schémas à
l'appui. Bonne navigation pour apprinfondir le sujet.

Prise de vues
-------------

Bougez, bougez, bougez... pour trouver le bon sujet.

Dans un premier temps, il convient de choisir une scène avec de la
profondeur. Le procédé capture le relief, il ne le crée pas.

Nous avons remarqué que le rendu était plus sympathique lorsque la
profondeur est limitée et continue. C'est-à-dire qu'il ne faut pas trop
de distance entre le premier et le dernier plan, et qu'il est préférable
d'avoir des éléments intermédiaires pour renforcer l'effet.

Le cerveau n'aime pas le flou en 3D en général. Il faudra donc préférer
des focales courtes et des ouvertures réduites pour obtenir une grande
profondeur de champ. C'est l'inverse de la photographie 2D.

Aussi, il est très important que la scène ne change pas entre les deux
vues. Pour cela, on peut utiliser des appareils synchronisés. Dans
l'exemple de ce petit guide, nous utilisons un seul appareil et nous
devons donc veiller à choisir des sujets immobiles : attention aux
feuillages, aux animaux, aux personnes, aux voitures, aux ombres et
lumières... Il est conseillé, surtout lorsque l'on utilise un seul
appareil, de cadrer plus large que la scène que l'on souhaite capturer
car nous aurons probablement à retailler les bords de l'image à la fin
du traitement.

Enfin, et certainement le plus important, il faut que les images soient
légèrement différentes. Pour cela, nous déplaçons l'objectif
latéralement. Il faut éviter de trop faire converger les axes optiques
(un décalage parallèle est préférable, surtout pour des sujets
moyennement lointains).

L'écart entre les prises de vues (appelée base stéréographique) dépend
de l'éloignement des plans du sujet. Par exemple pour des paysages
lointains, un écartement de plusieurs mètres augmente l'effet de
profondeur (hyperstéréoscopie) alors que la macrostéréoscopie requiert
des écartements de quelques millimètres.

Par exemple, choisissons ceux deux vues. La base était de l'ordre de 6 à
10 cm :

.. container:: aligncenter

	.. image:: /images/stereo/guide_premierspas/left.jpg
	.. image:: /images/stereo/guide_premierspas/right.jpg

Notez que ces clichés pris à main levée ne réunissent pas les conditions
optimales pour constituer un couple stéréographique. En plus du
déplacement horizontal, il y a un décalage vertical et angulaire par
exemple. Néanmoins, nous allons voir qu'il est possible, dans une
certaine mesure, de corriger ces défauts logiciellement.

Traitement logiciel
-------------------

Nous utilisons la suite hugin_ dont le premier usage est de réaliser des
panorama. Nous allons tirer profit de ses excellents algorithmes de
correction de perspective, de lentilles, de rotation, d'exposition, etc.

Afin de ne pas trop se fatiguer à entrer tous les points de contrôle à
la main dans l'interface graphiques, nous allons réaliser un
prétraitement en ligne de commande. Appelons left.jpg et right.jpg les
images respectivement destinés à l'œil gauche et droit.

La commande suivante va aligner les images en créant un fichier de
projet hugin (option -p), optimiser pour une translation en x (option
-x), configurer les algorithmes en mode stéréo (option -A) et proposer
un cadrage (option -C).

::

	$ align_image_stack -p stereo.pto -x -A -C left.jpg right.jpg 
	Run called
	Inner 512 6974464: 256 3392 - 256 2480
	Starting 512: 256 3392 - 256 2480
	Starting 256: 256 3392 - 256 2480
	Starting 128: 0 3392 - 256 2736
	Starting 64: 0 3520 - 128 2736
	Starting 32: 0 3520 - 64 2736
	Starting 16: 0 3520 - 64 2736
	Starting 8: 0 3520 - 48 2736
	Starting 4: 0 3520 - 40 2736
	Starting 2: 0 3524 - 36 2736
	Starting 1: 0 3524 - 36 2736
	Set crop size to 0,35,3524,2736
	Written project file stereo.pto

Il est maintenant possible d'ouvrir le projet dans hugin.

.. container:: aligncenter

	.. image:: /images/stereo/guide_premierspas/screenshot_pointsdecontrole.jpg

Dans l'onglet "Points de contrôle", après avoir sélectionné les vues
gauche et droite, nous voyons les points de correspondance trouvés dans
l'opération précédente.

Ces points sont les similitudes entre les deux images trouvées par
l'algorithme, dont il se servira pour aligner les vues. Pour que
l'algorithme d'alignement donne un bon résultat, il faut bien sûr
s'assurer qu'il n'y a pas d'erreur de reconnaissance et que les points
soient si possible répartis sur toute l'image.

À défaut, il faut en ajouter : un clic sur la photo de gauche sur un
point fixe reconnaissable et présent sur les deux vues ; puis un un clic
sur la photo de droite au même endroit (il se peut que l'interface
ajuste seule la correspondance) ; enfin un clic droit valide l'ajout du
point de contrôle.

Dans la colonne alignement sous les photos, il faut s'assurer que tous
les points de contrôle sont de type "ligne horizontale", en particulier
ceux ajoutés à la main.

Enfin, il faut choisir un de ces points à passer en type d'alignement
"normal". Un point proche de l'observateur semble bien fonctionner et
évite certaines incohérences de profondeur.

Maintenant, passons à la fenêtre d'aperçu rapide (icône avec un paysage
et les lettres GL).

.. container:: aligncenter

	.. image:: /images/stereo/guide_premierspas/screenshot_rendu.jpg


Ici, le bouton "Aligner..." lancera l'optimisation des paramètres de
déformation des images pour réaliser l'alignement à partir des points de
contrôle que nous avons définis. Une fenêtre s'ouvre pour résumer les
calculs en cours. Lorsqu'elle se ferme, nous pouvons passer au
recadrage.

Le recadrage s'effectue dans l'onglet "Recadrer". Pensez à afficher
alternativement les deux vues pour être certain que l'intégralité du
cadre contienne les deux photos.

Il faut alors exporter notre travail. De retour dans l'onglet
"Assistant", il faut s'assurer que les deux vues sont actives puis
cliquer sur le bouton "Créer le panorama...". L'important est de cocher
la case "Conserver les images intermédiaires" car c'est celles-ci qui
nous serviront dans la dernière étape.

Nous apposerons les deux vues côte-à-côte sur la même image. Pour
simplifier le traitement, nous utilisons imagemagick et son utilitaire
montage.

::

	montage *_exposure_layers_0001.tif *_exposure_layers_0000.tif -geometry +0+0 -background black stereo.jpg

Voilà, notre image est prête a être visionnée !

.. container:: aligncenter

	.. image:: /images/stereo/guide_premierspas/dhaum2.jpg

Maintenant, à vous de jouer ;-)

.. _hugin: http://hugin.sourceforge.net/
