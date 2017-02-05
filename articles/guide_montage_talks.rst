===================================
Le petit guide de montage des talks
===================================

:date: 2017-01-5 12:06
:tags: talks
:category: tuto
:slug: guide_montage_talks
:authors: MicroJoe
:summary: Tout ce que vous vouliez savoir sur le montage des talks sans jamais n'oser le demander

Bonjour à toi, petit contributeur curieux qui souhaite savoir comment sont
montés les talks du HAUM.

L'objectif du montage est de **réunir les différents fichiers vidéos et les
aligner avec la bande son externe**, de bien meilleure qualitée que le son de
la caméra. Une fois l'alignement réalisé on ajoutera **un titre au début et à
la fin de la vidéo** mentionnant le titre du talk, le nom du ou des talkers, et
la license CC-BY_ adoptée pour tous les talks.

Depuis les `HAUMTalks #8`_, l'ensemble des outils utilisés sont entièrement
libres, ce qui va permettre à d'autres personnes que moi de savoir comment
monter les vidéos des talks à partir des fichiers bruts.

.. _HAUMTalks #8: /pages/talks_session8.html

Les fichiers bruts
==================

Tout d'abord, il nous faut nous assurer d'être en possession de tous les
fichiers source bruts nécessaires au montage, à savoir :

- Les fichiers vidéos (parfois plusieurs par talk [1]_)
- Les fichiers audio stéréo, enregistrés avec le ZoomX

La vraie toute première étape est de trier tous les fichiers bruts en les
écoutant/visionant afin de les regrouper par talk.


.. _CC-BY: https://creativecommons.org/licenses/by/4.0/

.. [1] Le fait d'avoir plusieurs fichiers vidéo est lié à la limite de temps
   imposée aux constructeurs d'appareils photos, pour une raison de taxation
   différente de celle des caméscopes


Accélération du fichier audio
=============================

Le fichier audio du talk s'écoule plus lentement que celui de la vidéo, il va
donc falloir l'accélérer un tout petit peu pour pouvoir correctement l'aligner
avec la vidéo sans avoir de décalage au bout d'un certain moment.

Pour cela, nous allons utiliser **Audacity** afin d'accélérer la bande son.

Il faut effectuer une **accélération de 0,13 %** (passage de 100 % à 100.13 %).
Pour les curieux sachez que cette valeur a été obtenue empiriquement et qu'elle
est suffisamment précise pour la durée d'un morceau de vidéo (environ 20
minutes).

.. container:: aligncenter

    .. image:: /images/guide_montage_talks/audacity_speed.png

Une fois le son accéléré, on peut l'exporter au format non compressé
*Microsoft WAV flottant 32bit* (pas la peine de le compresser car ce
fichier n'aura pas besoin d'être distribué ; il sera très rapide à charger même
si il prendra pas mal de place sur votre disque dur).

Création d'un projet Kdenlive
=============================

Il est maintenant temps de créer un nouveau projet Kdenlive_. Nous allons créer
un projet par talk.

Le logiciel Kdenlive a été préféré à Pitivi_, du fait que ce
dernier soit très lent lors des phases de prévisualisation pendant le montage.
Vous êtes néanmoins libre d'utiliser un autre logiciel, il faudra simplement
adapter les étapes qui vont suivre.

Création d'un projet Kdenlive, donc. Pas de capture d'écran ici, il suffit
de l'installer, de le lancer, puis de créer un nouveau projet.

Ensuite, importez toutes les sources nécessaires au montage du talk sur lequel
vous allez travailler :

- Les fichiers vidéo du talk
- Le fichier audio accéléré au format WAV

Les plus attentifs d'entre vous auront remarqué qu'il manque l'image de titre
de début de talk ; celle-ci ne nous sera pas utile pour l'instant et nous
l'importeront en fin du montage.

.. _Kdenlive: https://kdenlive.org/
.. _Pitivi: http://www.pitivi.org/

Répartition des sources
=======================

On va maintenant pouvoir répartir grossièrement les différentes sources sur la
*timeline* avant de pouvoir tout bien caler correctement.

.. container:: aligncenter

  .. image:: /images/guide_montage_talks/placement_grossier.png

Les deux vidéos à la suite avec un petit écart, et le fichier sonore sur sa
propre piste audio.

Premier calage audio
====================

Voici l'étape qui demande le plus de temps en dehors de l'encodage (mais qui se
fait assez rapidement une fois que l'on a le coup de main).

Il faut faire correspondre le son du premier fichier vidéo avec le son du ZoomX
contenu dans le fichier audio accéléré.

Kdenlive possède une fonctionnalité d'alignement automatique de l'audio, mais
je n'ai pas réussi à la faire fonctionner ; étant donné que j'effectue
habituellement un calage manuel, c'est ce que nous allons faire ici.

Effets
------

Tout d'abord, nous allons appliquer des effets aux fichiers vidéo et audio afin
de simplifier ce calage manuel : l'objectif est de mettre le son de la vidéo à
gauche et le son "perche" à droite, afin de pouvoir bien distinguer les deux
lors de l'écoute au casque.

Étant donné que le son de la caméra est vraiment faible, nous allons également
devoir l'amplifier afin de pouvoir comparer le son des deux sources à l'oreille
plus facilement.

Si on résume les effets à appliquer :

- **Pour la vidéo**
    - **Amplification de 360%** (empirique, à adapter selon la vidéo)
    - **Panning à 0 pour le canal droit** (afin d'avoir tout le son stéréo
      sur la gauche)

- **Pour l'audio** (son perche)
    - **Panning à 1000 pour le canal gauche** (afin d'avoir tout le son stéréo
      sur la droite)

En image, voici ce que ça donne pour la piste audio :

.. container:: aligncenter

  .. image:: /images/guide_montage_talks/effets_alignement_audio.png

Et pour la vidéo :

.. container:: aligncenter

  .. image:: /images/guide_montage_talks/effets_alignement_camera.png

Vous pouvez maintenant écouter la prévisualisation afin de vous assurer que sur
la droite on a bien le son « propre » et à gauche le son de la caméra.
**L'utilisation d'un casque audio est indispensable** afin de bien percevoir
l'effet stéréo pour savoir de quel flux provient le son que vous entendez, et
pour caler le son *à la frame près*.

Vous pouvez de façon optionnelle créer un groupe d'effet pour chaque source
(vidéo ou audio) afin de placer tous les effets utilisés dedans en
glisser-déposer.  Ensuite enregistez le groupe d'effet, afin par exemple de ne
pas avoir à tout reconfigurer pour les prochains talks, ou même simplement
d'appliquer les effets de vidéo déjà réglés pour l'autre morceau de vidéo.

Parfois Kdenlive a tendance à appliquer les effets uniquement à partir d'un
certain moment. Cela va se manifester par un champ qui doit ressembler à
« début de l'effet », qu'il faudrait régler à 00:00 pour éviter ce décalage.

Calage
------

Une fois tous les effets correctement paramétrés, on peut vraiment passer au
calage audio.

L'objectif est de faire se correspondre le son de la vidéo et le son perche,
afin de pouvoir garder uniquement le son perche à la fin.

Il va donc falloir écouter (et réécouter encore et encore) la prévisualisation
en déplaçant, d'abord grossièrement, puis ensuite plus finement, la bande son
par rapport à la vidéo (ou inversement). Le zoom intégré à Kdenlive permet de
faire du calage *à la frame de vidéo près*.

Un autre outil pouvant aider au calage est la visualisation de la forme du
signal audio qui peut être utile quand on a plusieurs pics audio importants.
Il faudrait par exemple avant chaque talk taper deux fois dans les mains pour
avoir deux pics et ainsi permettre un calage visuel en regardant la forme
d'onde en plus du calage à l'oreille (mais bon, souvent on arrive à avoir une
personne qui tousse par talk, ce qui fait déjà un bon point de calage).

Finalisation
============

Audio final uniquement
----------------------

Une fois que le son est calé pour les deux morceaux de vidéo, on peut alors
désactiver les effets que l'on a appliqué (panning gauche/droite pour le casque)
ainsi que désactiver le son de la caméra (avec une icône en forme d'œil).

Si on lance une prévisualisation alors on a la vidéo de la caméra avec le son
du ZoomX en stéréo. On a donc réussi à avoir de l'audio correct en concordance
avec l'image de la caméra !

Ajout des titres
----------------

Il reste maintenant à récupérer le fichier SVG pour les titres des talks et de
l'ouvrir avec Inkscape_ afin de pouvoir changer le titre et le nom de l'auteur
(sans oublier le numéro de session des HAUMTalks). On importe ensuite ce
fichier SVG dans Kdenlive et on le place au début et à la fin de la vidéo
(durée de 5s), ainsi que dans le « trou » entre les deux vidéos si cela
s'applique.

.. _Inkscape: https://inkscape.org/fr/

Rendu
-----

Une fois que vous avez vérifié à coup de prévisualisations que tout s'enchaîne
bien aux points de jonction, il ne reste plus qu'à encoder la vidéo avec
l'outil d'exportation de Kdenlive.

J'utilise le format MP4 (H.264 de mémoire) en 720p (HD). Bien que ce format ne
soit pas libre, l'encodeur a l'avantage d'être plutôt rapide pour fournir un
résultat de taille raisonnable et de qualité correcte. J'ai essayé d'utiliser
WebM mais cet encodeur n'utilise pas tous les cœurs de ma machine de rendu et
est de fait beaucoup plus long pour arriver au final à un résultat comparable
à H.264.

Upload
------

Dernière étape, qui est très souvent chronophage sauf si vous avez une
connexion fibre et pas ADSL : uploader les quelques Go de vidéos des talks sur
un serveur pour les mettre à disposition sur le site.

Je conseille l'utilisation de rsync qui va passer par ssh pour uploader les
talks. L'avantage de rsync est qu'il peut reprende un téléversement interrompu
sans devoir redémarrer de zéro.

Si vous avez une connexion ADSL, alors lancer rsync avant d'aller vous coucher
devrait vous permettre d'avoir les talks mis en ligne sur le serveur à votre
réveil le lendemain matin !
