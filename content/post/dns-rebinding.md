---
title: "TIL: DNS Rebinding Protection"
date: 2025-03-10T22:00:13+01:00
cover:
    image: "/public/dns-rebinding-protection/image.jpg"
    relative: false
tags: ["DNS", "Rebinding", "TIL"]
---

Certains résolveurs DNS publics n'autorisent pas la résolution sur des adresses IPs privées.
C'est, par exemple, le cas des résolveurs de Free (Free l'a [confirmé](https://dev.freebox.fr/bugs/task/9909) il y a plusieurs années).
Cette protection est mise en place pour se protéger du [DNS Rebinding](https://en.wikipedia.org/wiki/DNS_rebinding).

Pour l'exemple, j'ai créé l'entrée DNS suivante sur mon domaine chicour.net : 
```
10.1.2.3.chicour.net.   10800   IN      A       10.1.2.3
```

Le domaine `10.1.2.3.chicour.net` pointe sur l'IP `10.1.2.3`.

Si on utilise le résolveur DNS de Google (8.8.8.8) avec la commande `dig`, le résolveur DNS me remonte bien l'adresse IP que j'ai renseignée.

```
dig +short @8.8.8.8 10.1.2.3.chicour.net
10.1.2.3
```

Si j'effectue la même requête sur un [résolveur DNS de Free](https://assistance.free.fr/articles/363) (`212.27.40.240`), je n'obtiens pas de résultats.

```
dig +short @212.27.40.240 10.1.2.3.chicour.net
```

Ce résolveur est utilisé par la Freebox. Donc si vous êtes chez Free, il est probable que vous ne puissiez pas résoudre des domaines pointant sur des adresses IP privées.

A priori, les résolveurs DNS des principaux autres opérateurs français ne sont pas joignables depuis mon opérateur. Je n'ai donc pas pu valider le comportement des autres opérateurs.

J'ai néanmoins testé les [résolveurs DNS de la FDN (French Data Network)](https://www.fdn.fr/actions/dns/). Les adresses IPs privées sont bien résolues.

```
dig +short @80.67.169.12 10.1.2.3.chicour.net
10.1.2.3
```

Voilà, voilà, ... Tout ça m'a joué des tours ces derniers jours et je suis content d'avoir trouvé une explication rationnelle à tout ça....

