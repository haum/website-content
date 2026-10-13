---
title: Timelapse
slug: timelapse
date: '2016-08-29T11:30:00'
authors:
- JackDesBwa
categories:
- tuto
tags:
- projet_labyrinthe_initiati
summary: Réalisation d'un timelapse
---

J'ai réalisé un timelapse du labyrinthe que nous avons présenté lors des Siestes Teriaki 2016. À cette occasion, voici un petit tutoriel pour présenter comment il a été réalisé.

## Timelapse ?

Une timelapse ou time-lapse est une technique photographique et cinématographique consistant à capturer une scène en omettant des bouts de temps. Une fois rejouée à vitesse normale, la vidéo résultante apparaît en accéléré.

Concrètement, nous allons prendre des photographies à intervalles réguliers et les assembler dans une vidéo pour revivre l'évènement en un temps court.

## Prise de vue

### Intervallomètre

Pour réaliser cet effet, nous allons prendre une photographie à intervalle régulier. Dans notre cas, l'appareil utilisé dispose d'un intervallomètre intégré qui simplifie les choses puisque nous n'aurons pas besoin d'opérateur qui observe sa montre toute la journée.

### Garder la forme

Poser l'appareil sur un trépied et revenir le chercher à la fin de la journée est très commode, mais il y a une difficulté technologique tout de même : l'appareil doit avoir suffisamment d'énergie en réserve.

Le premier jour, l'idée est venue sans avoir été préparée et l'appareil sorti du sac n'était pas complètement chargé. La prise de vue a duré un peu plus de 40 minutes. Seulement le début de l'installation a été capturé.

Le deuxième jour, la batterie chargée à bloc, l'appareil a réalisé environ 1h30 de capture avant épuisement. Il faudra donc prévoir une batterie supplémentaire pour les prochains essais.

## Développement

### Il y a foule

L'ensemble de ces 396 photographies en très haute résolution occupe 3.8Go de disque, malgré une compression en JPEG. Nous aurions pu réduire la résolution des images, mais compte tenu de la qualité médiocre du capteur, une haute résolution permettra de compenser légèrement ce handicap lors des traitements.

<div class="container aligncenter">

![Miniatures](/images/timelapse/miniatures.jpg)

</div>

Importées dans le logiciel darktable, nous voyons d'un simple coup d'œil la grande quantité de photos à traiter.

### Traitement

Pour réaliser le développement, nous allons être astucieux : il y a trois points de vue différents qui ont produit chacun des photographies à l'éclairage homogène. Nous n'allons donc développer que trois photographies et appliquer les mêmes réglages aux autres photos de la série.

Le processeur chauffe fort avec ces 8 cœurs occupés pendant quelques dizaines de minutes pour appliquer les traitements et réduire la taille des photographies à 960x720 pixels. Il y a toujours 396 clichés, mais le total ne pèse désormais plus « que » 342,3Mo.

## Overlay

Pour agrémenter le diaporama, nous allons ajouter un texte au-dessus de chaque photo. Pour cela, utilisons Inkscape pour dessiner cet overlay. En utilisant les trois photos-types en arrière-plan, nous pouvons nous assurer que cette surcouche s'accorde avec l'ensemble de la future vidéo.

<div class="container aligncenter">

![Overlay](/images/timelapse/overlay.jpg)

</div>

Une fois le dessin terminé, nous l'exportons en PNG avec transparence, en ayant pris soin de retirer les images de fond. Notons que l'overlay et toutes les images du timelapse sont de même définition (taille en pixels), ce qui simplifiera la suite.

## Assemblage

### À la queue leu leu

Avant de passer aux choses sérieuses, il faut nommer les prises de vues avec un format qui permettra à notre outil de reconnaître leur ordre. Pour cela, j'utilise GPRename pour renommer tous les fichiers sous la forme <span class="title-ref">laby_XXX.jpg</span> avec <span class="title-ref">XXX</span> un numéro d'ordre de trois chiffres.

### La formule magique

La formule magique qui réalise la vidéo est celle-ci :

    $ ffmpeg -r 8 -f image2 -i laby_%03d.jpg -i /tmp/overlay.png -filter_complex "overlay" -c:v libx264 -preset slow -crf 28 -c:a none -pix_fmt yuv420p laby_timelapse.mp4

### Explications succinctes

<span class="title-ref">ffmpeg</span> c'est la commande (utilitaire libre et multiplateforme) à laquelle nous donnons un ensemble d'images (format <span class="title-ref">image2</span>) dont le nom est <span class="title-ref">laby\_</span> suivi d'un numéro de séquence à trois chiffres ayant des zéros en tête suivi de <span class="title-ref">.jpg</span> et que nous jouerons à raison de <span class="title-ref">8</span> images par seconde.

Nous lui donnons aussi une seconde entrée <span class="title-ref">/tmp/overlay.png</span> que nous mixerons à l'aide du filtre <span class="title-ref">overlay</span>.

Le format de sortie vidéo est <span class="title-ref">libx264</span> avec un profile prédéfini pour l'encodage nommé <span class="title-ref">slow</span> avec pour paramètre <span class="title-ref">28</span> (c'est un nombre magique qui défini la qualité/compression finale). Le format de sortie audio est <span class="title-ref">none</span>.

Enfin, le fichier de sortie est <span class="title-ref">laby_timelapse.mp4</span> avec un encodage des couleurs en <span class="title-ref">yuv420</span>.

D'autres paramètres seront peut-être plus propices à votre usage. Je vous laisse expérimenter. Pour plus de détails, je vous renvoie au manuel de <span class="title-ref">ffmpeg</span> (RTFM).

### Accélération

Ayant pris une photo toutes les 20 secondes et les rejouant toutes les 1/8e de secondes, l'accélération obtenue est 160×. Avec 49 secondes de vidéos, nous retombons bien sûr les 2h10 réelles (les mathématiques sont cruellement inflexibles).

## Séquence de fin

### L'image

Pour finir la vidéo en apothéose, ajoutons le plan du labyrinthe pendant 10 secondes. Pour cela nous créons une image avec l'overlay intégré, le plan du labyrinthe, le logo de l'association et bien sûr une petite question pour narguer le visiteur : "Auriez-vous réussi à sortir ?" avec une emphase sur le verbe sortir.

### Vidéo

Même formule magique, avec deux images (identiques) pendant 5 secondes chacune :

    $ ffmpeg -r 0.2 -f image2 -i end_%d.png -c:v libx264 -preset slow -crf 28 -c:a none -pix_fmt yuv420p laby_end.mp4

### Assemblage

Tout est dans le bon format à la bonne définition, alors allons-y gaiement. Commençons par créer un fichier avec la liste des vidéos à concaténer.

    $ cat << EOF > concat.txt
    file laby_timelapse.mp4
    file laby_end.mp4
    EOF

Et réouvrons les grimoires :

    ffmpeg -f concat -i concat.txt -c copy laby.mp4

La vidéo finale pèse désormais 21Mo.

### Résultat

N'est-ce pas magnifique ?

<div class="container aligncenter">

<video width="960" height="720" controls>
    <source src="https://haum.svallee.fr/laby.mp4" type="video/mp4">
</video>

</div>
