==========================
Mobo illumine notre soirée
==========================

:date: 2016-12-06 23:00
:tags: stm32
:category: hack
:slug: stm32_hellomobo
:authors: JackDesBwa, Maximusk, LodeRunner, Gras
:summary: Démarrage warrior de la carte Mobo

Contexte
========

Tout commence l'an dernier par une idée folle d'atelier électronique. Il s'agissait de réaliser une petite carte à base de STM32, une famille de microcontrôleurs que nous voulions découvrir.
Le temps passe, l'idée revient. Nous commençons à expérimenter.

Une carte en une seule couche est nécessaire dans le cadre d'un atelier. Après tout, nous ne voulons pas briser de nombreux forets à percer des vias ou utiliser des plaques double-couche pour des schémas si simples. En essayant l'atelier, un membre expérimenté eût toutefois besoin de beaucoup de persévérance pour terminer le routage. Adieu atelier, nouvelle mise en sommeil.

Récemment, animé d'une pulsion artistique, et ne voulant pas laisser ce travail perdu, JackDesBwa a augmenté ce montage d'une forme originale et de dessins atypiques. Le tout a été tiré industriellement et le PCB résultant est arrivé hier. Le temps de souder les quelques composants qui le constituent et un Mobo était né.

.. container:: aligncenter

	.. image:: /images/stm32_articles/hellomobo_rendu.png
           :alt: Modèle 3D de la carte Mobo

Un programme inutile
====================

Dans un premier temps, nous constatons que le microcontrôleur est reconnu en le connectant en USB : le bootloader d'usine signale sa présence.
Il est donc temps de commencer à jouer avec.

En mode petits bourrins, nous suivons le tutoriel écrit en février dernier et le programme inutile ne fait effectivement rien. Mais à mieux y regarder, il ne fait pas le bon rien !

En suivant la progression du programme en mode pas-à-pas, nous nous apercevons que les adresses du pointeur programme sont complètement aberrantes. Une bonne demi-heure plus tard, nous comprenons subitement : on dévermine un programme qu'on a oublié de flasher. Une fois programmé, l'inutile bout de code se comporte adéquatement en ne faisant rien, correctement.

C'est un bon début.

Mode gros bourrins
==================

Bien barrés, nous décidons de jouer avec l'unique LED de la carte à la mode gros bourrins : pas de bibliothèque, que des pointeurs, des registres et une doc de 1800 pages sous le coude.

La première étape est de trouver les satanés registres nécessaires pour piloter une GPIO. Cela se trouve dans le 'reference manual', chapitre 'general purpose input/output', verset 'GPIO registers'. La messe est dite : c'est à l'offset 0x14.

Quoi ? Mais un offset par rapport à quoi ???

Là il faut aller consulter les saintes écritures de la cartographie mémoire. Le bloc GPIO-B commence à l'adresse 0x40021000. Et voilà, un gros pointeur dégueulasse en plein milieu du code avec une adresse en dur et une occulte valeur en hexadécimal sans commentaire aucun. Du grand n'importe quoi cosmique.

Ne soyons pas fous, il faut penser à passer la GPIO en sortie. Cette fois, c'est 0x48000400+0x00 le candidat. Et voilà, on compile, on pense à flasher cette fois, on envoie et... rien.

Vérifications faites, la broche est bien sur la fonction GPIO par défaut. Mais que manque-t-il ?

L'horloge, hosanna. Mais c'est bien sûr, pour que le bloc GPIO fonctionne, il faut qu'il reçoive un signal d'horloge. Là c'est l'épitre 'RCC' qui nous apporte la bonne parole : il fallait ajouter `*static_assert<volatile uint32_t *>(0x40021000 + 0x14) = 1 << 18`, tout simplement.

Une fois la carte mise en clock et reflashée... la lumière fût. Alléluia.

Encore moins subtil
===================

Ajoutons du calcul en masse, qui dans une longue tradition fructueuse... bouinera.
En effet de bord, un délai sera introduit sans aucune subtilité (non Arduino, ce n'est pas la bonne façon de faire !)

Pour attendre suffisamment longtemps, on copie-colle la boucle inutile.

« _Pourquoi tu ne fais pas une boucle de boucle ?

_ Parce que yyp est plus rapide à écrire. »

Et toujours en plein dans la vacuité en matière de finesse, nous éteignons le port complet au bout du «délai» ou ce qui passe pour cela.
Une boucle autour de ça et la lumière fût, puis ne fût plus, puis fût, puis ne fût plus, puis [yy100p], etc.

.. container:: aligncenter

	.. image:: /images/stm32_articles/hellomobo_photo.jpg
           :alt: Photographie de la carte finale avec la led allumée

        Ça ne se voit pas bien, mais il y a une discontinuité temporelle dans le flux lumineux rayonné par ce dispositif photoémetteur.

Documentation
=============

En plus de temps qu'il nous a fallu pour donner vie à la carte, nous avons rédigé cet éminent compte-rendu.

Concernant la forme, l'auteur n'a pas défini son intention, mais les témoins ont dit avoir vu : un fugu, une fraise, une carpe, un hérisson... Dans le fond, ça reste une question d'interprétation car en vérité je vous le dis, c'est une carte électronique.

Conclusion
==========

C'est joli, nous sommes contents (mieux ‽).
