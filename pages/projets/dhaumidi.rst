========
dHAUMidi
========

:slug: dhaumidi

:projet_realisation: terminé-brightgreen
:projet_etat: fonctionnel-brightgreen

Qu'est ce que c'est?
====================

Il s'agit d'un dôme musical fabriqué à partir du dhaum_ dont les visiteurs écrivent la partition.

Moult objets sont dispercés à l'intérieur et à l'extérieur de la structure géodésique.
Les visiteurs, en formant des chaînes humaines (ou pas), peuvent relier ces objets et
ainsi produire des réactions sonores ou lumineuses.

Ce projet a été initié pour l'édition 2015 du festival Teriaki.

Techniquement ?
===============

Structure
---------

Voir la page du dhaum_

Électronique
------------

Le dHAUMidi est construit avec la carte léoké_.

Chaque objet est relié à une broche du contrôleur.
Un programme spécialement écrit pour le projet fait passer de l'électricité (un peu) dans le
corps des gens et détecte sur quelles broches celle-ci revient.
Il associe alors une note midi iterprétée alors par le logiciel.

Logiciel
--------

À l'heure d'écrire ces lignes, le logiciel est indéfini

.. _dhaum: /pages/dhaum.html
.. _léoké: http://leoke.desbwa.org/
