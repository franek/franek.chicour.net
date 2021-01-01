---
date: 2009-12-04T17:36:00+01:00
title: "SSH : simplifier les connexions avec rebond"
author: "franek"
aliases: [/post/2009/10/16/SSH-%3A-simplifier-les-connexions-avec-rebond]
tags: ["développement web", "ProxyCommand", "rebond", "SSH", "tunnel"]
lastmod: 2011-10-16T15:12:35+02:00
---
Encore un billet de geek pour les geeks : la connexion SSH avec rebond. C'est un post qui trainait dans mes billets en attente. Je le publie afin de conserver une trace.

Exemple : vous souhaitez accéder à un serveur2 qui n'est accessible qu'à partir de serveur1 en une seule commande SSH depuis un de vos serveur (nous l'appellerons micha).

Solution : modifier la configuration ssh de micha.

Dans le fichier .ssh/config présent dans votre $HOME de micha, ajouter :

```

host nom_serveur2
   Hostname IP serveur2
   ProxyCommand ssh serveur1 nc %h %p 2> /dev/null
```

Vous pouvez ensuite utiliser ssh user@mon\_serveur2 pour vous connecter à serveur2. On vous demandera le mot de passe du compte sur serveur1 puis le mot de passe sur serveur2. Si vous souhaitez utiliser un compte particulier pour vous connecter à serveur1 vous pouvez utiliser la commande suivante :

```

   ProxyCommand ssh user@serveur1 nc %h %p 2> /dev/null
```

Le *nom\_serveur2* est un nom arbitraire. Vous pouvez mettre toto, titi, ... c'est comme vous voulez.

Le chemin de la connexion est le suivant : ma\_machine &gt; serveur1 &gt; serveur2. Si serveur1 et serveur2 possède un réseau privé, vous pouvez utiliser l'adresse privé.

Pour en savoir plus :

- [SSH proxy command ](http://wiki.tauware.de/blog:ssh-proxy-command "en")
- [Ssh ProxyCommand, a gateway for your xen vms](http://blog.tryphon.org/alban/archives/2009/01/22/ssh-proxycommand-a-gateway-for-your-xen-vms/)
- [Using ssh ProxyCommand to tunnel through two hosts](http://nico.schottelius.org/notizbuch-blog/archive/2008/06/07/using-ssh-proxycommand-to-tunnel-through-two-hosts)
