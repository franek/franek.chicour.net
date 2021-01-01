---
date: 2012-03-30T17:31:00+02:00
title: "Synology et variable d'environnement $HOME pour les utilisateurs"
author: "franek"
aliases: [/post/2012/03/30/Synology-et-variable-d-environnement-%24HOME-pour-les-utilisateurs]
tags: ["geek", "$HOME", "synology", "unix", "variable d environnement"]
lastmod: 2013-03-11T22:59:23+01:00
---
Si vous vous amusez à bidouiller un peu votre Synology et à créer des comptes utilisateurs afin que vous puissiez vous connecter en SSH, vous remarquerez que la variable d'environnement $HOME est positionné par défaut à /root. Si vous avez créer un compte "bidon", le $HOME de cet utilisateur sera donc /root. Cela peut parfois être gênant (notamment, pour git qui voudra créer le fichier de configuration $HOME/.gitconfig).

Pour régler ce problème, la solution que j'ai utilisée (il y a sûrement plus élégant) est la suivante :

Remplacement dans le fichier /etc/profile de :

```
HOME=/root
export HOME

```

par

```
if [[ $USER == "root" ]]; then
         HOME=/root
else
         HOME=/volume1/homes/$USER
fi
export HOME

```

J'espère que cette modification n'aura pas d'effets collatéraux.
