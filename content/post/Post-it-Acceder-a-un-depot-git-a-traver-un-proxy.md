---
date: 2011-08-06T17:12:00+02:00
title: "Post-it : Accéder à un dépôt git à traver un proxy"
author: ["franek"]
aliases: [/post/2011/08/05/Acc%C3%A9der-%C3%A0-un-d%C3%A9p%C3%B4t-git-%C3%A0-traver-un-proxy]
tags: ["geek", "corkscrew", "git", "post-it", "proxy"]
lastmod: 2011-10-11T12:44:24+02:00
---
Il est parfois nécessaire de pouvoir accéder à son dépôt git (push et pull) auto-hébergé derrière un proxy.

Mon dépôt git ne support pas le [smart HTTP protocol](https://github.com/blog/642-smart-http-support).

Je vais vous présenter ici une technique s'appuyant sur corkscrew. Il y existe sûrement d'autres techniques (port forwarding, ...).

Cette technique sous-entend que ssh est configuré sur le port 443 de votre serveur.

Installer corkscrew :

```

$ sudo apt-get install corkscrew
```

Ajouter dans le fichier ~/.ssh/config :

```

Host mon.domaine.net
 User git
 Port 443
 TCPKeepAlive yes
 ProxyCommand /usr/bin/corkscrew <proxy> <port proxy> %h %p
```

Cette configuration signifie : Pour le domaine *mon.domaine.net* (Host mon.domaine.net) utilise l'utilisateur git sur le port 443 et passe par le proxy &lt;proxy&gt; en utilisant corkscrew. TCPKeepAlive permet de maintenir la connexion.
