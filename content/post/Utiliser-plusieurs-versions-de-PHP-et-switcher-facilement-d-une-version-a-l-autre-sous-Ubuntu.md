---
date: 2010-03-30T18:32:00+02:00
title: "Utiliser plusieurs versions de PHP et switcher facilement d'une version à l'autre sous Ubuntu"
author: "franek"
aliases: [/post/2010/03/30/Utiliser-plusieurs-versions-de-PHP-et-switcher-facilement-d-une-version-a-l-autre-sous-Ubuntu]
tags: ["développement web", "installation", "Lamp", "oracle", "php", "ubuntu", "Zend Server"]
lastmod: 2010-04-09T16:34:16+02:00
---
**EDIT du 09/04/2010** : En fait, cette technique est obsolète. Je viens de découvrir [PHPFarm](http://cweiske.de/tagebuch/Introducing%20phpfarm.htm) qui semble faire plus ou moins ce que je souhaite faire. A tester donc.

\--

Sur mon environnement de développement, je souhaite pouvoir switcher facilement d'une version de PHP à l'autre. Mes pré-requis sont de disposer de versions compilées de PHP (avec les extensions APC et Xdebug) ainsi que d'une version de PHP packagée avec Zend Server.

Je souhaite conserver la même version d'Apache. Sous windows, j'aurai avantageusement pu utiliser [Wampserver](http://www.wampserver.com/), [EasyPHP](http://www.easyphp.org/), ... Sous Linux, à ma connaissance, il n'existe pas de mécanisme de ce type.

J'ai donc développé un petit script Bash qui permet d'installer rapidement l'ensemble des versions PHP nécessaires avec les mêmes options de compilation.

J'utilise une version de Ubuntu mais cela devrait fonctionner avec une autre distribution.

A l'issue de l'installation, je pourrais switcher d'une version de PHP en une seule commande. Le PHP installé contiendra les mêmes extensions.

Le script va installer les différentes versions de PHP en utilisant la ligne de compilation suivante (qui correspond à mes besoins - support Oracle, mysql, gettext - , il est bien entendu possible de l'adapter à votre besoin) :

```

./configure --prefix=$installdir/$version \
        --with-config-file-path=$installdir/$version/etc \
        --with-apxs2=/usr/bin/apxs2 \
        --with-oci8=instantclient,/usr/local/oracle/instantclient \
        --enable-pdo \
        --with-pdo-oci=instantclient,/usr/local/oracle/instantclient,10.2.0.3 \
        --with-libxml-dir=/usr/lib/libxml2 \
        --with-xsl \
        --enable-ftp \
        --with-gettext \
        --enable-mbstring \
        --enable-soap \
        --enable-calendar \
        --with-openssl \
        --with-zlib \
        --with-mysql \
        --with-gd \
        --with-freetype-dir=/usr \
        --with-jpeg-dir=/usr \
        --enable-gd-native-ttf \
        --with-ttf \
        --with-t1lib \
	--enable-cli
```

Préparation de l'environnement
------------------------------

1. Installer Zend Server. Vous pouvez suivre la [procédure habituelle](http://www.zend.com/fr/products/server/downloads).
2. Installer les paquets manquants afin de pouvoir compiler PHP (si vous souhaitez d'autres modules PHP, vous devrez ajouter d'autres paquets) :

```

sudo apt-get install apache2-prefork-dev libxml2-dev libxslt-dev openssl bison flex gcc automake libt1-dev libjpeg62-dev libfreetype6-dev freetype1-tools libgd-dev libmysqlclient15-dev
```

1. Créer un fichier compil-php.sh contenant :

```

#!/bin/bash
# ---------------------------------------------------------------
# Script d'installation de plusieurs versions PHP sous Ubuntu
# Auteur : franek (franek at chicour dot net)
# ---------------------------------------------------------------

# répertoire où seront stockées les sources compilées de PHP
compildir=/opt/compil-php

# répertoire où seront installées les différentes versions de PHP
installdir=/usr/local

# Liste des versions de PHP à installer. Respecter la syntaxe php-X.Y.Z (sauf pour zend-ce)
versioninstall="zend-ce php-5.2.5 php-5.2.13";

# Nom du programme
progname=$(basename $0)

# Usage de ce script
# ---
function Usage()
{
	echo ""
    echo " Objet :"
    echo "   Ce programme permet d'installer plusieurs version de PHP sur un même serveur et de switcher d'une version de PHP à l'autre"
    echo ""
    echo " Usage : "
    echo "   $progname <action>"
	echo " Les <action> possibles sont : "
	echo "   - list : liste les versions de php installées"
	echo "   - install : installe toutes les versions PHP"
	echo "   - switch : permet de switcher de version"
    echo "   exemple : "
    echo "   $progname list"
}

# Création de l'environnement
# ---
function CreateEnv
{
	echo " - Création de l'environnement de compilation"
	if [ ! -d $compildir ]; then
		echo " - Création du répertoire $compildir"
		sudo mkdir -p $compildir
		sudo chmod 777 $compildir
	fi
}

# Téléchargement des sources de PHP à installer
# ---
function Download
{
	version=$1
	echo " - Téléchargement de $version"
	cd $compildir
	# Pour la version 5.2.5, il faut la récupérer sur museum.php.net
	# @todo : gérer les versions inférieures à 5.2.5
	if [ $version = "php-5.2.5" ]; then
		url=http://museum.php.net/php5/php-5.2.5.tar.gz
	else
		url=http://fr.php.net/get/$version.tar.gz/from/this/mirror
	fi
	wget $url
}

# Décompression des sources de PHP
# ---
function Unzip
{
	version=$1
	cd $compildir
	tar xvfz $version.tar.gz
	rm $version.tar.gz
}

# Compilation de PHP
# ---
function Compil
{
	version=$1
	phpcompildir="$compildir/$version"
	echo $phpcompildir
	cd $phpcompildir
	
	export OPTIM=-02
	make clean

	# compilation de PHP avec support Oracle, Gettext, ...
	# cette configuration peut être modifiée.
	./configure --prefix=$installdir/$version \
        --with-config-file-path=$installdir/$version/etc \
        --with-apxs2=/usr/bin/apxs2 \
        --with-oci8=instantclient,/usr/local/oracle/instantclient \
        --enable-pdo \
        --with-pdo-oci=instantclient,/usr/local/oracle/instantclient,10.2.0.3 \
        --with-libxml-dir=/usr/lib/libxml2 \
        --with-xsl \
        --enable-ftp \
        --with-gettext \
        --enable-mbstring \
        --enable-soap \
        --enable-calendar \
        --with-openssl \
        --with-zlib \
        --with-mysql \
        --with-gd \
        --with-freetype-dir=/usr \
        --with-jpeg-dir=/usr \
        --enable-gd-native-ttf \
        --with-ttf \
        --with-t1lib \
		--enable-cli
	
	make -j 10
}

# Affiche la liste des versions de PHP disponibles
# ---
function List
{
	echo "Versions disponibles : "
	# pour chaque version, on installe
	for version in $versioninstall
	do
		echo " - PHP version $version";
	done
	echo "Si vous souhaitez ajouter des versions, vous devez simplement éditer la variable versioninstall"
}

# Fonction qui permet de switcher de version de PHP
# ---
function Switch
{
	i=1
	echo "Versions disponibles : "
	for version in $versioninstall
	do
		tab[$i]="$version"
		echo " $i/ PHP version $version";
		i=$(($i + 1))
	done
	echo " - Quelle version de PHP souhaitez-vous utiliser ?"
	read item
	echo " - vous avez choisi d'utilsier : ${tab[$item]}";
	
	version=${tab[$item]}
	cd /usr/lib/apache2/modules
	if [ "$version" = "zend-ce" ]; then
		# PHP version Zend
		sudo rm libphp5.so && sudo ln -s ../../../local/zend/lib/php/libphp5.so libphp5.so
	else
		# PHP version compilé 5.2.5
		sudo rm libphp5.so && sudo ln -s $compildir/$version/libs/libphp5.so
	fi
	sudo apache2ctl restart
}

# Procédure d'installation de PHP
# ---
function InstallPhp
{
	while :
	do
		version=$1
		echo " - voulez-vous installer PHP (version : $version) ? (0/N)"
		read OK
		case $OK in
			"O") 	sudo make install-cli
					sudo make install-pear
					sudo make install-programs
					sudo make install-programs
					sudo make install-build
					sudo make install-headers
					#installation de apc et xdebug
					cd "$installdir/$version/bin"
					sudo ./pear update-channels
					sudo ./pear upgrade-all
					sudo ./pecl install pecl/apc
					sudo ./pecl install pecl/xdebug
					#création du fichier php.ini par défaut
					sudo touch $installdir/$version/etc/php.ini
					sudo chmod 777 $installdir/$version/etc/php.ini
					sudo echo -e "extension=apc.so\nextension=xdebug.so" > $installdir/$version/etc/php.ini
					break;;
			"N") echo "Cette version ne sera pas installée."; break;;
			*) echo " /!\ Veuillez répondre par O ou N !";;
		esac
	done
}

# Fonction générale de lancement de l'installation de PHP
function Install
{
	# création de l'environnement
	CreateEnv

	# pour chaque version, on installe
	for version in $versioninstall
	do
		# on installe pas zend-ce
		if [ $version = "zend-ce" ]; then
			continue;
		fi
		Download $version
		Unzip $version
		Compil $version
		InstallPhp $version
	done;
}

# -------------------------------------------------------------------------------
# ---- début du script ----------------------------------------------------------
# -------------------------------------------------------------------------------

if [ ! $# -eq 1 ]
then
        Usage
        exit 0;
else
	action=$1
	case $action in
        "list") List;;
        "install") Install;;
		"switch") Switch;;
        *) echo " /!\ Mauvaise utilisation"; Usage; exit 1; ;;
    esac	
fi
```

1. Editer le script avec les versions de PHP que vous souhaitez installer. La variable à modifier est versioninstall. Chaque version doit être séparée par un espace. Le nom de la version doit respecter la syntaxe php-X.Y.Z.
2. Exécuter ce script.

./compil-php.sh

Par défaut, ce script va vous afficher les commandes disponibles. Vous avez 3 options :

- install : va installer les versions de PHP dans /usr/local/php-X.Y.Z
- list : afficher la liste des versions de PHP configurées dans le script
- switch : lorsque les versions de PHP ont été installées, permet de switcher d'une version de PHP à l'autre.

Par défaut, ce script va compiler les PHP dans le répertoire /opt/compil-php. Cette variable peut être modifiée dans le script.

Les binaires seront installés dans /usr/local/php-X.Y.Z. Le fichier de configuration php.ini se trouvera dans /usr/local/php-X.Y.Z/etc/php.ini (il est donc possible d'avoir un fichier php.ini par installation de PHP).

C'est un script brut. Des modifications pourraient être apportéees :

- mise en oeuvre des contrôles d'erreurs
- installation automatique de Zend Server
- installation de HipHop
- ...
