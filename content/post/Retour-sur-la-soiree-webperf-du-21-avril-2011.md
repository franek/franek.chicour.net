---
date: 2011-04-22T12:13:00+02:00
title: "Retour sur la soirée #webperf du 21 avril 2011"
author: "franek"
aliases: [/post/2011/04/22/Retour-sur-la-soir%C3%A9e-webperf-du-21-avril-2011]
tags: ["développement web", "atelier", "performance", "web", "webperf", "webperf user group"]
lastmod: 2011-10-23T17:00:15+02:00
---
J'ai assisté hier, pour la seconde fois, à l'atelier webperf organisé par le [Webperf User Group](https://sites.google.com/a/survol.fr/webperf-user-group) et principalement [Eric](http://eric.daspet.name "Site perso de Eric Daspet").

L'objectif de la soirée était d'analyser quelques sites en 30 minutes par groupe de 5 à 10 personnes puis d'échanger sur les analyses effectuées et sur les solutions possibles pour améliorer la performance (navigateur, réseaux) du site.

Nous avons bien sûr évoqués

- les outils habituels : 
  - YSlow!
  - Webpagetest

- et les méthodes classiques d'optimisation : 
  - réduction du nombre de requêtes
  - concaténation des fichiers JS/CSS
  - gestion des expirations des contenus
  - compression des contenus envoyés au navigateur (gzip &amp; co)
  - sprite des images CSS
  - ...

L'intérêt de la soirée résidait dans les astuces proposées qui étaient directement applicables aux sites audités. J'en ai relevé quelques unes. Certaines pourraient être généralisées à vos projets :

- Une bonne pratique pourrait être d'ajouter dès aujourd'hui dans le code HTML les balises &lt;link rel="prefetch" afin d'indiquer au navigateur de "préfetcher" certains éléments (exemple : requête DNS, ...). Tous les navigateurs ne supportent pas cette fonctionnalité. Quelques articles pour développer le sujet : 
  - [DNS Prefecth par Eric Daspet](http://davidwalsh.name/html5-prefetch "DNS Prefect")
  - [HTML5 Link Prefetch par David Walsh](http://davidwalsh.name/html5-prefetch)
- Le chargement des feuilles de styles d'impression (media=print) peut "ralentir" le chargement d'une page (ajout d'une requête) alors que dans la plupart des cas, elle n'est pas nécessaire dans le contexte de navigation. Une bonne pratique pourrait être : 
  - soit de charger les styles spécifiques via @media
  - soit de la charger via JS (en mode asynchrone)
- Suite au commentaire de Vincent Voyer, attention de ne pas charger la feuille de styles CSS print en fin de document (<q>sinon, les navigateurs comme IE6 et 7 n'afficheront rien tant que tous les CSS ne seront pas téléchargés.</q>)
- Si vous utilisez les commentaires conditionnels, il est nécessaire d'ajouter avant le HEAD un commentaire conditionnel vide. Sinon, IE bloque le téléchargement parallèle pendant le chargement de la première CSS (voir les commentaires pour les ressources permettant de valider ce problème). Voir le site de 20minutes.fr qui met en pratique cette technique
- Du fait, du faible nombre de téléchargement parallèle sous IE, il est préférable d'ajouter une classe IE sur le &lt;body&gt; (voire &lt;html&gt; comme le propose Nicolas Hoizey dans les commentaires) et cibler les styles IE via cette classe plutôt que d'avoir un fichier CSS dédié (hack-ie-6.css). On dispose ainsi que d'un seul fichier CSS pour l'ensemble des navigateurs.
- Google Analytics propose deux modes (synchrone, asynchrone). Il est préférable d'utiliser la version asynchrone (dernière version disponible).
- Afin d'éviter que le cookie de Google Analytics soient positionnés sur l'ensemble des sous-domaines, il est possible de lui dire de le positionner que sur un seul domaine en particulier via \_gaq.push(\['\_setDomainName', 'mondomaine'\]), je pense
- Pour des images inférieures à 100x150, il est souvent préférable de passer en PNG8 plutôt qu'en JPEG. La dégradation de la qualité de l'image ne sera pas perçue (ressource nécessaire pour valider ce point).

Enfin, quelques outils que je ne connaissais pas

- Pour les performances sur mobiles : 
  - [blaze.io](http://www.blaze.io/ "Blaze IO") : équivalent webpagetest pour Mobile mais les résultats ne sont pas toujours très pertinents
  - [5o9inc.com](http://www.5o9inc.com/) propose un APK à installer sur un téléphone Androïd afin de collecter des informations sur les performances du site mobile.
- Pour l'analyse : 
  - [speedtracer](http://code.google.com/intl/fr/webtoolkit/speedtracer/) : pour suivre le traitement du chargement d'un site dans le navigateur (traitement du javascript, reflow, analyse CSS,...). C'est une extension pour Google Chrome ou Chromium.
- Pour le chargement des fichiers JS 
  - [requirejs](http://requirejs.org/) : équivalent à headJS, ...

C'est tout pour le moment.

Edit : Correction suite différents commentaires.
