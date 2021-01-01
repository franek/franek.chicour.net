---
date: 2013-11-11T22:25:00+01:00
title: "Lister toutes les machines d'un réseau"
author: "franek"
aliases: [/post/2013/11/11/Lister-toutes-les-machines-d-un-r%C3%A9seau]
tags: ["geek", "list", "network", "nmap", "réseau"]
lastmod: 2013-11-19T13:31:18+01:00
---
Je note ici quelques commandes que j'utilise mais dont j'ai la manie d'oublier.

Pour lister les machines présentes sur le réseau, il est possible d'utiliser nmap :

```

# nmap -sP 192.168.0.0/24
Nmap scan report for server1 (192.168.0.2)
Host is up (0.0031s latency).
Nmap scan report for 192.168.0.4
Host is up (0.00037s latency).
Nmap scan report for 192.168.0.5
```

source : [Nmap: le scanneur de réseau](http://blog.nicolargo.com/2007/08/nmap-le-scanneur-de-reseau.html) sur Nicolargo
