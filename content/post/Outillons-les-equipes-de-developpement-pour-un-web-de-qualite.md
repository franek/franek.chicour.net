---
date: 2008-11-01T00:42:00+01:00
title: "Outillons les équipes de développement pour un web de qualité"
author: "franek"
aliases: [/post/2008/11/01/Outillons-les-%C3%A9quipes-de-d%C3%A9veloppement-pour-un-web-de-qualit%C3%A93]
tags: ["développement web", "outils", "web"]
lastmod: 2008-11-19T00:42:54+01:00
---
L'organisation d'une équipe de développement passe par la mise en place d'outils. Ces outils ne font pas la qualité d'un projet web mais ils y participent. J'ai sélectionné une dizaine d'outils que je trouve indispensable pour améliorer la qualité d'un projet PHP :

Dans le processus de développement :
------------------------------------

- des normes de développement (convention de codage, norme de paramétrage des outils communs,...)
- [Firefox](http://www.mozilla-europe.org/fr/firefox/), et ses nombreuses extensions - Firebug, Firephp, Webdevelopper Toolbar -,
- [un outil de gestion des versions](http://fr.wikipedia.org/wiki/Syst%C3%A8me_de_gestion_de_versions). Personnellement, j'apprécie Subversion que j'utilise quotidiennement mais je m'intéresse de plus en plus à des outils de [gestion de version décentralisée](http://fr.wikipedia.org/wiki/Gestion_de_version_d%C3%A9centralis%C3%A9e) (Mercurial,...)
- un [outil de suivi de projets de développement](http://en.wikipedia.org/wiki/List_of_project_management_software) (référencement des bugs/évolutions, espace de documentation, statistiques sur le référentiel,...) (exemple : [trac](http://trac.edgewall.org/))
- un framework de développement ou un ensemble de librairies afin de mutualiser les développements. Le [Zend Framework](http://framework.zend.com/) est, à mes yeux, une bonne base car il possède des librairies de qualité qui peuvent être utilisées de manière autonome et qui ne remettent pas nécessairement en cause les développements en cours.
- un framework de développement javascript ([jquery](http://jquery.com/) ?) pour les mêmes raisons.
- Un outil de validation continu (exemple : [phpundercontrol](http://www.phpundercontrol.org/)) afin lancer chaque nuit les process de validation de respect des normes de codage, les tests unitaires, les tests de sécurité,...
- [xdebug](http://xdebug.org/), associé à Kcachegrind, afin d'évaluer la performance des scripts PHP.
- [smush-it](http://www.smushit.com/), afin qu'il soit intégré dans le processus de développement,

Dans le processus de validation :
---------------------------------

- [Y! Slow](http://developer.yahoo.com/yslow/), afin de valider que les bonnes pratiques de performance ont bien été mises en oeuvre,
- [Mon opquast](http://mon.opquast.com/), outil développé par la société Temesis qui permet de valider qu'un projet respecte un ensemble de bonnes pratiques.
