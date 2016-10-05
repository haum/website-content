======
1Dpong
======

:slug: 1dpong

:projet_realisation: terminé-brightgreen
:projet_etat: fonctionnel-brightgreen

.. image:: /images/bannieres_projets/1dpong.1.jpg
	:alt: 1DPong

Qu'est ce que c'est?
====================

Le 1DPong est avant tout un jeu. Les deux joueurs s'affrontent en face à face en renvoyant une "balle" materialisée
par un point lumineux se déplaçant sur une rangée de LEDs.

Bien que la balle ne puisse se déplacer que sur une seule dimension, les joueurs doivent faire preuve d'adresse pour
renvoyer la balle au bon moment et peuvent user de stratégie pour envoyer la balle plus ou moins fort selon le
risque encouru. Par ailleurs, la bande de LEDs souple permet de varier la difficulté selon la forme que l'on donne
à la trajectoire parcourue par la balle.

Le jeu au demeurant simple est ludique et addictif.

Utilisation
===========

Chaque joueur choisit une manette qui déterminera son côté. Pendant l'affichage d'attente, les deux joueurs doivent maintenir
le bouton de la manette enfoncé pour que la partie commence. Il existe un mode "CONQUER" qui est activé par un double clic maintenu par
les deux joueurs.

La partie commence par une balle qui traverse la bande de LEDs. Lorsqu'elle arrive de son côté, chaque joueur doit la
renvoyer. Si l'on appuie trop tôt, la balle n'est pas renvoyée. Trop tard, le point est perdu. Pour matérialiser la zone
de renvoi, la balle change de couleur.

Notez que la balle accélère de plus en plus à mesure que la partie avance. Les joueurs peuvent également influencer
momentannément la vitesse de la balle. En effet, elle est renvoyée d'autant plus rapidement qu'elle est frappée proche
de la fin de la bande.

Le score est affiché à chaque point par une barre de progression qui part de l'extrêmité. Plus on a de points, plus la
barre de notre couleur est longue. En mode normal, la partie se termine lorsque les deux barres se rencontrent. En mode
"CONQUER", il est encore possible de grignoter les points de l'autre et la partie s'arrête lorsqu'un joueur a conquis tous
les points.

Fabrication
===========

Matériel
--------

Le matériel, c'est ce qui subit la force d'attraction de la Terre et que l'on transporte à chaque fois que l'on déplace le Pong.

On peut le diviser en deux parties: ce que l'on voit, *la boîte* et ce que l'on ne voit pas : l'électronique qui est dans la boîte et le programme qui pilote l'électronique.

Mise en boite
~~~~~~~~~~~~~

Comme le HAUM dispose d'une `fraiseuse numérique`_, c'est l'outil que nous avons utilisé pour la création du boîtier. La fraiseuse a aussi été mise à contribution pour la création de circuits «imprimés» indispensables à la connexion des différents ensembles électroniques.

.. _fraiseuse numérique: /pages/axihaum.html

Électronique
~~~~~~~~~~~~

En plus du ruban de LEDs qui assure l'affichage, on trouve deux parties principales: l'alimentation et le contrôle.

- Ruban de LEDs : ruban de LEDs adressables WS2812 (acheté sur *la bay*)
- L'alimentation : une alim ATX (récupérée sur un vieux PC)
- Le contrôle : une carte Arduino Mini avec son interface USB-série


Logiciel
--------

Le logiciel utilise la bibliothèque PolychrHAUM_ pour les animations et la gestion du matériel (LEDs, boutons...)

Sur le `dépôt`_ sur lequel est sauvegardé le code, vous trouverez le code, les instructions pour la compilation
(émulateur PC et code embarqué), le paramétrage pour adapter à votre copie...

Le dossier *sprites* contient les éléments graphiques qui seront affichés sur le bandeau. Par exemple la balle
est dessinée dans la classe BallSprite. Grâce à cet objet, l'application n'a plus qu'à indiquer qu'elle veut
dessiner la balle et l'objet calcule tout seul les couleurs à afficher pour ajouter l'effet de trainée ou passer
la balle en couleur. Il en va de même pour les batons et le score.

Le dossier *game* contient la logique du jeu. La classe *game_manager* gère l'affichage en cours. Les autres
classes indiquent ce qu'il faut afficher dans chaque écran du jeu.

L'écran *poweroff* est utilisé lorsque l'alimentation de puissance est éteinte. Dans cet écran, rien ne s'affiche
et l'on attend simplement que l'alimentation soit réactivée pour réinitialiser le jeu.

L'écran *waitplayers* est celui qui s'affiche après l'écran *poweroff*. Dans cet écran, nous attendons que les
joueurs valident leur participation. Une petite animation permet aussi de patienter. Lorsque les deux joueurs
ont validé, une petite animation sert de transition avant de passer à l'écran suivant.

L'écran *playing* est le cœur du jeu. C'est dans cet écran que l'on joue ! Il gère les échanges balles et le décompte
des scores. Lorsqu'un des joueurs gagne un point, un nouvel écran s'affiche.

L'écran *score* affiche le score courant. Il attend une validation des joueurs et permet éventuellement de quitter
la partie.

L'écran *rainbow* est affiché en fin de partie et a une vocation purement décorative.

L'écran *testhardware* fut initialement créé pour tester le bandeau de LEDs pour chaque couleur de chaque LED.

[flickr:id=16329255616]

Et après ?
==========

Concernant le jeu lui-même, il y a déjà un mode CONQUER qui change la difficulté du jeu. Nous pensons également
à la possibilité de jouer en réseau avec un autre 1DPong ou encore exploiter le double clic pendant le jeu.

.. _PolychrHAUM: /pages/polychrhaum.html
.. _dépôt: https://github.com/haum/ponghaum
