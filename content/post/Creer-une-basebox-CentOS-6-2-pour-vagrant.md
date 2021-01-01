---
date: 2012-06-02T11:54:00+02:00
title: "Créer une basebox CentOS-6.2 pour vagrant"
author: "jack"
aliases: [/post/2012/06/02/Cr%C3%A9er-une-basebox-CentOS-6.2-pour-vagrant]
tags: ["geek", "basebox", "CentOS", "french", "ruby", "vagrant", "veewee", "virtualbox"]
lastmod: 2013-03-11T22:49:57+01:00
---
[Vagrant](https://franek.chicour.net/post/2012/06/02/vagrantup.com/) est un logiciel écrit en Ruby permettant de simplifier la gestion des machines virtuelles dans un environnement de développement. Il va permettre de décrire (via un système de provisionning : puppet, chef, script sh) les composants nécessaires à un projet (php, mysql, ...).

Si vous souhaitez en savoir plus sur vagrant, je vous invite à consulter [cette présentation](http://www.ichilton.co.uk/blog/virtualization/my-phpne-talk-on-vagrant-496.html).

Vagrant [fournit](https://github.com/mitchellh/vagrant/wiki/Available-Vagrant-Boxes), par défaut, des box sous Ubuntu (Lucid et Precise).

Il est possible de récupérer des box créés par la communautés sur le [site vagrantbox.es](http://vagrantbox.es/) pour la plupart des distributions LINUX.

J'ai besoin d'une box (vagrant) CentOS-6.2 avec Puppet. Sauf erreur, ce type de VM n'est pas disponible sur [site vagrantbox.es](http://vagrantbox.es/). Je vais donc la créer grâce à [veewee](https://github.com/jedi4ever/veewee) qui est un utilitaire écrit en Ruby permettant de créer des box pour Vagrant.

Pré-requis :

- avoir installé VirtualBox
- avoir installé vagrant (qui est désormais dans les dépôts Ubuntu (`sudo apt-get install vagrant`))

Installation de veewe
---------------------

```
$ sudo gem install veewee
$ sudo gem install bundler

```

L'installation de veewee va ajouter l'ensemble des commandes *vagrant basebox*.

Pour vérifier que veewee a bien été installé, vous pouvez lancer la commande :

```
$ vagrant basebox

```

Cela devrait retourner :

```
Usage: vagrant basebox <command> [<args>]

Available subcommands:
     build
     define
     destroy
     export
     list
     ostypes
     templates
     undefine
     validate

For help on any individual command run `vagrant basebox COMMAND -h`

```

Veewee vient, par défaut, avec des templates de création de machine virtuelle. Pour lister l'ensemble des templates existant :

```
$ vagrant basebox templates

```

Cerise sur le gâteau, veewee dispose de plusieurs templates pour CentOS. Nous allons utiliser le template 'CentOS-6.2-x86\_64-minimal' dans la suite de ce document.

Création de la "basebox" pour vagrant
-------------------------------------

Nous allons lancer la création d'une machine virtuelle à partir du template 'CentOS-6.2-x86\_64-minimal'.

```
 $ vagrant basebox define 'centos-6.2'  'CentOS-6.2-x86_64-minimal'

```

centos-6.2 est un nom arbitraire. Il peut être remplacé par un nom qui vous semblera plus parlant.

Cette commande va créer un répertoire **definitions** qui contiendra des scripts de configuration de la VM. Il est possible de les éditer pour coller à l'environnement souhaité.

Notamment, par défaut, les machines virtuelles sont configurées pour utiliser des locales américaines. Il est possible de le changer en éditant le fichier definitions/centos-6.2/ks.cfg :

```
$ vi definitions/centos-6.2/ks.cfg

# valeurs à utiliser pour avoir l'OS en français (avec un clavier français)
lang fr_FR.UTF-8
keyboard fr 

```

On lance ensuite la création de la machine virtuelle :

```
 $ vagrant basebox build 'centos-6.2'

```

Cette commande va :

- télécharger l'ISO associer au template choisi (ici, CentOS-6.2-x86\_64-minimal.iso). L'iso sera placé dans le répertoire iso.
- vérifier le checksum de l'iso
- lancer VirtualBox avec l'iso
- exécuter les différents scripts présents dans le répertoire definitions.

Cela peut prendre quelques temps. Lorsque l'installation est terminée, vous pouvez vérifier la machine virtuelle :

```
 $ vagrant basebox validate centos-6.2

```

Ou l'exporter pour l'utiliser comme machine virtuelle vagrant :

```
 $ vagrant basebox export centos-6.2

```

Pour commencer à utiliser la machine virtuelle créée avec vagrant :

```
 $ vagrant box add centos-6.2 centos-6.2.box
 $ vagrant init centos-6.2
 $ vagrant up

```

Vous pouvez également partager cette basebox sur un serveur. D'autres utilisateurs pourront ainsi l'utiliser via une commande du type :

```
 $ vagrant box add centos-6.2 http://mon-serveur-web/chemin/vers/centos-6.2.box
 $ vagrant init centos-6.2
 $ vagrant up

```

La prochaine étape va être d'ajouter les éléments spécifiques à mon projet dans la basebox. Deux options s'ouvrent à moi :

- utiliser un système de provisionning (type puppet ou chef)
- modifier les scripts décrivant cette basebox (répertoire definitions) pour ajouter de base l'ensemble des logiciels dont j'ai besoin (php5, apache, oci8, ...). Je serai donc obligé de récréer cet environnement, ce qui peut être un peu plus fastidieux.

La suite au prochain épisode...
