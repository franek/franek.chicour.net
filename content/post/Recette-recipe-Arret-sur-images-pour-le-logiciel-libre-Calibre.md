---
date: 2013-03-30T19:16:00+01:00
title: "Recette (/recipe) \"Arrêt sur images\" pour le logiciel libre Calibre"
author: ["franek"]
aliases: [/post/2013/03/30/Recette-%28/recipe%29-Arr%C3%AAt-sur-images-pour-le-logiciel-libre-Calibre]
tags: ["geek", "arrêt sur images", "calibre", "ebook", "liseuse", "news"]
lastmod: 2014-01-06T21:55:26+01:00
---
Je suis abonné [Arrêt sur images](http://www.arretsurimages.net/), un site de news français réalisant un décryptage de l'actualité des médias et également possesseur d'une liseuse (e-book), Sony PRS-T1. Cette liseuse me permet de lire les contenus de différents sites hors ligne.

Pour synchroniser les contenus de différentes sites ([Instapaper](http://www.instapaper.com/), Le Monde, Médiapart, ....), j'utilise un logiciel libre [Calibre](http://calibre-ebook.com/). Calibre propose un système d'extension (Recette / recipe) permettant d'étendre le logiciel et d'ajouter la synchronisation de sites n'étant actuellement pas gérés.

Bien que la plupart des contenus proposés par le site Arrêt sur Images soient des vidéos, certains sont des contenus textuels (chroniques, vite-dit, ...) de qualité inégale (mais parfois intéressant). Je cherchais depuis longtemps une solution permettant de synchroniser ces contenus sur ma liseuse afin de pouvoir les lire dans les transports en commun.

J'ai donc développé rapidement une recette permettant d'extraire le contenu de quelques catégories ([vite dit et gratuit](http://www.arretsurimages.net/vite-dit.php), [Toutes les chroniques](http://www.arretsurimages.net/chroniques.php), [dossiers de la rédaction](http://www.arretsurimages.net/tous-les-dossiers.php)), de générer un epub et de les synchroniser avec ma liseuse (il est nécessaire de préciser son login et son mot de passe pour récupérer le contenu réservé aux abonnés). Cette recette n'est sûrement pas parfaite mais semble fonctionner.

Le code source est disponible sur [Github](https://github.com/franek/calibre-recipe-arret-sur-images/) si vous souhaitez l'enrichir. Les Pull Requests sont les bienvenus...

En espérant que cette recette pourra être utile à d'autres...
