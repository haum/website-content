---
title: Opendata Crunching
slug: opendata-crunching
realisation:
  label: terminé
  color: brightgreen
etat:
  label: fonctionnel
  color: brightgreen
banner: /images/bannieres_projets/opendata-crunching.1.jpg
---

Au HAUM, on aime les trucs ouverts, les codes sources ouverts, les portes ouvertes, les gens ouverts, les bières ouvertes et bien sûr : les **données ouvertes** !

<div class="container alignright">

<img src="/images/opendata/parkings_nantes.jpg" width="400" alt="image" />

alt  
Parking Nantes

</div>

Vu qu'au Mans, les données ouvertes, c'est pas encore ça, nous, on titille un peu. Ça a commencé gentillet en utilisation des [données de Nantes](http://blog.matael.org/writing/dataporn-les-parkings-de-nantes/) dans une présentation publique au Mans.

Les parkings de Nantes, c'était rigolo.... mais... on pouvait aller plus loin.

<div class="container clearer">

</div>

## Setram

Depuis, on a joué avec les données de la SETRAM.

<div class="container alignright">

<img src="/images/opendata/timeomap.png" width="400" alt="image" />

alt  
Carte TIMEO

</div>

Cette fois ci, il s'agissait de pouvoir récupérer les informations de passage des bus et tram sur Le Mans.

Sachant que la SETRAM propose un service (appelé [Timeo](http://www.setram.fr/698-TIMEO2C-l-info-en-temps-reel.html)) d'accès aux horaires de passage en temps réel, nous avons écrit un *wrapper* Python permettant de récupérer facilement ces données et une API pour y accèder *over HTTP*.

Ces projets sont disponibles sur le github du HAUM pour l'API et sur celui de [matael](http://twitter.com/matael) pour le *wrapper* :

- *wrapper* (**pyTimeo**) :
  - [pytimeo@github](https://github.com/Matael/pytimeo)
  - [documentation](http://pytimeo.rtfd.org)
- API (**timeoapi**) :
  - [Accès HTTP](http://timeoapi.haum.org)
  - [timeoapi@github](https://github.com/haum/timeoAPI)
  - [documentation de l'API](http://timeoapi.rtfd.org)

Histoire de documenter un peu le processus, on a aussi rédigé deux articles : un [article technique](http://blog.matael.org/writing/cyber-ouvre-boite-opendata-ou-pas/) pour expliquer l'analyse et un autre plus politique et [explicatif](http://blog.matael.org/writing/cyber-ouvre-boite-le-concept/) pour mettre en avant l'intérêt de cette action.

## Data Citoyenne

L'opendata est un moyen de transparence important et l'année 2014 a vu deux élections.

<div class="container twocolumns">

<div class="container alignleft">

<img src="/images/opendata/municipales.png" width="300" alt="image" />

alt  
Cartes municipales

</div>

<div class="container textcolumn">

Les élections municipales ont été pour le HAUM un bon prétexte pour s'intéresser à ce type de données. Après un lent et douloureux *mapping* des secteurs de vote sur Le Mans, nous avons pu recréer une [carte des résultats](http://umap.openstreetmap.fr/fr/map/le-mans-elections_6485#12/47.9773/0.2575).

Là aussi, deux articles ont accompagné la carte : comme auparavant [le premier](http://blog.matael.org/writing/scrutin-et-opendata-parlons-technique/) explique les aspects techniques et [le second](http://blog.matael.org/writing/scrutin-et-opendata-le-concept/) les aspects politiques.

</div>

</div>

<div class="container clearer">

</div>

<div class="container twocolumns">

<div class="container alignright">

<img src="/images/opendata/europeennes.png" width="300" alt="image" />

alt  
Carte européennes

</div>

<div class="container textcolumn">

Comme les élections européennes étaient dans la foulée et que la manière de présenter les données n'avait pas changé, nous avons remis ça et créé de nouveau une [carte](http://umap.openstreetmap.fr/en/map/elections-europeennes-14-sur-le-mans_10621#13/47.9852/0.2379).

</div>

</div>

<div class="container clearer">

</div>

## Et maintenant ?

L'opendata est encore à ses débuts et tout reste à faire. Si vous voulez en savoir plus sur nos actions ou même mieux y participer, contactez nous *via* la [mailing-list](https://lists.haum.org) , le [twitter](http://twitter.com/haum72) ou parlez en avec [jblb](http://twitter.com/jblb_72), [feedoo](http://twitter.com/fblain) ou [matael](http://twitter.com/matael).

Pour vous mettre l'eau à la bouche, en ce moment, ça cause des données d'endettement et de la répartition des équipements culturels.
