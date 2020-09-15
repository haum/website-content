==========================================
Teriaki 2020, le HAUM au temps du COVID-19
==========================================

:date: 2020-09-15 23:30
:tags: projet_pong1d, 2020, teriaki, epau
:category: news
:slug: teriaki2020
:authors: Jblb, JackDesBwa & Loderunner
:summary: Pong sans contact en 2020

Contexte
========

L'année 2020 a vu un arrêt total du monde et des mesures de prévention contre la pandémie de COVID-19 un peu partout. Malgré la limitation imposée sur les rassemblements festifs encore en vigueur fin août, les `Siestes Teriaki`_ ont pu avoir lieu (mais sans chaise longue).

Comme chaque année, le HAUM a répondu présent à l'invitation. Cependant, il nous fallait trouver une installation qui soit compatible avec les contraintes sanitaires du moment. Pas facile quand la base de nos créations est l'interactivité avec le public et des commandes tactiles !

Cogito
======

Première contrainte : le temps. Avec l'incertitude de la période, nous avons été prévenus tardivement que les siestes auraient finalement lieu. Il restait alors deux mois pour trouver une idée, vérifier son concept et la mettre en œuvre.

Nous venions tout juste de reprendre les séances au local après quelques mois de rencontres virtuelles par visioconférence pendant le confinement général et quelques semaines qui ont suivi. Le sujet est naturellement arrivé dans la discussion et comme toujours, au détour d'une boutade, est venue l'idée d'une interaction sans contact ; restait à trouver comment la réaliser et à quel projet l'appliquer.

De manière pragmatique, étant donné le peu de temps disponible, nous avons passé en revue les différents projets déjà réalisés et le choix s'est imposé : nous redéfinirions le `Pong1D`_. L'idée était de remplacer les boutons (donc tactiles digitaux) par des capteurs détectant la présence de la main à distance.

Experimento
===========

Hasard heureux, l'un des membres présents ce soir-là avait, dans sa caravane, un capteur infrarouge par réflexion. Ni une, ni deux, nous nous emparons du sésame, direction l'établi pour un premier test immédiat. Sous les yeux ébahis du généreux fournisseur, nous l'avons fait fonctionner en quelques minutes alors que lui-même avait renoncé auparavant.

On-Off-On-Off... Ça fonctionnait bien, en tout cas dans le principe, mais quelque chose nous gênait : la portée était très faible (deux centimètres tout au plus) et donc le risque de toucher accidentellement le support dans l'euphorie du jeu était très grand. Il fallait détecter plus loin.

D'un côté nous avons fait quelques essais pour améliorer la portée du dispositif, mais le succès était très limité. Les télémètres ultrasons n'étaient pas plus pratiques car leur cône large et leur temps de réponse auraient rendu l'interaction peu intuitive. Mais cette idée en a menée une autre : nos voisins ST_ ont un produit de télémétrie très réactif dont nous pensions pouvoir tirer profit.

Après avoir exposé le projet à la direction, nous avons rapidement été soutenus et ils nous ont même offert deux de ces télémètres laser. La réception a été quelque peu folklorique dans cette période estivale, mais nous avons bien reçu le colis et il restait donc à les mettre en œuvre.

Quelques lignes de code plus tard, et beaucoup de grattage de tête avant de s'apercevoir que des résistances externes étaient indispensables (les pull-up internes ne fonctionnaient pas) nous avions une distance ! Très rapidement, nous avons ajouté une sortie open-collector et testé sur le vrai Pong avec succès.

Fabricato
=========

Toutes les briques étant réunies, il faillait créer le mortier pour les lier. Deux axes principaux : les boîtes accueillant les capteurs et la connectique à recâbler.

Dans un premier temps, nous avions envisagé de créer une boîte en bois, mais la conception était laborieuse. En se baladant dans le local, une nouvelle boutade nous a amené à sérieusement envisager de transformer une sorbetière et une cafetière en boîte atypique pour nos capteurs. Finalement, ce sont deux tirelires cylindriques transparentes qui ont retenu notre attention.

La fente pour insérer la pièce était tout juste assez large pour faire passer la partie active du capteur. Un morceau de mousse découpée circulairement au laser permettait de coincer la cartelette dans la partie haute tandis que les fils de communication redescendaient vers une carte de contrôle dans la partie basse s'ajustant elle-même au millimètre près dans l'espace disponible. Nous avons seulement percé un trou pour sortir le câble allant vers le Pong.

Pour les câbles justement, nous avons trouvé dans l'espace free-to-hack de quoi satisfaire nos appétits. L'alimentation a été ajoutée dans le lien et le tout a été encapsulé dans une connectique personnalisée du plus bel effet.

Trois morceaux de palette, un bout de tube PVC, de la peinture dans l'escalier, un bout de support découpé au laser... et nous voilà avec un rehausseur de capteur tout en beauté.

Côté Pong, nous avons profité du design transparent des capteurs pour proposer une électronique exposée, elle aussi dans une boîte transparente, improvisée en un soir avec un couvercle thermoformé récupéré, découpé et plié pour l'occasion.

Avec tout ça, nous étions fin prêts.

.. container:: aligncenter

  .. image:: https://photos.haum.org/small/teriaki2020/IMG_20200821_095229.jpg
    :alt: Rehausseur en construction

  .. image:: https://photos.haum.org/small/teriaki2020/IMG_20200916_001716.jpg
    :alt: Pong avec capot transparent

  .. image:: https://photos.haum.org/small/teriaki2020/IMG_20200916_002553.jpg
    :alt: Tirelire capteur

Veni, vidi, lusi*
=================

\* Indicatif parfait de ludere

Nous voilà le jour J. Cette année, l'installation est plutôt légère (pour une fois) et nous la montons en une dizaine de minutes avec un coup de main (et d'échelle) de l'équipe technique de l'abbaye de l'Épau. Il ne restait qu'à attendre le public... en regardant la pluie tomber dans le cloître.

Malgré tout, les premiers spectateurs arrivent et la jauge de seulement 5 visiteurs est vite atteinte. Les agents de sécurité nous aidaient à contrôler le flux de festivaliers. Le port du masque et les distances physiques permettaient de profiter de ce moment festif sans que les mesures ne paraissent trop contraignantes.

Les parties s'enchaînent sans contact, avec un réel intérêt du public happé par le jeu et ébahi par l'ingéniosité ayant transformé une contrainte (négatif) en une expérience de jeu atypique (positif). Enfin, jusqu'à ce que...

.. container:: aligncenter

  .. image:: https://photos.haum.org/small/teriaki2020/teriaki20_01.jpg
    :alt: Joueurs l'un contre l'autre

Fregi*
======

\* Indicatif parfait de frangere

Lors de la conception, nous avions un doute sur la longueur des pieds des rehausseurs et envisagions de les raccourcir pour éviter aux joueurs de taper dedans. L'idée était passée. Mais la question s'est finalement ré-imposée en fin d'après-midi lorsqu'un festivalier a buté dedans, faisant vaciller puis tomber le support, entraînant le capteur inexorablement vers le sol.

Si le spectateur n'a pas eu mal et a pu continuer à pérégriner joyeusement, ce ne fut pas le cas de notre capteur. Celui-ci a en effet entamé son ultime voyage... en deux morceaux !

Nous voilà donc en fin d'après-midi du samedi, avec seulement un capteur sachant capter ; et pas moyen de réparer le second.

Cogito [denuo]
==============

Il fallait encore une fois être créatifs pour pouvoir se passer d'un capteur tout le reste du week-end, d'autant plus que nous n'avions pas les boutons originels sous la main.

Rapidement, il parait évident qu'il faut modifier le code du jeu pour que la machine joue contre les prochains joueurs humains. La modification a été faite rapidement et 15 minutes plus tard, les premiers matchs contre l'intelligence artificielle avaient lieu.

.. container:: aligncenter

  .. image:: https://photos.haum.org/small/teriaki2020/teriaki20_02.JPG
    :alt: Joueurs contre l'IA

Dimanche
========

Nous revoilà le lendemain avec un jeu contre la machine. Dans un premier temps, nous avons cherché à améliorer le rendu du jeu de celle-ci pour paraître plus naturel. Mais nous faisions tout de même assez rapidement le constat que l'enthousiasme des visiteurs est beaucoup moindre quand il n'y a pas d'adversaire incarné, avec qui rire et commenter les échanges.

Entre-temps, nous avions pu récupérer les boutons historiques et avons donc très vite recâblé pour proposer des matchs humain contre humain, avec un adversaire utilisant le bouton sans contact (visiteur) et l'autre avec le bouton physique (HAUM).

L'entrain est immédiatement revenu et la journée s'est très bien passée. Nous avons même eu plusieurs fois des files d'attente extérieures malgré une pluie légère.

.. container:: aligncenter

  .. image:: https://photos.haum.org/small/teriaki2020/teriaki20_03.JPG
    :alt: Public attendant sous la pluie

À la fin, avant de démonter totalement notre installation, nous avons invité les agents de sécurité qui nous ont bien aidé à contrôler les flux de visiteurs tout le week-end, à jouer quelques parties avec nous.

Bilan
=====

Compte tenu du contexte de vigilance sanitaire et de la mauvaise météo (première fois en sept ans de participation pour nous), la fréquentation était très bonne. Nous avons eu peu de pauses pendant tout le week-end et elles étaient courtes. Le retour des visiteurs (et de l'équipe organisatrice, et de l'abbaye) était très enthousiaste.

Il faut sans conteste remercier les équipes qui ont œuvré pour que l'évènement ait lieu malgré le contexte pandémique et qui ont montré qu'il est possible d'organiser un tel évènement dans de très bonnes conditions de sécurité sanitaire sans qu'elles ne paraissent contraignantes.

Du côté du Pong, il est intéressant de noter l'importance de l'interaction entre les joueurs au-delà du jeu lui-même qui participe énormément du plaisir de jouer. Nous avons pensé, mais un peu tard, qu'il serait utile d'ajouter un repère fixe indiquant la zone dans laquelle le joueur peut taper la balle (histoire de simplifier le jeu et l'explication à un public passant). Tardivement également, nous avons ajouté un repère indiquant lorsque le faisceau était interrompu, ce qui a fortement amélioré la jouabilité. Bref, le Pong a été amélioré encore une fois.

.. _Siestes Teriaki: http://www.teriaki.fr/
.. _Pong1D: /pages/1dpong.html
.. _ST: https://www.st.com/
.. _Haum: https://haum.org
