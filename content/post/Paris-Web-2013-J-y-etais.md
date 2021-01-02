---
date: 2013-10-19T11:44:00+02:00
title: "Paris Web 2013 : J'y étais !"
author: ["franek"]
aliases: [/post/2013/10/19/Paris-Web-2013-%3A-J-y-%C3%A9tais]
tags: ["développement web", "2013", "accessibilité", "conférence", "paris", "paris web", "qualité", "web"]
lastmod: 2013-10-19T23:16:16+02:00
---
Après 2 années d'absence aux conférences de [Paris Web](http://www.paris-web.fr) (mais pas les ateliers), j'ai à nouveau participé aux conférences Paris Web (merci à mon employeur).

Comme d'habitude, j'ai trouvé que la journée du samedi (les ateliers) était indispensable : les intervenant prennent le temps de rentrer dans le détail des sujets et les petites salles sont propices aux échanges. Je regrette de ne pas disposer d'un don d'ubiquité.

La qualité des conférences des journées du jeudi et vendredi était inégale. Je ne ferai pas de compte-rendu complet, certains sont bien meilleurs que moi pour cet exercice. J'ai appris ou découvert quelques petites choses lors de ces 3 jours que je vais essayer de partager avec vous.

[Steve Faulkner](http://www.paris-web.fr/orateurs/steve-faulkner.php) nous a parlé de [HTML5 Accessibility](http://www.paris-web.fr/2013/conferences/html5-accessibility.php). J'ai bien aimé sa conférence. Les spécialistes de l'accessibilité n'ont sûrement pas appris grand chose. J'ai aimé l'anecdote sur la page d'accueil de Google qui utilise encore des balises &lt;table&gt; ou &lt;font&gt; pour le layout de sa page. On se dit qu'il y a encore du travail à faire pour l'accessibilité. Vous pouvez retrouver les [slides de la conférence de Steve Faulkner](http://weba.im/parisweb).

[Jean-Philippe Encausse](http://www.paris-web.fr/orateurs/jean-philippe-encausse.php) nous a [parlé](http://encausse.wordpress.com/2013/10/13/parisweb-2013-retours-sur-ma-presentation-de-sarah/) de la solution qu'il développe pour faire communiquer des objets intelligents, [S.A.R.A.H](http://encausse.wordpress.com/s-a-r-a-h/). Sa solution semble vraiment intéressante, elle s'appuie sur des briques ouvertes pour interroger les API des objets connectés (TV, domotique, ... ) qui, elles, sont souvent fermées. Son outil m'a fait penser à [Weboob](http://weboob.org/) mais pour les objets connectés. Durant son intervention, il nous a conseillé de tester le jeu de réalité augmentée développé par Google, [Ingress](http://www.ingress.com/).

[Stéphane Bortzmeyer](http://www.paris-web.fr/orateurs/stephane-bortzmeyer.php) que l'on ne présente plus nous a parlé de la sécurité et principalement de la sécurité autour des DNS. J'ai appris plein de petites choses que vous pouvez retrouver dans [ses slides](http://www.bortzmeyer.org/static/Securite@ParisWeb/﻿﻿ "Les slides de Stéphane Bortzmeyer à Paris Web"). J'aurais souhaité qu'il approfondisse un peu plus le sujet mais ce n'était sûrement pas le lieu. Par contre, vous pouvez le retrouver à [Pas Sage en Seine 2012](http://seenthis.net/messages/86234) ou ailleurs. Il nous a conseillé de lire :

- [Rapport annuel sur la résilience de l'Internet en France](http://www.ssi.gouv.fr/fr/menu/actualites/l-observatoire-sur-la-resilience-de-l-internet-francais-publie-son-rapport-2012.html)
- [Sécurité des noms de domaine (AFNIC - 4 juillet 2012)](http://fr.slideshare.net/AFNIC/tutoriel-afnic-par-stphane-bortzmeyer-securitnomsdomaines20120704)

[Amaëlle Guitton](http://www.paris-web.fr/orateurs/amaelle-guiton.php) a synthétisé son livre [Hackers: Au cœur de la résistance numérique](http://www.decitre.fr/livres/hackers-9782846265010.html) lors d'une [conférence](http://www.techn0polis.net/2013/10/13/paris-web-2013/). Ayant lu son livre, j'ai apprécié qu'elle détaille de vives voix ses écrits. Bien que persuadé de l'importance des sujets abordés par Amaëlle, je suis partagé sur la place de ce genre de conférences à Paris Web. Elle nous a notamment conseillé de (re-)lire :

- ["Je vous ai menti" de Laurent Chemla](http://reflets.info/laurent-chemla-je-vous-ai-menti/)
- ["L'éthique des hackers"](http://www.editions-globe.fr/project/lethique-des-hackers/) dont la traduction française vient d'être publiée en France.

Et d'utiliser les outils suivants :

- [Cryptocat](https://crypto.cat/), un chat crypté
- [mailpile](http://www.mailpile.is/), un webmail open-source se rapprochant de Gmail dans ses fonctionnalités

L'une des conférences où j'ai le plus appris est la conférence de [Christopher Schmitt](http://www.paris-web.fr/orateurs/christopher-schmitt.php) sur les différentes techniques permettant de rendre des images [adaptables au Responsive Design](http://fr.slideshare.net/teleject/parisweb-adaptive-images-in-responsive-web-design). J'ai noté quelques liens intéressants :

- [UserAgentStrings](http://www.useragentstring.com/pages/useragentstring.php), un site qui regroupe l'ensemble des valeurs des User-Agents des navigateurs (et/ou robots).
- [adaptative-images.com](http://adaptive-images.com), est une solution côté serveur (script PHP et configuration Apache) permettant de servir l'image adaptée selon la résolution de l'utilisateur
- [HiSrc](https://github.com/teleject/hisrc), un plugin jQuery réalisant le même type d'opération
- [CSS-Tricks : Which responsive images solution should you use ?](http://css-tricks.com/which-responsive-images-solution-should-you-use/)
- [FittextJS](http://fittextjs.com/)
- [Icon Fonts are awesome](http://css-tricks.com/examples/IconFont/)
- [Fontello](http://fontello.com/), un générateur d'icon-fonts
- [IcoMoon](http://icomoon.io/)
- [Clown Car Technique: Solving Adaptive Images In Responsive Web Design](http://coding.smashingmagazine.com/2013/06/02/clown-car-technique-solving-for-adaptive-images-in-responsive-web-design/)

[Florian Le Goff](http://www.paris-web.fr/orateurs/florian-le-goff.php) nous a présenté [Boucles de rétroactions, ou comment personnaliser vos applications](http://www.paris-web.fr/2013/conferences/boucles-de-retroactions-ou-comment-personnaliser-vos-applications.php). J'ai noté quelques liens intéressants (voir ses [slides](https://speakerdeck.com/madflo/retroaction-premieres-etapes-vers-lautomatisation)) :

- [Apache Mahout](http://mahout.apache.org/) : librairie permettant de faire de la prédiction à partir de données (clients, utilisateurs), version libre
- [Google Prediction API ](https://developers.google.com/prediction/?hl=fr) : la même chose mais non libre
- [mixpanel](https://mixpanel.com/)
- [KissMetrics](https://www.kissmetrics.com/)

[Olivier Thereaux](http://www.paris-web.fr/orateurs/olivier-thereaux.php) et [Karl Dubost](http://www.paris-web.fr/orateurs/karl-dubost.php) nous ont présenté [Esthétique et pratique du Web qui rouille](http://www.paris-web.fr/2013/conferences/esthetique-et-pratique-du-web-qui-rouille.php). Une bien [belle conférence](https://github.com/olivierthereaux/rustyweb) sur la gestion de l'information, de l'archivage,... à l'heure du web.

[Geoffrey Dorne](http://www.paris-web.fr/orateurs/geoffrey-dorne.php) nous a parlé de [Multimodalité &amp; interfaces. Le design est une question d'humains, pas de machine](http://www.paris-web.fr/2013/conferences/multimodalite-des-interfaces-web-une-nouvelle-approche-du-design.php). Je vous conseille de regarder la vidéo lorsqu'elle sera disponible (ses [slides](http://fr.slideshare.net/geoffreydorne/salon-d-honneurvendredi15h05multimodaliteetinterfacesdesignquestiondhumainspasdemachine-27072507)). A nouveau quelques liens glanés :

- [Outlisten](http://www.outlisten.com/)
- [Flutter](https://flutterapp.com/)
- [diplomatic-cover](http://www.diplomatic-cover.com/fr)
- [Little Printer](http://bergcloud.com/littleprinter/)
- [Plex.io](http://plex.io/)

La première conférence que j'ai suivi lors des ateliers fut celle de [Goulven Champenois](http://www.paris-web.fr/orateurs/goulven-champenois.php) sur [Responsive, l’indispensable révolution des outils et processus](http://www.paris-web.fr/2013/ateliers/). L'atelier s'est vite transformé en discussion autour du Responsive Design avec de bons échanges avec Jérémie Pattonnier.

- [styletil.es](http://styletil.es/), guide de styles / planches de composant
- [This is the web par Brad Frost](http://bradfrostweb.com/blog/post/this-is-the-web/)

J'ai ensuite suivi l'excellente conférence de [Raphaël Rougeron](http://www.paris-web.fr/orateurs/raphael-rougeron.php) sur les [tests unitaires en Javascript](http://www.paris-web.fr/2013/ateliers/tester-son-js-cest-possible.php). Pour résumer sa [conférence](http://fr.slideshare.net/goldoraf/tester-son-js) en quelques mots, il a nous conseillé d'utiliser :

- [mocha](http://visionmedia.github.io/mocha/) : librairie de tests
- [sinon.js](http://sinonjs.org/) : librairie pour gérer les mocks et les stubs
- [chais.js](http://chaijs.com/) : librairie de gestion des assertions
- [karma](http://karma-runner.github.io/) : runner des tests (exécution des tests dans les différents navigateurs)

Dans l'assistance, [Sentry](https://getsentry.com) a été recommandé pour faire de la supervision orientée front et [Gatling](http://gatling-tool.org/) pour faire des tests de charge.

J'ai continué sur un excellent atelier de [Thomas Basseto](http://www.paris-web.fr/orateurs/thomas-bassetto.php) sur [Les outils pour développeurs inclus dans les navigateurs Web](http://www.paris-web.fr/2013/ateliers/les-outils-pour-developpeurs-inclus-dans-les-navigateurs-web.php).

Enfin, j'ai terminé par l'atelier de [Arnaud Limbourg](http://www.paris-web.fr/orateurs/arnaud-limbourg.php) et [son retour d'expérience](https://speakerdeck.com/arnaudlimbourg/monitoring-mise-en-place) dans l'utilisation d'outils de monitoring dont on parle beaucoup :

- [elasticsearch](http://www.elasticsearch.org/)/[kibana](http://www.elasticsearch.org/overview/kibana/)
- [graphite](http://graphite.wikidot.com/)
- [StatsD](https://github.com/etsy/statsd/)

A l'année prochaine ?

P.S: J'ai oublié de remercier toute l'équipe de Paris Web pour le travail réalisé. N'oublions pas de dire que les organisateurs comme les orateurs sont tous bénévoles !!
