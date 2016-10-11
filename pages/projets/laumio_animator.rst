==============
LaumioAnimator
==============

:slug: laumio-animator
:projet_realisation: à continuer -yellow
:projet_etat: fonctionnel -brightgreen

.. image:: /images/bannieres_projets/laumio-animator.1.jpg
	:alt: LaumioAnimator


Qu'est ce que c'est ?
=====================
LaumioAnimator, c'est un compositeur de partitions lumineuses développé en Qt/C++, pour accorder les laumios_ avec un morceau de musique. Ses sources sont disponibles sur le `dépôt Git dédié`_. Il a été brièvement utilisé pendant les `Siestes Teriaki`_ 2016.

.. _Laumios: /pages/laumios.html
.. _Siestes Teriaki: http://www.teriaki.fr/
.. _dépôt Git dédié: https://github.com/haum/laumio_animator/


LaumioAnimator en moins bref
============================
Le moteur d'animation
---------------------

Les animations
--------------
Les animations disponibles sont les suivantes :

- **Animation constante *ConstantColor* :**

- **Animation progressive *ProgressiveColor* :**

- **Animation pulsatile *PulsingColor* :** 

- **Animation pulsatile bornée *BoundedPulsingColor* :**


L'interface
-----------
La preview
~~~~~~~~~~

.. container:: aligncenter

  .. image:: /images/laumioAnimator/laumioAnimator_preview.jpg
     :height: 360px
     :alt: LaumioAnimator "preview" tab

La map
~~~~~~

.. container:: aligncenter

  .. image:: /images/laumioAnimator/laumioAnimator_map.jpg
     :height: 360px
     :alt: LaumioAnimator "map" tab


La timeline
~~~~~~~~~~~

.. container:: aligncenter

  .. image:: /images/laumioAnimator/laumioAnimator_timeline.jpg
     :height: 360px
     :alt: LaumioAnimator "timeline" tab


Le JSON
~~~~~~~
Le logiciel est capable de charger ou d'enregistrer des compositions via un fichier JSON. Le chemin vers une source audio eut aussi être ajouté manuellement fans le JSON.
La structure générale du fichier généré est la suivante (avec l'exemple d'une seule animation constante noire de 2,5 secondes pour un laumio lambda) :

.. code-block:: javascript

  {
      "animations": [
          {
              "anims": [
                  {
                      "color": "#000000",
                      "duration": 2.5,
                      "fromStart": 0.0,
                      "priority": 5,
                      "type": "ConstantColor"
                  },
                  ...
              ],
              "laumio": {
                  "ip": "192.168.0.1",
                  "name": "Laumio",
                  "port": 6969,
                  "x": 0,
                  "y": 0.25
              }
          },
          ...
      ],
      "audioSource": "file:///tmp/audioSource.wav"
  }



Evolution du projet
===================
Les signaux
-----------

La pioche à idées
-----------------
Des idées, il y en a toujours à revendre... ou à laisser gratuitement à disposition. En voici quelques-unes pour qui voudrait aider sur LaumioAnimator mais ne saurait pas quoi faire !

- **Plus de facilité !** Ajouter une fonctionnalité de recherche de laumios connectés au réseau.
- **Plus de mémoire !** Ajouter une fonctionnlité d'enregistrement de la map avec les infos des Laumios.
- **Plus de simplicité !** Forker LaumioAnimator_ pour le rendre utilisable sur ordiphone et pour répondre à des besoins simples. 
- **Plus de complexité !** Gérer les animations des laumios led par led et non pas en remplissage intégral.

.. _LaumioAnimator: /pages/laumio-animator.html

