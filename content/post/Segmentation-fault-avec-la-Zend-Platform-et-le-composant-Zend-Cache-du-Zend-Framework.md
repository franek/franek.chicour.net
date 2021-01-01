---
date: 2009-11-09T09:25:00+01:00
title: "Segmentation fault avec la Zend Platform et le composant Zend_Cache du Zend Framework"
author: "franek"
aliases: [/post/2009/11/09/Segmentation-fault-avec-la-Zend-Platform-et-le-composant-Zend-Cache-du-Zend-Framework]
tags: ["développement web", "apache", "Segmentation Fault", "Zend Cache", "Zend Framework", "Zend Platform"]
lastmod: 2009-11-09T09:25:00+01:00
---
Il nous aura fallu environ 1 mois sur nos serveurs de production pour trouver une résolution à ce problème. Afin que sa résolution puisse servir, je poste un petit mémo.

Si vous rencontrez des segmentations fault Apache du type :

`[Mon Oct 05 13:02:32 2009] [notice] child pid 25046 exit signal Segmentation fault (11)`

et que vous utilisez la [Zend Platform](http://www.zend.com/fr/products/platform/) et [Zend Framework](http://framework.zend.com) (et notamment le composant [Zend\_Cache](http://framework.zend.com/manual/fr/zend.cache.html)), cela peut venir du [backend Zend\_Platform du module Zend Cache du Zend Framework](http://framework.zend.com/manual/en/zend.cache.backends.html#zend.cache.backends.platform).

En effet, le backend Zend\_Platform du composant Zend\_Cache du Zend Framework utilise les méthodes obsolètes de stockage en cache de la Zend Platform (output\_cache\_get / output\_cache\_put). Ces méthodes sont obsolètes (cf. la [documentation de l'API de la Zend Platform](http://files.zend.com/help/Zend-Platform/deprecated_caching_apis_and_directives.htm)). Vous devriez plutôt utiliser les méthodes zend\_\[shm|disk\]\_cache\_delete, zend\_\[shm|disk\]\_cache\_store, zend\_\[shm|disk\]\_cache\_fetch.

Un [bug](http://framework.zend.com/issues/browse/ZF-8003) (ZF-8003) a été ouvert sur le Zend Framework qui ne sera pas corrigé en raison de la non homogénéité des plate-formes (la version windows de la Zend Platform ne connait pas les nouvelles méthodes).

Pour régler le problème, une des solutions est d'utiliser le backend Zend Server du Zend Framework qui fonctionne avec les dernières version de la Zend Platform (3.6.2 et supérieure). Ce backend utilise les méthodes zend\_\[shm|disk\]\_cache\_delete, zend\_\[shm|disk\]\_cache\_store, zend\_\[shm|disk\]\_cache\_fetch qui sont compatibles avec la Zend Platform.

J'espère que cela pourra aider.
