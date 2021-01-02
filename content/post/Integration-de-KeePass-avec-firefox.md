---
date: 2013-10-18T23:30:00+02:00
title: "Intégration de KeePass avec firefox"
author: ["franek"]
aliases: [/post/2013/10/19/Int%C3%A9gration-de-KeePass-et-firefox]
tags: ["geek", "firefox", "keepass", "mot de passe", "sécurité"]
lastmod: 2017-05-15T19:25:32+02:00
---
Je cherchais depuis plusieurs années (sans jamais avoir pris le temps de chercher...) une solution permettant d'intégrer les mots de passe Firefox dans [KeePass](http://fr.wikipedia.org/wiki/KeePass) (un gestionnaire de mots de passe - coffre fort numérique), la sauvegarde des mots de passe dans Firefox étant un peu faible (stockage en clair).

La solution que l'on m'a conseillée est l'utilisation de l'[extension Firefox keefox](https://addons.mozilla.org/en-US/firefox/addon/keefox/). L'extension keefox remplace le gestionnaire natif de Firefox et communique directement avec la base de données KeePass (que vous aurez pris soin de sécuriser). Lorsque la connexion est établie entre KeePass et Firefox, Firefox est capable de lire les mots de passe présents dans la base de données KeePass ainsi que d'écrire les nouveaux mots de passe.

Cette solution fonctionne sous linux (après avoir installé keepass2 avec mono).

Avec cette solution, vous n'aurez plus aucune raison de ne plus disposer d'un mot de passe fort par site.

Il existe le même genre de plugins pour Chrome.
