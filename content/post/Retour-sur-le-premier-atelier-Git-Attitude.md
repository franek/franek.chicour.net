---
date: 2010-07-12T21:06:00+02:00
title: "Retour sur le premier atelier Git Attitude"
author: ["franek"]
aliases: [/post/2010/07/12/Retour-sur-le-premier-atelier-Git-Attitude]
tags: ["geek", "git", "gitattitude", "subversion"]
lastmod: 2011-10-23T17:00:15+02:00
---
Christophe Porteneuve, ancien Président de [Paris Web](http://www.paris-web.fr) et directeur technique chez [Ciblo](http://www.ciblo.net), a eu l'excellente idée d'organiser le [premier atelier Git Attitude](http://blog.git-attitude.fr/post/2010/06/18/premier-atelier-git-attitude). Cela s'est passé samedi dernier dans les locaux de [Clever Age](http://www.clever-age.com/) (Paris).

L'objectif de cet atelier était de présenter les fonctionnalités de Git et d'aider les participants à prendre en main ce [système de gestion des sources décentralisé](http://fr.wikipedia.org/wiki/Logiciel_de_gestion_de_versions#Distribu.C3.A9). Le [programme de la journée](http://blog.git-attitude.fr/post/2010/06/18/premier-atelier-git-attitude) était dense. Malgré les 8 heures prévues, il n'a pas été possible d'étudier l'ensemble des points au programme, mais on a vu beaucoup de choses intéressantes, de très bonnes astuces et l'envie d'approfondir nos connaissances.

Christophe partage avec enthousiasme sa passion pour Git. On sent qu'il est heureux d'avoir quitté les anciens systèmes de gestion de source centralisé (type Subversion ou CVS) pour Git.

Le prix demandé pour ce type de manifestation est dérisoire (50€ pour les early birds, 75€ pour les autres, petit-déjeuner - avec ses succulents croissants - et déjeuner inclus).

Si ce type d'évènement se reproduit et, que vous aussi, vous souhaitez vous former à Git rapidement, courrez rejoindre Christophe et Dick Rivers (git revert) à cette manifestation, vous ne le regretterez pas !

Utilisateur au quotidien de Subversion depuis plusieurs années, je réfléchis depuis plusieurs semaines au passage à un gestionnaire de sources décentralisé. Je teste Mercurial depuis quelques semaines (et pourquoi Mercurial ? parce que ...). Cet atelier m'a donné envie de passer à Git. Il faudra néanmoins que je trouve des solutions pour remplacer correctement les ressources externes (j'utilise à fond les ressources externes de subversion pour pointer sur des bibliothèques partagées - framework commun, ...) et migrer en douceur ma vingtaine de projets. Git propose des solutions :

- [git svn](http://www.kernel.org/pub/software/scm/git/docs/git-svn.html) pour utiliser subversion en dépôt central
- les [submodule](http://www.kernel.org/pub/software/scm/git/docs/git-submodule.html) (qui ne sont pas aussi puissants que les ressources externes)

Quelques notes prises durant la journée
---------------------------------------

### Installation de la dernière de version de Git sous Ubuntu

Pour installer une version récente de Git sur Ubuntu, il est nécessaire de compiler Git à partir des sources, la version présente dans les dépôts étant un peu vieille. Pour se faire, il est nécessaire d'installer les outils de compilation et certaines dépendances pour générer la documentation :

```
sudo apt-get install build-essential
sudo apt-get install -q -y libcurl4-openssl-dev tk asciidoc docbook2x xmlto
```

Télécharger[ git-1.7.1.1](http://git-scm.com/) et décompresser dans un répertoire temporaire.

Compiler :

```
<pre class="c c" style="font-family:inherit">.<span style="color: #339933;">/</span>configure
make all man info
sudo make install install<span style="color: #339933;">-</span>man install<span style="color: #339933;">-</span>info
```

Par défaut, git s'installera dans /usr/local. Si vous souhaitez l'installer dans un autre répertoire, vous pouvez modifier les options de configuration de ./configure

A priori, il semble exister des [paquets Ubuntu plus récents sur les dépôts PPA](https://launchpad.net/~voronov84/+archive/andreyv).

### Configuration de l'environnement

Il est possible de définir une configuration globale au système. Cette configuration va notamment contenir les Alias de configuration. Exemple de configuration à positionner dans /home/user/.gitconfig

```

[user]
	name = My Name
	email = adresse@domain.net
[color]
	diff = auto
	status = auto
	branch = auto
[alias]
	st = status
	ci = commit
	co = checkout
	fp = format-patch
	lg = log --graph --pretty=tformat:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%an %cr)%Creset' --abbrev-commit --date=relative
[core]
	pager = cat
```

*(à compléter)*

Merci à Christophe pour l'initiative. J'espère que les ateliers Git Attitude seront une aussi belle réussite que Paris Web.
