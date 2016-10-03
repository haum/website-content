===========================================
Les projets du HAUM et comment y contribuer
===========================================

:slug: les-projets

Plusieurs projets ont été, sont ou seront développés au sein du HAUM.
L'objectif de ici est de vous les présenter en détails, de les documenter au fur et à mesure de leur avancement, et de vous informer des personnes à contacter si vous souhaitez en savoir davantage pour participer à leur élaboration/maintenance.

À noter que pour garantir une certaine lisibilité ainsi qu'une certaine visibilité pour les plus "petits" projets, ceux a contrario plus "importants" sont présentés au travers d'une page dédiée.

Nos projets
===========

.. list-projects::

Envie de contribuer ?
=====================

Autant que faire se peut, les projets du HAUM sont sous licences Open-source et leurs sources logicielles librement accessibles sur la plateforme GitHub.

Le `dépôt du HAUM`_ est ainsi plein de projets auxquels vous pouvez contribuer si vous le souhaitez ! Forkez les dépôts qui vous intéressent et faites nous une pluie de *pull-requests* !
Si on vous croise deux trois fois au HAUM et qu'on vous aime bien, on vous donnera un bel accès à l'organisation elle-même pour directement contribuer *upstream* :)

En attendant voilà les projets softwares (ou de rédaction) auxquels vous pouvez contribuer pour nous aider :

- Haumtalks : https://github.com/haum/haumtalks
- AxiHAUM : https://github.com/haum/axihaum
- Formation arduino : https://github.com/haum/forma_arduino
- Haniview : https://github.com/haum/hanivew
- TwitterBot : https://github.com/haum/TwitterBot
- timeoAPI : https://github.com/haum/timeoAPI
- heeksCNC (parce qu'on va s'en servir sous peu) : https://code.google.com/p/heekscnc/

.. _dépôt du HAUM: https://github.com/haum/

Vu qu'on est des hackers, la *todolist* de l'asso est aussi `sur github`_. Si le coeur vous en dit, commentez les tickets ou mieux, essayez de voir comment les fixer !

.. _sur github: https://github.com/haum/haum_internal/issues/

Haniview
--------

Haniview a pour objectif de hacker l'afficheur à LEDs bi-colores (vert et rouge) de jblb_ pour l'utiliser sous GNU/Linux, afficher des images, etc.
Ce projet est supporté par jblb_,  neomilium_ et  matael_.

HaumBots
--------

Actuellement, 3 bots travaillent pour nous : Twaum (Twitter ⇔ IRC), bcazeneuve (Mises à jour du site, gestion de l’agenda, ouverture du local, récupération des liens sur notre subreddit_, …), et un `bot GitHub`_ qui notifie sur notre chan IRC les différents évèments git (push, pull-resquest & co) des principaux dépots git de l'association.
Il fut un temps où combot, un bot codé en Perl avec amour par matael, nous servait bien, mais il a laissé sa place à bcazeneuve (pour les mêmes fonctions), un bot basé sur une infrastructure de microservice, monté par notre MicroJoe.

Vous pouvez contribuer à Twaum ou au bot GitHub en forkant un des dépôts suivants ou bien pinger matael_ ou feedoo_ sur IRC :

- https://github.com/haum/TwitterBot
- https://github.com/Matael/GithubBot

Vous pouvez aussi contribuer à bcazeneuve en forkant un des dépots commençant par HMS sur le github du HAUM. Voici ceux existant à l'heure de l'écriture de cet article :

- https://github.com/haum/hms_irc (Connexion IRC)
- https://github.com/haum/hms_spacestatus (Ouverture du local)
- https://github.com/haum/hms_agenda (Gestion de l'agenda)
- https://github.com/haum/hms_website (Mise à jour du site)
- https://github.com/haum/hms_logger (Log des conversations IRC)
- https://github.com/haum/hms_reddit (Récupération des liens reddit)
- https://github.com/haum/hms_ping (Ping des éléments de l'infra HMS)
- https://github.com/haum/hms_base (Base de developpement pour un nouveau module HMS)
- https://github.com/haum/hms_help (Aide de fonctionnement de l'infrastructure)

Notre dévoué combot est toujours présent sur GitHub, dans l'état où il se trouvait avant son arrêt :

- https://github.com/haum/combot


.. _bot GitHub: http://blog.fredblain.org/2014/05/github-bot-pour-irc
.. _subreddit: https://www.reddit.com/r/haum

.. _neomilium: http://twitter.com/neomilium
.. _matael: http://twitter.com/matael
.. _jblb: http://twitter.com/jblb_72
.. _rebrec: https://twitter.com/elfrancesco
.. _feedoo: http://twitter.com/fblain
