---
date: 2009-11-19T23:25:00+01:00
title: "Mise en place de la délégation d'authentification OpenID"
author: "franek"
aliases: [/post/2009/11/19/Mise-en-place-de-la-d%C3%A9l%C3%A9gation-d-authentification-OpenId]
tags: ["développement web", "authentifcation", "délégation", "OpenID"]
lastmod: 2011-10-16T21:35:39+02:00
---
Je continue dans la reprise du contrôle de mes données. Mon objectif, comme je l'ai déjà évoqué, est de ne pas être dépendant d'un fournisseur et de pouvoir facilement changer de fournisseur si celui-ci ne respecte plus ce que j'attends de lui (prix, publicité intempestive, politique de stockage de données, ...).

J'ai déjà repris la main sur mes mails ([avec mon propre nom de domaine et l'utilisation pour le moment de Google Apps](http://www.karlesnine.com/post/2009/11/20/Migration-DNS-n%C3%A9c%C3%A9ssaire-pour-utiliser-Google-App-avec-votre-nom-de-domaine)), le stockage de mes photos, sur le [microblogging](https://franek.chicour.net/post/2009/11/04/Le-microblogging-opensource) (que je n'utilise pas beaucoup mais c'est un autre sujet). Aujourd'hui, je vais vous parler de l'authentification via OpenID.

> OpenID est un système d’authentification décentralisé qui permet l’authentification unique (...). Il permet à un utilisateur de s’authentifier auprès de plusieurs sites (devant prendre en charge cette technologie) sans avoir à retenir un identifiant pour chacun d’eux mais en utilisant à chaque fois un unique identifiant OpenID.

(source [Wikipedia](http://fr.wikipedia.org/wiki/OpenID))

En résumé, vous vous authentifiez une fois auprès de votre fournisseur (par exemple, Yahoo) avec votre identifiant/mot de passe classique et vous êtes automatiquement identifié sur l'ensemble des services qui utilisent cette technologie et où vous avez renseigné votre adresse OpenID.

Il existe de nombreux fournisseurs OpenID (PIP Verisign, MyOpenId, Yahoo, Google, Orange). J'utilisais jusqu'à maintenant [celui de Yahoo](http://openid.yahoo.com/) mais, sauf erreur de ma part, il a un inconvénient majeur. Il n'autorise pas la délégation d'authentification. J'ai donc changé pour un fournisseur acceptant la délégation authentification (en l'occurence [PIP Verisign](https://pip.verisignlabs.com/)).

L'inconvénient de [PIP Verisign](https://pip.verisignlabs.com/) est que l'identifiant OpenID fourni n'est pas facile à retenir. Je souhaitais avoir quelque chose de plus simple. L'adresse de mon blog, par exemple, serait parfait. C'est là qu'intervient la délégation d'authentification OpenID.

La délégation d'authentification OpenID permet de définir l'adresse de votre site web comme identifiant OpenID. Cela fonctionne par l'ajout de balises META dans le code HTML de votre page qui va indiquer l'adresse du fournisseur OpenID que vous utilisez.

Les balises META ressemblent à ça :

- pour OpenID 1.0

```

<link rel="openid.server" href="http://myprovider.com/openid/server" />
<link rel="openid.delegate" href="http://john.myprovider.com/" />
```

- pour OpenID 2.0 (si votre fournisseur supporte OpenID 2.0)

```

<link rel="openid2.provider" href="http://myprovider.com/server" />
<link rel="openid2.local_id" href="http://john.myprovider.com/" />
```

Pour plus de détails, je vous renvoie sur la page dédiée de OpenID.net (<http://wiki2008.openid.net/Delegation>

Bien sûr, si vous utilisez Dotclear, il existe un [plugin](http://lab.dotclear.org/wiki/plugin/openidDelegation/fr) qui va vous permettre de vous faciliter la vie. Vous n'aurez pas à tripatouiller le code html. Merci à [Aurélien Bompard](http://aurelien.bompard.org/), le développeur de ce plugin. Pour plus d'infos, je vous invite d'ailleurs à lire son [billet sur le même sujet](http://aurelien.bompard.org/post/2009/05/18/Utiliser-son-blog-Dotclear-comme-identifiant-OpenID).

OpenID a un inconvénient majeur. Toute la sécurité de vos accès reposent sur le fournisseur OpenID. Si quelqu'un arrive à récupérer l'identifiant/mot de passe du compte de votre fournisseur OpenID. Il aura accès à l'ensemble des sites que vous utilisez avec OpenID. Utilisez donc un mot de passe très fort et changez le régulièrement.
