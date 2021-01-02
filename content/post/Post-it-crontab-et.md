---
date: 2012-01-04T20:59:00+01:00
title: "Post-it : crontab et %"
author: ["franek"]
aliases: [/post/2012/01/04/Post-it-%3A-crontab-et]
tags: ["geek", "astuce", "crontab", "linux", "post-it", "sysadmin", "échappement"]
lastmod: 2012-01-04T21:06:02+01:00
---
Une petite astuce concernant crontab que je ne connaissais pas (on apprend tous les jours).

Les caractères % doivent être échappés dans crontab.

Le crontab suivant :

```

00 19 * * * /chemin/vers/mon/script.sh >/chemin/vers/output-`date +%Y%m%d`.log
```

ne fonctionnait pas.

J'obtenais une erreur du type :

```

/bin/sh: Syntax error: EOF in backquote substitution
```

Après quelques recherches, je suis tombé sur un [fil de stackoverflow](http://stackoverflow.com/questions/7068759/crontab-syntax-error) qui correspondait à mon problème.

Dans crontab, il est nécessaires d'échapper avec un backslash le caractère %. Le contab suivant fonctionne :

```

00 19 * * * /chemin/vers/mon/script.sh >/chemin/vers/output-`date +\%Y\%m\%d`.log
```
