=======================================
Comment modifier le contenu du site web
=======================================
:status: hidden

Préambule
`````````
Le site web du **HAUM** est un espace collaboratif qui peut être enrichi par chacun de ses membres.
Cette page se veut un aide mémoire pour que chacun dispose des informations nécéssaires à la création de contenu sur ce site.

Édition de texte directement sur github
```````````````````````````````````````

Souvent, le membre contributeur souhaite seulement corriger des fautes d'orthographes ou ajouter un paragraphe supplémentaire au contenu déjà présent, voire créer une page et y ajouter sa prose personnelle. Dans ces cas, nul besoin de sortir la grosse artillerie !

En étant identifié sur la plateforme Github avec un identifiant présent dans le groupe HAUM, il suffit de
visiter le dépôt website-content_. Muni des droits sus-cités, un petit icône en forme de crayon apparaît
sur les documents préexistants. Il n'y a plus qu'à éditer directement dans la page !

De même, lorsque l'on souhaite ajouter une page, il faut se placer dans le dossier afférant et cliquer sur le signe "+" qui apparaît à la suite du chemin du dossier visité. Attention, si github propose un fork ou pas de "+", c'est que vos droits ne sont pas suffisants.

Une fois la modification effectuée, une zone en bas de page permet de valider la modification et y adjoindre un message. Ce message permet de tracer les intentions de chacun et constituer un historique. Il faut qu'il soit suffisamment clair, par exemple : ajout d'un paragraphe pour l'édition depuis github dans la page howto. Un second champ permet (optionnellement) de préciser si l'action ne peut être décrite en quelques mots.

L'appui sur le bouton commit sauvegarde les changements.

Enfin, il faut passer sur le salon IRC pour demander à un des modérateurs de lancer une mise à jour du site (après qu'il aura vérifié que tout se passera bien).

Préparation de l'environnement de travail
`````````````````````````````````````````

Installation des pré-requis
+++++++++++++++++++++++++++

Pour isoler l'environnement Python, il est recommandé d'utiliser "Virtualenv" :
``$ sudo apt-get install python-virtualenv`` (Ubuntu) ou ``$ pip install virtualenv``  (MacOS)

Récupération des sources et configuration initiale
++++++++++++++++++++++++++++++++++++++++++++++++++

	- Cloner ([#]_) le dépôt git de la structure du site web : ``$ git clone git@github.com:haum/website.git`` ;
	- Cloner le dépôt git du contenu du site web : ``$ git clone git@github.com:haum/website-content.git`` ;
	- Se déplacer vers le répertoire de travail : ``$ cd website`` ;
	- Créer un lien entre le squelette et le contenu : ``$ ln -s ../website-content/ content`` ;
	- Préparer l'environement virtuel : ``$ virtualenv .pelican -ppython2`` ;
	- Activer l'environement virtuel : ``$ source .pelican/bin/activate`` ;
	- Installer pelican, qui est necessaire pour tous les autres paquets : ``$ pip install pelican`` ;
	- Installer les requirements : ``$ pip install -r requirements.txt`` ;

Voilà, l'ensemble des pré-requis est installé, tant coté système que dans l'environnement local.

Édition et publication du contenu
`````````````````````````````````

Dans le répertoire *website* se trouve un répertoire *content* où se trouve l'ensemble des pages et autres articles présents sur le site.
C'est probablement dans ce répertoire que vous allez pouvoir éditer/ajouter vos pages_ ;

Rappel: il faut avoir activé l'environnement virtuel pour produire localement le contenu (``$ source .pelican/bin/activate``) et de préférence avoir mis à jour ses sources (``$ git pull``)
Note: pour désactiver l'environnement virtuel : ``$ deactivate``


Lancement du serveur pour visuliser les modifications
`````````````````````````````````````````````````````
	- Compiler l'ensemble des pages statiques : ``$ make html`` ;
	- Lancer le serveur de test : ``$ make serve`` ;

Le serveur écoute désormais sur le port 8000, il est donc accessible dans un navigateur à l'adresse : http://localhost:8000/ .
Un appui sur la combinaison CTRL+C stoppera l'exécution du serveur.

Propager ses modifications
``````````````````````````

S'assurrer que l'on est dans la branche master du dépot :``$ git checkout master``

Pour propager ses modifications sur le dépôt git :
  - Ajouter les pages modifées/crées: ``$ git add vos-pages-modifiées``
  - Commiter votre travail: ``$ git commit -m"votre commentaire de commit"``
  - Pousser votre travail sur le dépôt: ``$ git push``

.. _pages:

À vous de jouer !
``````````````````

Maintenant que votre environnement est prêt, il va vous falloir comprendre/apprendre le système de gestion et de publication des pages sous Pelican_. Pour ce faire, vous aurez besoin notamment de connaître un des deux langages utilisés pour la création des pages : reStructuredText_ ou Markdown_.

.. _reStructuredText:

Quelques outils pour comprendre et utiliser *reStructuredText* :

    - La `référence simplifiée <http://docutils.sourceforge.net/docs/user/rst/quickref.html>`_ du langage, ou la version `complète <http://docutils.sourceforge.net/rst.html>`_

.. _editeur:

    - Un éditeur de texte qui permet de visualiser du *reStructuredText* :  ReText_ (ou `ici <http://www.webupd8.org/2012/03/retext-30-released-text-editor-for.html>`_)

.. _Markdown:

Et pour le *Markdown* alors ?

    - La `documentation <http://daringfireball.net/projects/markdown>`_ du langage
    - L'editeur_ ReText est également compatible pour la rédaction du Markdown

La publication
``````````````

La publication s'opère en une étape simple :

Mise à jour du rendu sur le site
++++++++++++++++++++++++++++++++

``!updatesite`` dans le canal IRC du `haum <http://irc.lc/freenode/haum>`_


Des liens qui peuvent servir
----------------------------

    - `Markdown Cheatsheet <https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet>`_
    - `Ce que j’aurais aimé savoir quand j’ai commencé GIT <http://software-craftsman.fr/2014/05/12/a-la-decouverte-de-git/>`_


.. [#] Demadez un accès si vous n'en avez pas.

.. _Pelican: http://docs.getpelican.com/en/latest/index.html
.. _ReText: http://sourceforge.net/p/retext/home/ReText
.. _website-content: https://github.com/haum/website-content/
