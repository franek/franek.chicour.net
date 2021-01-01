---
date: 2011-11-27T09:48:00+01:00
title: "Retour sur le #phptour de Lille"
author: "franek"
aliases: [/post/2011/11/27/Retour-sur-le-phptour-de-Lille]
tags: ["développement web", "afup", "lille", "php", "phptour"]
lastmod: 2011-12-23T15:53:40+01:00
---
J'ai participé au [\#phptour](http://afup.org/pages/phptourlille2011/), un nouvel événement itinérant autour de la technologie PHP proposé par l'[AFUP](http://afup.org). Cette année, cet événement avait lieu à Lille. Pour l'année prochaine, on évoque Nantes, Lyon ou Bordeaux. Le Forum PHP est quant à lui décalé et aura désormais lieu en juin.

Voici quelques notes prises concernant les conférences auxquelles j'ai assistées.

Présentation de PHP5.4 par Julien Pauli (en remplacement de David Soria Parra qui ne pouvait être présent)
----------------------------------------------------------------------------------------------------------

Julien a fait un rapide état des lieux autour de la future version de PHP :

- Le mode de contribution avec PHP5.4 évolue. Il est désormais obligatoire de passer par une [RFC](https://wiki.php.net/rfc).
- Le mode de publication évolue également à partir de la version 5.4 en se rapprochant d'un système de publication à la Ubuntu. Une version mineure sera publiée chaque année. Chaque version aura une durée de vie de 3 ans. Seules les versions majeures pourront casser la compatibilité. Le nouveau mode de publication est détaillée sur le [wiki de php](https://wiki.php.net/rfc/releaseprocess).
- Le dépôt des sources de PHP va migrer de subversion à git (a priori, à Noël). Les sources seront disponibles sur les serveurs de PHP.net (mais également sur github, miroir).
- Le principale apport de PHP5.4 est sa performance. PHP5.4 sera environ 50% plus rapide (d'après les quelques benchs réalisés, tout dépend de votre application)
- PHP5.4 supprime des vieilleries (notamment, register\_globals, magic\_quotes, session\_register(),...)
- E\_ALL contiendra désormais E\_STRICT.
- La syntaxe &lt;?= n'est plus dépendante de la configuration short\_open\_tags.
- PHP5.4 propose un serveur web embarqué afin de simplifier le développement mais qui ne doit pas être utilisé en production !!
- PHP5.4 propose ensuite des nouvelles fonctionnalités au niveau du langage : 
  - Le nouveau type Callable qui permet de décrire un callback dans une fonction (voir la [RFC pour plus d'explications](https://wiki.php.net/rfc/callable))
  - Une [nouvelle syntaxe pour les tableaux](https://wiki.php.net/rfc/shortsyntaxforarrays)
  - Array derefencing
  - Les [traits](https://wiki.php.net/rfc/traits)
  - et enfin les [closures](https://wiki.php.net/rfc/closures)

Les slides de la conférences sont disponibles sur [slideshare](http://www.slideshare.net/jpauli/phptour-2011php54).

Industrialisation PHP chez lamaisondevalerie par Sophie Beaupuis
----------------------------------------------------------------

Sophie travaille historiquement chez lamaisondevalerie.fr. Lamaisondevalerie a été racheté par Conforama afin de développer l'offre e-commerce de conforama. Sophie nous a présenté les méthodes et outils mis en oeuvre pour la réécriture de la solution e-commerce de Conforama :

- choix d'une solution basée sur le Zend Framework en remplacement de Websphere e-commerce
- recrutement d'une équipe de développement (non sans difficultés apparemment)
- passage à une méthodologie agile. Elle essaye de se rapprocher de plus en plus de la méthodologie Scrum.
- chaque matin, réunion de 20 minutes pour faire un bilan sur les dev réalisés la veille et sur la planification des dev de la journée.
- mise en place de bonnes pratiques : 
  - mise en place de convention de codage
  - mise en place de tests unitaires
- Passage à git, comme gestion des sources. Le passage à git a nécessité de créer des rôles de Source Manager. 2 personnes sont responsables des fusions des branches chaque soir.
- mise en place d'une plate-forme d'intégration continue (PHPUnderControl, pour le moment)

Suggestion dans la salle :

- [icescrum](http://www.icescrum.org/) pour gérer les backlogs

Les [slides](http://afup.org/templates/phptourlille2011/resumes/526-la_maison_de_valerie.pdf) sont disponible sur le site de l'AFUP.

Retour d'expérience sur XHProf par Martin Supiot
------------------------------------------------

Martin nous a présenté son retour d'expérience sur XHProf un outil de profilage de PHP développé par Facebook qui mériterait d'être plus connu. Cet outil n'est pas très gourmand et peut-être installé en production. Il est possible de configurer XHProf afin qu'il exécute le profilage par échantillonnage (une requête sur 10000, par exemple).

En attendant les slides, je vous renvoie sur un [article que j'avais écrit qui reprend une partie des slides de Martin](https://franek.chicour.net/post/2011/04/15/Installer-xhprof-et-xhprof-gui-sur-Zend-Server).

Dommage que Martin n'ait pas parlé des alternatives au profilage en production (pas en dev), notamment, [Newrelic](http://newrelic.com/) (solution dans le cloud) qui est vraiment intéressante mais un peu chère.

Edit : Les [slides sont disponibles sur le blog de Martin](http://www.webaaz.com/2011/11/profilage-avec-xhprof-xhgui/ "Slides conférence de Martin Supiot").

Services asynchrones &amp; multilangages avec Mongrel2 et ZeroMQ par Loïc d'Anterroches
---------------------------------------------------------------------------------------

(A venir)

phpcloud.com : Be a PHP Hero! par Zeev Suraski
----------------------------------------------

Zeev nous a présenté la nouvelle offre de Zend [PHPCloud](http://www.phpcloud.com/) qui permet de déployer facilement une application dans un cloud proposé par Zend. La solution est encore en beta. PHPCloud intègre toutes les fonctionnalités de Zend Server (profilage, cache d'opcode, évènements, ...).

Les CMS basés sur framework en environnement profressionnel par Mathias Desloges et Raphaël Theet
-------------------------------------------------------------------------------------------------

Mathias et Raphaël travaillent chez Octave&amp;Octave. Ils nous ont présenté leur solution de CMF (Content Management Framework), [Centurion](http://centurion-project.org/). Centurion est basé sur le Zend Framework (version 1.X, il n'est pas prévu de migrer en 2.X pour le moment). Centurion propose un ensemble de mécanisme permettant de simplifier le développement d'un site e-commerce.

Atoum, framework de tests unitaires pour PHP5.3+ par Frédéric Hardy
-------------------------------------------------------------------

Frédéric Hardy nous a présenté son [nouveau framework de tests unitaires](https://github.com/mageekguy/atoum/). Excellente présentation qui donne envie de le tester. Atoum est désormais un excellent challenger à PHPUnit. La concurrence a, en général, du bon.

Drupal et Varnish, une histoire qui marche par Nicolas Silberman
----------------------------------------------------------------

Nicolas nous a fait un retour d'expérience sur l'intégration de Varnish en frontal de Drupal. Il a largement utilisé les [VCL](https://www.varnish-cache.org/docs/3.0/reference/vcl.html) ainsi que les [ESI](http://en.wikipedia.org/wiki/Edge_Side_Includes) (Edge Side Includes). Les ESI permettent de mettre en cache un bloc de page et sont interprétées par Varnish. Depuis la version 2 de Symfony, il est possible de les intégrer facilement dans un développement à [base de Symfony](http://symfony.com/doc/2.0/book/http_cache.html#using-edge-side-includes).

Etes-vous prêts pour le succès par Steven Van Poeck
---------------------------------------------------

Steven nous a présenté une méthodologie pour faire évoluer une architecture en fonction du nombre de visiteurs. Je n'ai pas toujours été d'accord avec ses choix (notamment, sur la désactivation des logs Acces\_log sur les frontaux) mais globalement, assez d'accord.

Les slides de sa présentation sont disponibles sur [Slideshare](http://www.slideshare.net/svanpoeck/etes-vouspretspourlesucces2011-10320332).

Suivi qualité avec Sonar pour PHP par Gabriele Santini
------------------------------------------------------

Gabriel nous a présenté Sonar pour PHP. Sonar ne doit pas être comparée à une PIC (Plate-forme d'Intégration Continue) comme Jenkins. Sonar est un logiciel libre permettant de mesurer la qualité du code source des projets de développement. Depuis peu, Sonar propose un plugin pour PHP. Il vient en complément de Jenkins. Pour Gabriele, les conventions de codage (via PHP\_Code\_Sniffer), la complexité du code (via PHPMD), ... ne doivent pas être vérifiées dans la PIC mais dans Sonar. Il existe un plugin permettant d'intégrer Sonar dans Jenkins.

Améliorez votre productivité avec Symfony2 par Hugo Hamon
---------------------------------------------------------

Rapide présentation de Hugo sur les nouvelles fonctionnalités de Symfony2. Je ne suis personnellement pas fan des annotations mais c'est avis totalement personnel. Cette présentation donne envie d'aller plus loin. Le système de génération de l'admin, l'héritage dans Twig ou la gestion des caches (Reverse Proxy) semblent vraiment bien intégrées.

Sécurité des applications PHP par Marion Agé et Sébastien Baudru
----------------------------------------------------------------

Rien de neuf dans cette présentation sur la sécurité mais la mise en scène était excellente.

Zend Framework2 : State of the art par Enrico Zimuel
----------------------------------------------------

Enrico nous a présenté les nouvelles fonctionnalités de ZF2.

Sortie prévue de ZF2 : pas avant avril 2012 si j'ai bien noté.

Dev et admin sys : une cohabitation simplifiée par Nicolas Silberman et Sébastien Lucas
---------------------------------------------------------------------------------------

J'ai loupé le début de la conférence. Nicolas et Sébastien ont plutôt présenté la culture [devops](http://devops.fr/) qui visent à rapprocher les équipes de dev avec les admin sys. J'ai bien aimé le tableau de présentation des outils à partager entre les équipes de dev et les équipes d'admin.

Magento - intégration continue, tests et automatisation par Alexande Salomé
---------------------------------------------------------------------------

Enfin, pour terminer, une bonne conférence sur la mise en place de l'intégration continue sur un projet. Alexandre a pris comme exemple Magento mais ça méthode pourrait s'appliquer à n'importe quel projet.

Les slides de sa conférence sur [SpeackerDeck](http://speakerdeck.com/u/alexandresalome/p/magento-integration-continue-tests-automatisation).
