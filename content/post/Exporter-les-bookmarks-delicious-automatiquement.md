---
date: 2011-12-31T11:50:00+01:00
title: "Exporter les bookmarks delicious automatiquement"
author: ["franek"]
aliases: [/post/2011/12/31/Exporter-les-bookmarks-delicious-automatiquement]
tags: ["geek", "backup", "crontab", "delicious", "export", "python"]
lastmod: 2012-01-04T21:07:00+01:00
---
Un petit script python (mon premier) de fin d'année...

Si comme moi, vous souhaitez conserver les données que vous publiez dans le cloud, voici un petit script permettant d'exporter l'ensemble des bookmarks publiés sur [delicious](http://delicious.com).

Pour exporter automatiquement l'ensemble de vos bookmarks présents sur delicious, vous pouvez utiliser l'[API mise à disposition par delicious](http://delicious.com/help/api).

En utilisant quelque chose comme ça :

```

curl -k --user username:password -o backup.xml -O 'https://api.del.icio.us/v1/posts/all' 
```

[source](http://support.delicious.com/delicious/topics/export_delicious_to_xml_only_results_in_first_1000_bookmarks)

Cependant, l'API limite l'export aux 1000 derniers bookmarks.

Pour récupérer la totalité des bookmarks, delicious propose une [fonctionnalité d'export depuis l'interface utilisateur](http://export.delicious.com/settings/bookmarks/export) qui génère un fichier HTML.

Mon [script](https://gist.github.com/1540460), qui s'inspire d'un [autre script disponible sur github](https://gist.github.com/1431352), automatise l'export proposé par delicious depuis l'interface et ajoute simplement la possibilité de passer en paramètre les informations d'identification.

Pour l'utiliser :

```

git clone git://gist.github.com/1540460.git backup-delicious
cd backup-delicious
python delicious.py -u <username> -p <password> -o delicious.html
```

Pré-requis :

- Vous devez disposer de [python-requests](http://docs.python-requests.org/en/latest/index.html) (voir le fichier [delicious.py](https://gist.github.com/1540460#file_delicious.py) pour l'installation)

Vous pourrez ensuite ajouter ce script dans le crontab.

Par exemple :

```

0 19 * * * /usr/bin/python /directory/to/delicious.py -u <username> -p <password> -o /directory/to/backup/delicious-`date +\%Y\%m\%d`.html
```
