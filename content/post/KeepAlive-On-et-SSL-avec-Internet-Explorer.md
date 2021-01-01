---
date: 2011-04-29T15:26:00+02:00
title: "KeepAlive On et SSL avec Internet Explorer"
author: "franek"
aliases: [/post/2011/04/29/KeepAlive-On-et-SSL-avec-Internet-Explorer]
tags: ["développement web", "apache", "keepalive", "ssl", "webperf"]
lastmod: 2011-10-23T17:00:15+02:00
---
Une des bonnes pratiques de performance web est d'activer KeepAlive sur un serveur Apache.

Sur une de mes applications, le KeepAlive n'était pas activé pour IE et je ne comprenais pas pourquoi.

Après investigation, cela venait de la configuration par défaut de Apache dans mon Virtual Host sur le port 443 qui contenait les directives suivantes :

```

 SetEnvIf User-Agent ".*MSIE.*" \
            nokeepalive ssl-unclean-shutdown \
            downgrade-1.0 force-response-1.0
```

Cette directive indique à Apache de désactiver le KeepAlive pour Internet Explorer (Toute version confondue). C'est dû à un bug de IE de gestion du protocole SSL. Ce bug n'est présent que sur les versions de Internet Explorer inférieures ou égales à 6.

Dans mon cas, on peut remplacer la directive Apache par :

```

BrowserMatch ".*MSIE [2-5]\..*" \
	nokeepalive ssl-unclean-shutdown \
	downgrade-1.0 force-response-1.0
```

Source : [http://blogs.msdn.com/b/ieinternals/archive/2011/03/26/https-and-connection-close-is-your-apache-modssl-server-configuration-set-to-slow.aspx](http://blogs.msdn.com/b/ieinternals/archive/2011/03/26/https-and-connection-close-is-your-apache-modssl-server-configuration-set-to-slow.aspx "Blogs MSDN HTTPS & KeepAlive")
