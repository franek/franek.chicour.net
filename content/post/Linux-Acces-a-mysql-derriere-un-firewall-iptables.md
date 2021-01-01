---
date: 2011-03-04T22:58:00+01:00
title: "Linux : Accès à mysql derrière un firewall (iptables)"
author: "franek"
aliases: [/post/2011/03/04/Linux-%3A-Acc%C3%A8s-%C3%A0-mysql-derri%C3%A8re-un-firewall-%28iptables%29]
tags: ["geek", "iptables", "mysql"]
lastmod: 2011-03-04T23:04:19+01:00
---
Je souhaite pouvoir accéder à une base mysql hébergée sur un serveur distant depuis un pc local. Ce serveur distant est protégé par un firewall (iptables).

Comment configurer mysql et iptables afin de pouvoir accéder à cette base mysql depuis mon poste local ?

Dans la suite de ce billet,

- 10.10.10.10 correspond à l'adresse IP du pc local
- 12.12.12.12 coresspond à l'adresse IP du serveur distant

Par défaut, sous debian, mysql n'écoute que sur l'interface locale (localhost). Il est donc nécessaire de configurer mysql afin qu'il écoute sur l'ensemble des interfaces. Pour se faire, il est nécessaire dans le fichier /etc/my.cnf de commenter la ligne suivante :

```

bind-address           = 127.0.0.1
```

puis redémarrer mysql

Pour vérifier que le paramétrage a bien été pris en compte, vous pouvez exécuter sur le serveur distant la commande suivante :

```

# netstat -lnt | grep 3306
tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN
```

Si votre serveur dispose d'un firewall (iptables) bloquant les ports non utiles, il est nécessaire d'ouvrir les ports associés à mysql pour votre PC local :

```

iptables -A INPUT -s 10.10.10.10 -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT
```

avec 10.10.10.10 correspondant à l'IP depuis laquelle vous souhaitez accéder à mysql

Pour vérifier que le paramétrage est bien pris en compte, vous pouvez utiliser nmap :

```

nmap -v -A 12.12.12.12 -p 3306
```

Dès lors si tout s'est bien passé, vous devriez pouvoir vous connecter à mysql :

```

mysql -ulogin -ppassword -h 12.12.12.12
```
