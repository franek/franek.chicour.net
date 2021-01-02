---
date: 2010-02-26T14:46:00+01:00
title: "Zend Server 5 et Oracle"
author: ["franek"]
aliases: [/post/2010/02/26/Zend-Server-5-et-Oracle]
tags: ["développement web", "encodage", "oracle", "php", "Zend", "Zend Platform", "Zend Server"]
lastmod: 2011-10-16T15:11:23+02:00
---
[Zend Server](http://www.zend.com/fr/products/server/) vient de sortir en version 5. Zend Server est le remplaçant de la Zend Platform.

Par défaut, Zend Server est fourni avec le client Oracle Instant Client Lite qui ne prend pas en charge les bases de données Oracle avec des encodages un peu exotique (WE8ISO8859P15, par exemple) :

> ZS is shipped with the OCI library Lite version which only supports OCI and OCCI for US locales only. You may download the full version from Oracle's site and replace the current libraries shipped with ZendServer with those, they are API and ABI compatible so you should have no issues.

Si comme moi, vous disposez de bases Oracle dans ce type d'encodage, il est nécessaire d'installer un client Oracle Basic et d'indiquer à Zend Server le chemin vers ce client Oracle.

Voici la procédure :

- [Téléchanger](http://www.oracle.com/technology/software/tech/oci/instantclient/index.html) instantclient-sdk-linux32-11.2.0.1.zip and instantclient-basic-linux32-11.2.0.1.zip
- Décompressez les 2 archives. Cela va créer un répertoire : instantclient\_11\_2
- Copier le répertorie dans /usr/local/oracle/
- Créer un lien symbolique ln -s instantclient\_11\_2/ instantclient
- Ajouter dans le fichier /etc/apache2/envvars

> export LD\_LIBRARY\_PATH=/usr/local/oracle/instantclient:/usr/local/zend/lib  
> export ORACLE\_HOME=/usr/local/oracle/instantclient

- Redémarrer Apache.

Cela devrait fonctionner.
