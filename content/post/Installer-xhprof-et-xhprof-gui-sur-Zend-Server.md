---
date: 2011-04-15T11:58:00+02:00
title: "Installer xhprof et xhprof gui sur Zend Server"
author: "franek"
aliases: [/post/2011/04/15/Installer-xhprof-et-xhprof-gui-sur-Zend-Server]
tags: ["développement web", "php", "profiling", "xdebug", "xhprof", "Zend Server"]
lastmod: 2012-11-27T21:13:27+01:00
---
[Xhprof](http://mirror.facebook.net/facebook/xhprof/doc.html "xhprof") est un profiler de code PHP. C'est un concurrent de Xdebug développé par Facebook.

Il a le gros avantage de permettre de visualiser l'évolution de la mémoire. A ma connaissance, Xdebug ne le permet pas.

Il ne nécessite pas l'utilisation d'un logiciel tiers (type KCachegrind, non disponible sous Windows...argh...) et peut être installé sur un serveur de production sans, normalement, trop dégrader les performances.

Je vais ici vous décrire son installation sur Zend Server CE et l'installation de *xhprof gui*

Si vous utilisez une installation de PHP moins exotique (genre une debian avec les [dotdeb](http://www.dotdeb.org/ "dotdeb")), son installation sera, à mon avis, simplifiée :

```

apt-get install php5-xhprof
```

Installation de xhprof
----------------------

On récupère les sources et on les décompresse :

```

$ wget http://pecl.php.net/get/xhprof-0.9.2.tgz
$ tar xvfz xhprof-0.9.2.tgz
```

On compile :

```

$ cd xhprof-0.9.2/extension
$ /usr/local/zend/bin/phpize
$ ./configure --with-php-config=/usr/local/zend/bin/php-config
$ make
$ make test
$ sudo make install
```

On modifie la configuration de PHP pour lui indiquer de charger cette extension :

```

$ sudo vi /usr/local/zend/etc/php.ini
```

On ajoute :

```

[xhprof]
extension=xhprof.so
;
; directory used by default implementation of the iXHProfRuns
; interface (namely, the XHProfRuns_Default class) for storing
; XHProf runs.
;
xhprof.output_dir=/tmp/xhprof
```

Il est nécessaire de créer le répertoire /tmp/xhprof et de donner les droits à l'utilisateur Apache (je fais un 777 par simplicité)

```

$ mkdir -p /tmp/xhprof
$ chmod 777 /tmp/xhprof
```

On redémarre Apache :

```

$ sudo /etc/init.d/zend-server restart-apache
```

Un phpinfo() doit normalement afficher l'extension xhprof.

On va tester rapidement que cela fonctionne en essayant de profiler un script PHP. Pour profiler il est nécessaire d'ajouter quelques lignes de code dans le script PHP. Vous verrez ensuite une technique pour l'ajouter de manière automatique sur l'ensemble des scripts PHP (via xhprof gui) :

```

<?php
...
xhprof_enable();

/**
 * your application code
 * ......
 * ......
 */

$xhprof_data = xhprof_disable();
$xhprof_root = '/chemin/vers/le/repertoire/xhprof-0.9.2/';
include_once $xhprof_root . "xhprof_lib/utils/xhprof_lib.php";
include_once $xhprof_root . "xhprof_lib/utils/xhprof_runs.php";
$xhprof_runs = new XHProfRuns_Default();
$run_id = $xhprof_runs->save_run($xhprof_data, "xr");
```

L'exécution de ce script devrait générer un fichier dans le répertoire /tmp/xhprof. Si oui, l'installation de l'extension xhprof est ok.

Visualiser l'analyse de vos scripts
-----------------------------------

xhprof propose une interface de consultation des "profiling" effectués. Cette application (xhprof gui) est disponible dans un [dépôt git](https://github.com/preinheimer/xhprof "xhprof gui").

![Xhprof gui](https://franek.chicour.net/public/xhprof/.XHGuiRun_m.jpg "Xhprof gui, avr. 2011")

Actuellement, elle possède quelques dysfonctionnements (plantage lors de l'analyse d'un script trop important) mais qui peuvent être résolus.

Pour installer *xhprof gui*, vous pouvez suivre la procédure d'installation :

```

git clone https://github.com/preinheimer/xhprof.git
cd xhprof
ln -s xhprof_lib/utils/xhprof_runs_mysql.php xhprof_runs.php
mv xhprof_lib/config.sample.php xhprof_lib/config.php
```

*Xhprof gui* propose de stocker les éléments d'analyse dans une base (mysql, mssql, ...). Dans notre exemple, nous allons utiliser mysql.

On crée une base pour xhprof :

```

$ mysql -uroot -p
mysql > create database xhprof;
```

*xhprof gui* a besoin d'une table *details* dans la base xhprof. La description de la table est décrite dans le fichier [Mysqli](https://github.com/preinheimer/xhprof/blob/master/xhprof_lib/utils/Db/Mysqli.php).

```

 CREATE TABLE `details` (
`id` char(17) NOT NULL,
`url` varchar(255) default NULL,
`c_url` varchar(255) default NULL,
`timestamp` timestamp NOT NULL default CURRENT_TIMESTAMP on update CURRENT_TIMESTAMP,
`server name` varchar(64) default NULL,
`perfdata` MEDIUMBLOB,
`type` tinyint(4) default NULL,
`cookie` BLOB,
`post` BLOB,
`get` BLOB,
`pmu` int(11) unsigned default NULL,
`wt` int(11) unsigned default NULL,
`cpu` int(11) unsigned default NULL,
`server_id` char(3) NOT NULL default 't11',
`aggregateCalls_include` varchar(255) DEFAULT NULL,
PRIMARY KEY (`id`),
KEY `url` (`url`),
KEY `c_url` (`c_url`),
KEY `cpu` (`cpu`),
KEY `wt` (`wt`),
KEY `pmu` (`pmu`),
KEY `timestamp` (`timestamp`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8;
```

Il est ensuite nécessaire de créer un Virtual Host pour accéder à *xhprof gui* :

```

<VirtualHost *:80>
   DocumentRoot /mon/super/chemin/vers/xhprofgui/xhprof_html
   ServerName xhprof.local
   DirectoryIndex index.php
</VirtualHost>
```

N'oubliez pas de l'activer et d'ajouter dans votre fichier /etc/hosts une entrée pour ce nouveau domaine.

Il est nécessaire de modifier le fichier xhprof\_lib/config.php avec les paramètres qui vont bien.

Voici les premières lignes du fichier config.php que j'utilise :

```

<?php
$_xhprof = array();

// Change these:
$_xhprof['dbhost'] = 'localhost';
$_xhprof['dbuser'] = 'root';
$_xhprof['dbpass'] = 'root';
$_xhprof['dbname'] = 'xhprof';
$_xhprof['servername'] = 'myserver';
$_xhprof['namespace'] = 'myapp';
$_xhprof['url'] = 'http://xhprof.local/';

//These are good for linux and its derivatives.
//*
$_xhprof['dot_binary']  = '/usr/bin/dot';
$_xhprof['dot_tempdir'] = '/tmp';
$_xhprof['dot_errfile'] = '/tmp/xh_dot.err';
//*/

$exceptionURLs = array();

$exceptionPostURLs = array();
$exceptionPostURLs[] = "login";


$_xhprof['display'] = false;
$_xhprof['doprofile'] = true;

$controlIPs = array();
$controlIPs[] = "127.0.0.1";   //Localhost, you'll want to add your own ip here
$controlIPs[] = "ma super ip personnelle";   // Je bosse sous Windows (on ne choisit pas toujours...) mais mon serveur est dans une VM. J'indique l'IP de mon Windows.

$otherURLS = array();

$weight = 100;
```

Ensuite pour tous les virtual hosts que vous souhaiteraient monitorer, vous pouvez ajouter les lignes suivantes dans la configuration du VH :

```

php_admin_value auto_prepend_file "/mon/super/chemin/vers/xhprofgui/external/header.php"
```

Désormais en bas de chaque page, vous disposerez normalement d'un lien permettant d'accéder au profiling de la page courante.

Dernier point, si vous souhaitez générer des graphiques de ce type ![xhprof gui callgraph](https://franek.chicour.net/public/xhprof/.XHGuiCallGraph_m.jpg "xhprof gui callgraph, avr. 2011"), il est nécessaire d'installer graphviz :

```

$ sudo apt-get install graphviz
```

J'espère que ces quelques notes vous aiderons à débuter avec xhprof.

Cet article s'est largement inspiré de [profiling php application](http://css.dzone.com/news/profiling-php-application "Profiling php application")?

Edit 27/11/2012 : Correction suite à commentaire d'un visiteur.
