=======
Laumios
=======

:slug: laumios
:projet_realisation: v1 terminée -brightgreen
:projet_etat: fonctionnel -brightgreen

.. image:: /images/bannieres_projets/laumios.1.jpg
	:alt: Laumios

Qu'est ce que c'est ?
=====================

Les Laumios sont des lampes connectées initialement conçues pour le festival
`BienVenus sur Mars`_ qui a eu lieu du 27 avril au 1er mai 2016
(`Photos <https://photos.haum.org/albums/bvsm2016/>`__).
Dans le cadre de cet événément, elles étaient
coordonnées avec un pupitre lui aussi fabriqué pour l'occasion pour former les
`lampes orbitales`_.

Associé à LaumioAnimator_, logiciel développé à l'occasion des `Siestes Teriaki`_ 2016
(`Photos <https://photos.haum.org/albums/teriaki2016/>`__),
il est possible de composer des partitions lumineuses pour accompagner des morceaux musicaux.

Dans un tout autre registre, ces petites boules ont servi dans le cadre des `24h du code`_ 2017
(`Photos <https://photos.haum.org/albums/24hc17/>`__),
qui se sont déroulées cette année là les 21 et 22 janvier, où elles ont servi de `boîte noire... lumineuse`_.

En bref, c'est une lampe connectée à base de leds multicolores (on retrouve du
matériel déjà connu de l'association) et d'un ESP8266, qui est un
microcontrôleur de petite taille et à bas coût pour communiquer en WiFi. Le HAUM
a conçu les Laumios de A à Z, en les accompagnant d'une API pour faciliter leur
communication avec le monde extérieur. Les intérêts sont multiples, allant du
changement sur commande de l'ambiance d'une salle à la création de systèmes
interactifs et/ou ludiques !

Une doc en français est déjà disponible sur readthedocs_, mais la page ici présente en reprend globalement les mêmes lignes.

Les Laumios ont maintenant un `album photo dédié`_ !

.. _lampes orbitales: /pages/lampes-orbitales.html
.. _BienVenus sur Mars: http://www.bienvenus-sur-mars.fr/
.. _readthedocs: http://laumio.readthedocs.io/en/latest/
.. _Siestes Teriaki: http://www.teriaki.fr/
.. _24h du code: http://www.les24hducode.fr/
.. _album photo dédié: https://photos.haum.org/albums/laumio/
.. _boîte noire... lumineuse: /pages/24h-du-code-2017.html

Le Laumio en moins bref
=======================

La structure
------------
Comment faire un Laumio ? On prend un peu d'eau, un peu de mi, et quelques "oh !" qu'on plante ensemble, et on laisse pousser à maturité !

Plus sérieusement, les Laumios actuels (dans la version 1) sont des structures articulées en forme d'arbres que l'on vient insérer dans des lampes de table FADO_ vendues par IKEA. Elles accueillent 4 colonnes de 3 leds ainsi qu'une led tout en haut, pour un total de treize loupiottes.

.. container:: aligncenter

  .. image:: /images/laumios/arbres_laumios.jpg
   :height: 280px
   :alt: Arbres des laumios
  .. image:: /images/laumios/arbre_branchu.jpg
   :height: 280px
   :alt: Arbre branchu des laumios

La structure porteuse se pose à la place de l'ampoule et porte tout l'appareillage nécessaire, en essayant de disposer les leds de manière sphérique. L'articulation des bras permet de replier l'arbre avant de l'insérer dans l'abat-jour sphérique de la lampe, et de le déplier ensuite (il est fortement conseillé de procéder la main dans le sac !).


.. container:: aligncenter

  .. image:: /images/laumios/laumio_sur_socle.jpg
   :height: 280px
   :alt: Laumio sur socle
  .. image:: /images/laumios/laumio_avec_socle.jpg
   :height: 280px
   :alt: Laumio avec socle

Les arbres ont été usinés à l'aide de notre mini-fraiseuse AxiHAUM_ dans des plaques de PVC expansé Komacel_ et l'assemblage a été réalisé par les courageuses petites mains du HAUM ! Les plans sont disponibles `ici <https://github.com/haum/laumio/tree/master/CAD>`__ sur github.

.. container:: aligncenter

  .. image:: /images/laumios/laumio_factory.jpg
     :height: 280px
     :alt: The Laumio Factory


.. _AxiHAUM: /pages/axihaum.html
.. _FADO: http://www.ikea.com/fr/fr/catalog/products/80096372/
.. _Komacel: https://www.sunclear.fr/sunclear/contenu.php?nId=13


L'électronique
--------------
Une fois construit, il faut décorer notre arbre !

Ici, point de guirlandes mais un bandeau de leds découpé... Celui utilisé ici est un WS2812B_ noir, avec 60 leds par mètre. Pour chaque Laumio, 13 leds ont été découpées du bandeau et préparées pour la soudure en déposant une bille d'étain sur chaque borne. Les leds sont ensuite pistocollées sur les branches de la structure et recâblées entre elles.

.. container:: aligncenter

  .. image:: /images/laumios/decoupage_leds.jpg
     :height: 280px
     :alt: Découpage des LEDs
  .. image:: /images/laumios/ledmap_deplie.png
     :height: 280px
     :alt: Schema LEDs


Le shield conçu pour l'occasion (voir le `dépôt correspondant <https://github.com/haum/laumio/tree/master/kicad>`__ ) relie le bandeau de leds à un `WeMos D1 mini`_, en prenant soin d'adapter les tensions d'alimentation et de communication. L'apport en électricité se fait par une alimentation 5V 1.2A.

.. _WS2812B: https://www.adafruit.com/products/1461
.. _WeMos D1 mini: https://www.wemos.cc/product/d1-mini-pro.html


Le code
-------
Dans la suite du programme... place au code !

Pour ce qui est du firmware, le code se "cache" `ici <https://github.com/haum/laumio/tree/master/laumio>`__. Actuellement, l'ESP8266 contenu dans le WeMos D1 mini est programmé en Arduino et utilise la librairie Adafruit_NeoPixel pour contrôler le bandeau de leds. Le Laumio réagit pour l'instant à l'envoi de paquets UDP et de requêtes HTTP.

L'API pour la communication UDP est disponible sur readthedocs_, avec des exemples de scripts en  langages Python et Bash.


Evolution du projet
===================
Une structure mécanique plus souple
-----------------------------------
Parmi les différents essais de structure qui ont pu être menés, une idée qui a pu sortir du lot est d'utiliser des arcs déformables sur lesquels placer les leds plutôt que d'utiliser des branches articulées. En l'occurrence, les soudures supportent assez mal les pliages et dépliages répétés et peuvent casser (gymnastique déconseillée pour les pauvres petites, donc...).


.. container:: aligncenter

  .. image:: /images/laumios/arbre_du_turfu.jpg
   :height: 280px
   :alt: Arbre futur


La pioche à idées
-----------------
Des idées, il y en a toujours à revendre... ou à laisser gratuitement à disposition. En voici quelques-unes pour qui voudrait aider sur les Laumios mais ne saurait pas quoi faire !

- **Plus de leds !** Concevoir une nouvelle structure pouvant porter jusqu'à 8 colonnes de 5 leds en plus des leds supérieures, en prévoyant l'alimentation adéquate. Faire en sorte que l'on puisse utiliser ces Laumios comme s'ils n'avaient que 13 leds pour des questions de rétrocompatibilité.
- **Plus de performance !** Recoder le firmware en se passant des libairies Arduino pour augmenter la réactivité de la lampe. Améliorer la structure pour en faciliter l'insertion et le maintien dans l'abat-jour. Améliorer les connectiques.
- **Plus d'interopérabilité !** Créer un logiciel passerelle pour adapter les Laumios aux différents standards que l'on retrouve dans le monde du spectacle.
- **Plus de Laumios !** Parce qu'on n'en a jamais assez.
- **Plus de simplicité !** Forker LaumioAnimator_ pour le rendre utilisable sur ordiphone et pour répondre à des besoins simples.
- **Plus de configurabilité !** Faire en sorte que Madame Michu n'ait pas à trifouiller le code pour que la lampe se connecte à son réseau.

.. _LaumioAnimator: /pages/laumio-animator.html

