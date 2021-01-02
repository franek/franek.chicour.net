---
date: 2008-03-31T22:12:00+02:00
title: "Easter Egg dans PHP"
author: ["franek"]
aliases: [/post/2008/03/31/Easter-Egg-dans-PHP]
tags: ["geek", "easter egg", "php"]
lastmod: 2008-03-31T22:12:00+02:00
---
Le [CERTA](http://www.certa.ssi.gouv.fr/) (Centre d'Expertise Gouvernemental de Réponse et de Traitement des Attaques informatiques) m'a fait découvrir un [Easter Egg](http://fr.wikipedia.org/wiki/Easter_egg) dans PHP que je ne connaissais pas. Lorsque expose\_php est à on dans le fichier de configuration php.ini, l'ajout dans l'URL de "?=PHPB8B5F2A0-3C92-11d3-A3A9-4C7B08C10000" enverra le Easter Egg (message adressé aux développeurs)

Essayer d'appeler l'URL chez php.net : <http://www.php.net/index.php?=PHPB8B5F2A0-3C92-11d3-A3A9-4C7B08C10000>

Sur le serveur qui héberge ce site, le paramètre expose\_php est à off. L'URL <http://franek.chicour.net/index.php?=PHPB8B5F2A0-3C92-11d3-A3A9-4C7B08C10000> ne renvoie donc rien.

Rigolo, n'est-il pas ?

Rappel : Afin de ne pas divulger la version de PHP que vous utilisez, il est conseillé de positionner à off la variable de configuration [expose\_php dans le fichier php.ini](http://fr2.php.net/manual/fr/ini.core.php).

Source : [communiqué 2008-013 du CERTA](http://www.certa.ssi.gouv.fr/site/CERTA-2008-ACT-013.pdf)
