---
date: 2011-03-03T22:20:00+01:00
title: "APC et Zend Server"
author: ["franek"]
aliases: [/post/2011/03/03/APC-et-Zend-Server]
tags: ["développement web", "Apc", "php", "Zend", "Zend Server"]
lastmod: 2011-10-23T17:00:15+02:00
---
Une des limitations du cache de Zend Server (ShMem ou Disk) est de ne pas proposer d'outils de monitoring des éléments mis en cache. Apc propose cela par défaut via l'installation du script apc.php.

Zend Server propose, par défaut, une [émulation de APC via le Zend DataCache](http://forums.zend.com/viewtopic.php?f=8&t=5436#p18722). Cependant, cette émulation ne propose pas toute l'API de APC. Le script apc.php ne fonctionne donc pas. Je n'ai pas trop cherché mais, a priori, cela vient du non support complet des méthodes suivantes apc\_compile\_file(), apc\_sma\_info(), apc\_cache\_info() (voir [forum chez phpfrance](http://forum.phpfrance.com/php-avance/probleme-zend-server-apc-apc-cache-info-t255768.html)).

Je viens de découvrir que Zend mettait à disposition un paquet Apc.

Pour l'installer sur une debian/ubuntu, il suffit de :

```

# php-5.2
sudo apt-get install php-5.2-apc-zend-server
# php-5.3
sudo apt-get install php-5.3-apc-zend-server
```

puis redémarrer Apache (vérifier au préalable que le fichier /usr/local/zend/etc/conf.d/apc.ini est bien présent)

Il est donc ensuite possible de charger l'extension apc.so dans son php.ini. A nous les joies de l'utilisation de apc.php avec Zend Server.
