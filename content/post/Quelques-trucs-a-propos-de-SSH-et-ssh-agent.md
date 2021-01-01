---
date: 2013-07-22T14:23:00+02:00
title: "Quelques trucs à propos de SSH et ssh-agent"
author: "franek"
aliases: [/post/2013/07/22/Quelques-trucs-sur-SSH-et-SSH-AGENT]
tags: ["geek", "ssh", "ssh-agent", "sysadmin"]
lastmod: 2013-07-22T14:23:00+02:00
---
Je note ici quelques trucs que j'utilise et dont j'ai la manie d'oublier...

Pour propager les clés SSH entre serveur (via ssh-agent), une option intéressante est ForwardAgent.

Cela peut être utilisé dans le fichier de configuration ~/.ssh/config

```

Host example.com
  ForwardAgent yes
```

ou dans putty (si vous êtes sous Windows, malheureux...) : Property &gt; Connection &gt; SSH &gt; Auth &gt; Allow Agent Forwarding

Pour lister l'ensemble des clés SSH qui sont présentes dans l'agent SSH (ssh-agent), vous pouvez utiliser l'option -l de ssh-add

```

$ ssh-add -l
2048 72:...:52 description of the key (RSA)
```
