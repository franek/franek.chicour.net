---
date: 2011-08-12T14:55:00+02:00
title: "Quelques trucs et astuces concernant git (et git svn)"
author: "franek"
aliases: [/post/2011/02/11/Quelques-trucs-et-astuces-concernant-git-%28et-git-svn%29]
tags: ["geek", "astuces", "git", "git-svn"]
lastmod: 2011-08-12T14:55:00+02:00
---
Une petite liste de trucs et astuces concernant l'utilisation de git (avec svn ou non).

Pour définir l'éditeur par défaut utilisé par git (ici vi) :

```

$ git config --global core.editor vi
```

Récupérer l'ensemble du dépôt subversion dans un environnement git :

```

$ git svn clone -s http://url_depot_svn/ rep-destination/
```

Resynchroniser le dépôt local (git) avec le dépôt subversion (récupération des tags notamment).

```

$ git svn fetch
```

Dans le cas d'une utilisation de git avec subversion, afficher tous les tags et les branches subversion

```

$ git branch -a
```

Créer une branche git qui suit les modifications d'une branche subversion

```

$ git checkout -b local-trunk remotes/trunk
```

Ici, on crée une branche git local-trunk qui est une copie de remotes/trunk et qui suit ces modifications

Commiter l'ensemble des modifications locales vers le dépôt subversion

```

$ git svn dcommit
```

Par défaut, git ne supprime pas les répertoires vides. Il est possible d'indiquer à git de supprimer les répertoires vides dans subversion :

- option 1, dans le fichier de configuration de git ~/.gitconfig

```

[svn]
        rmdir = true
```

- option 2, lors de l'appel de git svn dcommit :

```

$ git svn dcommit --rmdir
```

Disposer d'un diff en couleur ([source](https://git.wiki.kernel.org/index.php/GitFaq#Why_does_diff.2Flog_not_show_color.2C_even_though_I_enabled_it.3F "git diff en couleur")) :

```

[core]
        pager = less -FXRS
```
