---
date: 2013-02-11T21:01:00+01:00
title: "Exporter une page web avec l'ensemble des assets (CSS, JS, images)"
author: ["franek"]
aliases: [/post/2013/02/21/Exporter-une-page-web-avec-l-ensemble-des-assets-%28CSS%2C-JS%2C-images%29]
tags: ["geek", "export", "html", "wget"]
lastmod: 2013-02-21T21:09:49+01:00
---
Aide mémoire...

Si vous cherchez à exporter une seule page web avec l'ensemble des assets (CSS, JS, images), le script suivant devrait répondre à votre besoin :

```

$ wget -p --html-extension -k <url>
```

- -p, --page-requisites : obtenir toutes les images, etc. nécessaires à l'affichage de la page HTML.
- -k, --convert-links : fait pointer les liens dans le HTML/CSS téléchargé vers des fichiers locaux.
- --html-extension : pour ajouter l'extenion .html à vos fichiers

Par exemple, pour exporter une page de votre application en développement et la transmettre à un développeur front-end n'ayant pas accès à votre environnement :

```

$ wget -p --html-extension -k http://machine.dev.local/vers/ma/super/page
```

Et si vous souhaitez récupérer cette page en étant connecté à l'application, vous pouvez passer un fichier de cookies (cookies.txt) :

```

$ wget --load-cookies cookies.txt  -p --html-extension \
   -k http://machine.dev.local/vers/ma/super/page
```

Il y a sûrement moyen de faire la même chose avec curl.
