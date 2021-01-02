---
date: 2009-12-29T22:20:00+01:00
title: "Amélioration du \"post script\" de backup-manager"
author: ["franek"]
aliases: [/post/2009/12/29/Am%C3%A9lioration-du-post-script-de-backup-manager]
tags: ["geek", "backup", "backup-manager", "hook", "linux", "sauvegarde"]
lastmod: 2010-08-17T13:36:24+02:00
---
[backup-manager](http://www.backup-manager.org/) est un script très pratique permettant de faire la sauvegarde d'un serveur dédié. Ce script est utilisé pour effectuer la sauvegarde de la dédibox qui héberge [ce site](http://franek.chicour.net) et [ces satellites](http://www.chicour.net). Par défaut, ce script ne propose pas de contrôle des fichiers déposés sur le serveur de sauvegarde ou d'envoi d'un email lors de la fin de l'exécution de la sauvegarde.

Il est possible d'ajouter des fonctionnalités à ce script via des hooks exécutés avant ou après la sauvegarde. [Alsacréations](http://www.alsacreations.com) propose un [exemple de hook](http://www.alsacreations.com/tuto/lire/618-Sauvegarde-backup-manager.html) permettant d'envoyer un mail à la fin de l'exécution de la sauvegarde. Malheureusement, ce script ne vérifie pas que les fichiers ont bien été déposés sur le serveur de sauvegarde et que les fichiers sont bien complets. Ce script n'est utile que si la méthode d'upload est FTP. Dans le cadre d'une autre méthode d'upload (rsync, par exemple), le contrôle peut être exécuté nativement.

J'ai donc adapté le script d'alsacréations.

```
<pre class="php php" style="font-family:inherit">#!/usr/bin/php
<span style="color: #000000; font-weight: bold;"><?php</span>
<span style="color: #009933; font-style: italic;">/**
 * backup-manager post script :
 *  - permet de vérifier l'intégrité des fichiers uploadés sur le serveur de sauvegarde
 *    (comparaison des chaines md5)
 *  - envoie d'un mail récapitulatif contenant la liste des fichiers et la taille totale utilisée
 *
 * @references script inspiré de Alsacréation : http://www.alsacreations.com/tuto/lire/618-Sauvegarde-backup-manager.html
 * @autor Franek <franek at chicour dot net>
 */</span>
 
<span style="color: #009933; font-style: italic;">/**
 * Configuration
 */</span>
<span style="color: #666666; font-style: italic;"># email des destinataires
</span><span style="color: #000088;">$email_dest</span> <span style="color: #339933;">=</span> <span style="color: #990000;">array</span><span style="color: #009900;">(</span>dest<span style="color: #339933;">@</span>domain<span style="color: #339933;">.</span>com<span style="color: #0000ff;">');
# répertoire local de stockage des fichiers de sauvegarde
$archives_dir = '</span><span style="color: #339933;">/</span><span style="color: #000000; font-weight: bold;">var</span><span style="color: #339933;">/</span>archives<span style="color: #0000ff;">';
# adresse du serveur FTP
$ftp_server = '</span><span style="color: #0000ff;">';
# identifiant du serveur FTP
$ftp_user_name = '</span><span style="color: #0000ff;">';
# mot de passe du serveur FTP
$ftp_user_pass = '</span><span style="color: #0000ff;">';
 
/**
 * Ne pas modifier - ci-dessous
 */
 
/**
 *
 * Envoi d'</span>un <span style="color: #990000;">mail</span>
 <span style="color: #339933;">*</span>
 <span style="color: #339933;">*</span> <span style="color: #339933;">@</span>param <span style="color: #990000;">array</span> <span style="color: #000088;">$email_dest</span>
 <span style="color: #339933;">*</span> <span style="color: #339933;">@</span>param string <span style="color: #000088;">$subject</span>
 <span style="color: #339933;">*</span> <span style="color: #339933;">@</span>param string <span style="color: #000088;">$content</span>
 <span style="color: #339933;">*/</span>
<span style="color: #000000; font-weight: bold;">function</span> sendMail<span style="color: #009900;">(</span><span style="color: #000088;">$email_dest</span><span style="color: #339933;">,</span> <span style="color: #000088;">$subject</span><span style="color: #339933;">,</span> <span style="color: #000088;">$content</span><span style="color: #009900;">)</span>
<span style="color: #009900;">{</span>
    <span style="color: #b1b100;">foreach</span><span style="color: #009900;">(</span><span style="color: #000088;">$email_dest</span> <span style="color: #b1b100;">as</span> <span style="color: #000088;">$dest</span><span style="color: #009900;">)</span>
    <span style="color: #009900;">{</span>
        <span style="color: #990000;">mail</span><span style="color: #009900;">(</span><span style="color: #000088;">$dest</span><span style="color: #339933;">,</span> <span style="color: #000088;">$subject</span><span style="color: #339933;">,</span> <span style="color: #000088;">$content</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">}</span>
<span style="color: #009900;">}</span>
 
<span style="color: #009933; font-style: italic;">/**
 * Récupère la liste des fichiers présents en local pour une date donnée
 * @param $archives_dir string répertoire de stockage des fichiers
 * @param $filtre_date string date à filtrer (format YYYYMMDD)
 * @return array
 */</span>
<span style="color: #000000; font-weight: bold;">function</span> getLocalFiles<span style="color: #009900;">(</span><span style="color: #000088;">$archives_dir</span><span style="color: #339933;">,</span> <span style="color: #000088;">$filtre_date</span><span style="color: #009900;">)</span>
<span style="color: #009900;">{</span>
	<span style="color: #990000;">clearstatcache</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
 
	<span style="color: #000088;">$files</span> <span style="color: #339933;">=</span> <span style="color: #990000;">array</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
	<span style="color: #b1b100;">foreach</span> <span style="color: #009900;">(</span><span style="color: #000000; font-weight: bold;">new</span> DirectoryIterator<span style="color: #009900;">(</span><span style="color: #000088;">$archives_dir</span><span style="color: #009900;">)</span> <span style="color: #b1b100;">as</span> <span style="color: #000088;">$file_info</span><span style="color: #009900;">)</span>
	<span style="color: #009900;">{</span>
	    <span style="color: #b1b100;">if</span><span style="color: #009900;">(</span><span style="color: #000088;">$file_info</span><span style="color: #339933;">-></span><span style="color: #004000;">isDot</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span> <span style="color: #339933;">||</span> <span style="color: #339933;">!</span><span style="color: #990000;">preg_match</span><span style="color: #009900;">(</span><span style="color: #0000ff;">'/'</span><span style="color: #339933;">.</span><span style="color: #990000;">date</span><span style="color: #009900;">(</span><span style="color: #0000ff;">'Ymd'</span><span style="color: #009900;">)</span><span style="color: #339933;">.</span><span style="color: #0000ff;">'/'</span><span style="color: #339933;">,</span><span style="color: #000088;">$file_info</span><span style="color: #339933;">-></span><span style="color: #004000;">getFileName</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #009900;">)</span><span style="color: #009900;">)</span>
	    <span style="color: #009900;">{</span>
		<span style="color: #b1b100;">continue</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">}</span>
	    <span style="color: #000088;">$file</span><span style="color: #009900;">[</span><span style="color: #0000ff;">'name'</span><span style="color: #009900;">]</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$file_info</span><span style="color: #339933;">-></span><span style="color: #004000;">getFilename</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
	    <span style="color: #666666; font-style: italic;">// on utilise cette commande car filesize ne gère pas les fichiers de plus de 2Go.</span>
            <span style="color: #000088;">$file</span><span style="color: #009900;">[</span><span style="color: #0000ff;">'size'</span><span style="color: #009900;">]</span> <span style="color: #339933;">=</span> <span style="color: #990000;">exec</span><span style="color: #009900;">(</span><span style="color: #0000ff;">"stat -c <span style="color: #009933; font-weight: bold;">%s</span> '"</span><span style="color: #339933;">.</span><span style="color: #000088;">$file_info</span><span style="color: #339933;">-></span><span style="color: #004000;">getPathname</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #339933;">.</span><span style="color: #0000ff;">"'"</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
            <span style="color: #000088;">$files</span><span style="color: #009900;">[</span><span style="color: #009900;">]</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$file</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">}</span>	
	<span style="color: #990000;">sort</span><span style="color: #009900;">(</span><span style="color: #000088;">$files</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
	<span style="color: #b1b100;">return</span> <span style="color: #000088;">$files</span><span style="color: #339933;">;</span>
<span style="color: #009900;">}</span>
 
<span style="color: #009933; font-style: italic;">/**
 *
 * Compare le hachage md5 des fichiers locaux avec les fichiers envoyés
 * sur le serveur FTP
 * Si le hachage est identique, renvoie true.
 * Sinon, renvoie false
 *
 * @param string $md5_file
 * @param string $ftp_server
 * @param string $ftp_user_name
 * @param string $ftp_user_pass
 * @param string $filtre_date
 * @return bool
 */</span>
<span style="color: #000000; font-weight: bold;">function</span> verifMd5Ftp<span style="color: #009900;">(</span><span style="color: #000088;">$md5_file</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_server</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_user_name</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_user_pass</span><span style="color: #339933;">,</span> <span style="color: #000088;">$filtre_date</span><span style="color: #009900;">)</span>
<span style="color: #009900;">{</span>
	<span style="color: #000088;">$handle</span> <span style="color: #339933;">=</span> <span style="color: #990000;">fopen</span><span style="color: #009900;">(</span><span style="color: #000088;">$md5_file</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">"r"</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
	<span style="color: #b1b100;">if</span> <span style="color: #009900;">(</span><span style="color: #000088;">$handle</span> <span style="color: #339933;">!==</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #009900;">)</span>
        <span style="color: #009900;">{</span>
		<span style="color: #b1b100;">while</span> <span style="color: #009900;">(</span><span style="color: #339933;">!</span><span style="color: #990000;">feof</span><span style="color: #009900;">(</span><span style="color: #000088;">$handle</span><span style="color: #009900;">)</span><span style="color: #009900;">)</span> 
		<span style="color: #009900;">{</span>
	        	<span style="color: #000088;">$buffer</span> <span style="color: #339933;">=</span> <span style="color: #990000;">fgets</span><span style="color: #009900;">(</span><span style="color: #000088;">$handle</span><span style="color: #339933;">,</span> <span style="color: #cc66cc;">4096</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
	        	<span style="color: #990000;">list</span><span style="color: #009900;">(</span><span style="color: #000088;">$md5</span><span style="color: #339933;">,</span> <span style="color: #000088;">$filename</span><span style="color: #009900;">)</span> <span style="color: #339933;">=</span> <span style="color: #990000;">explode</span><span style="color: #009900;">(</span><span style="color: #0000ff;">"  "</span><span style="color: #339933;">,</span> <span style="color: #000088;">$buffer</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
			<span style="color: #666666; font-style: italic;">// pour supprimer /n</span>
			<span style="color: #000088;">$filename</span> <span style="color: #339933;">=</span> <span style="color: #990000;">trim</span><span style="color: #009900;">(</span><span style="color: #000088;">$filename</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
			<span style="color: #b1b100;">if</span> <span style="color: #009900;">(</span><span style="color: #339933;">!</span><span style="color: #990000;">empty</span><span style="color: #009900;">(</span><span style="color: #000088;">$filename</span><span style="color: #009900;">)</span><span style="color: #009900;">)</span>
			<span style="color: #009900;">{</span>
				<span style="color: #b1b100;">if</span> <span style="color: #009900;">(</span><span style="color: #000088;">$md5</span> <span style="color: #339933;">!==</span> getMd5OverFtp<span style="color: #009900;">(</span><span style="color: #000088;">$filename</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_server</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_user_name</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_user_pass</span><span style="color: #009900;">)</span><span style="color: #009900;">)</span>
				<span style="color: #009900;">{</span>
					<span style="color: #990000;">fclose</span><span style="color: #009900;">(</span><span style="color: #000088;">$handle</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
					<span style="color: #b1b100;">return</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">;</span>
				<span style="color: #009900;">}</span>
			<span style="color: #009900;">}</span>
		<span style="color: #009900;">}</span>
	<span style="color: #990000;">fclose</span><span style="color: #009900;">(</span><span style="color: #000088;">$handle</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">}</span>
        <span style="color: #b1b100;">else</span>
        <span style="color: #009900;">{</span>
            <span style="color: #b1b100;">return</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">}</span>
	<span style="color: #b1b100;">return</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #339933;">;</span>
<span style="color: #009900;">}</span>
 
<span style="color: #009933; font-style: italic;">/**
 *
 * Renvoie le hachage md5 d'un fichier présent sur le serveur FTP de sauvegarde
 *
 * @param string $file fichier dont le md5 doit être calculé
 * @param string $ftp_server adresse du serveur FTP de sauvegarde
 * @param string $ftp_user_name identifiant de connexion du serveur FTP
 * @param string $ftp_user_pass mot de passe de connexion du serveur FTP
 * @return string
 */</span>
<span style="color: #000000; font-weight: bold;">function</span> getMd5OverFtp<span style="color: #009900;">(</span><span style="color: #000088;">$file</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_server</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_user_name</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_user_pass</span><span style="color: #009900;">)</span>
<span style="color: #009900;">{</span>
	<span style="color: #000088;">$connect_string</span>  <span style="color: #339933;">=</span> <span style="color: #0000ff;">'ftp://'</span><span style="color: #339933;">;</span>
	<span style="color: #000088;">$connect_string</span> <span style="color: #339933;">.=</span> <span style="color: #000088;">$ftp_user_name</span><span style="color: #339933;">;</span>
	<span style="color: #b1b100;">if</span> <span style="color: #009900;">(</span><span style="color: #339933;">!</span><span style="color: #990000;">empty</span><span style="color: #009900;">(</span><span style="color: #000088;">$ftp_user_pass</span><span style="color: #009900;">)</span><span style="color: #009900;">)</span>
	<span style="color: #009900;">{</span>
		<span style="color: #000088;">$connect_string</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">':'</span><span style="color: #339933;">.</span><span style="color: #000088;">$ftp_user_pass</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">}</span>
	<span style="color: #000088;">$connect_string</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">'@'</span><span style="color: #339933;">.</span><span style="color: #000088;">$ftp_server</span><span style="color: #339933;">;</span>
	<span style="color: #000088;">$connect_string</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">'/'</span><span style="color: #339933;">.</span><span style="color: #000088;">$file</span><span style="color: #339933;">;</span>
	<span style="color: #b1b100;">return</span> <span style="color: #990000;">md5_file</span><span style="color: #009900;">(</span><span style="color: #000088;">$connect_string</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
<span style="color: #009900;">}</span>
 
 
<span style="color: #009933; font-style: italic;">/**
 * Renvoie la taille du fichier en un format compréhensif
 *
 * source : http://fr.php.net/manual/en/function.filesize.php (nak5ive at DONT-SPAM-ME dot gmail dot com)
 *
 * @param int $bytes
 * @param int $precision
 * @return string
 */</span>
<span style="color: #000000; font-weight: bold;">function</span> formatBytes<span style="color: #009900;">(</span><span style="color: #000088;">$bytes</span><span style="color: #339933;">,</span> <span style="color: #000088;">$precision</span> <span style="color: #339933;">=</span> <span style="color: #cc66cc;">2</span><span style="color: #009900;">)</span>
<span style="color: #009900;">{</span>
    <span style="color: #000088;">$units</span> <span style="color: #339933;">=</span> <span style="color: #990000;">array</span><span style="color: #009900;">(</span><span style="color: #0000ff;">'B'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'KB'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'MB'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'GB'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'TB'</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
 
    <span style="color: #000088;">$bytes</span> <span style="color: #339933;">=</span> <span style="color: #990000;">max</span><span style="color: #009900;">(</span><span style="color: #000088;">$bytes</span><span style="color: #339933;">,</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
    <span style="color: #000088;">$pow</span> <span style="color: #339933;">=</span> <span style="color: #990000;">floor</span><span style="color: #009900;">(</span><span style="color: #009900;">(</span><span style="color: #000088;">$bytes</span> ? <span style="color: #990000;">log</span><span style="color: #009900;">(</span><span style="color: #000088;">$bytes</span><span style="color: #009900;">)</span> <span style="color: #339933;">:</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">)</span> <span style="color: #339933;">/</span> <span style="color: #990000;">log</span><span style="color: #009900;">(</span><span style="color: #cc66cc;">1024</span><span style="color: #009900;">)</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
    <span style="color: #000088;">$pow</span> <span style="color: #339933;">=</span> <span style="color: #990000;">min</span><span style="color: #009900;">(</span><span style="color: #000088;">$pow</span><span style="color: #339933;">,</span> <span style="color: #990000;">count</span><span style="color: #009900;">(</span><span style="color: #000088;">$units</span><span style="color: #009900;">)</span> <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
 
    <span style="color: #000088;">$bytes</span> <span style="color: #339933;">/=</span> <span style="color: #990000;">pow</span><span style="color: #009900;">(</span><span style="color: #cc66cc;">1024</span><span style="color: #339933;">,</span> <span style="color: #000088;">$pow</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
 
    <span style="color: #b1b100;">return</span> <span style="color: #990000;">round</span><span style="color: #009900;">(</span><span style="color: #000088;">$bytes</span><span style="color: #339933;">,</span> <span style="color: #000088;">$precision</span><span style="color: #009900;">)</span> <span style="color: #339933;">.</span> <span style="color: #0000ff;">' '</span> <span style="color: #339933;">.</span> <span style="color: #000088;">$units</span><span style="color: #009900;">[</span><span style="color: #000088;">$pow</span><span style="color: #009900;">]</span><span style="color: #339933;">;</span>
<span style="color: #009900;">}</span>
 
 
<span style="color: #009933; font-style: italic;">/**
 * début du script
 */</span>
<span style="color: #000088;">$date</span> <span style="color: #339933;">=</span> <span style="color: #990000;">date</span><span style="color: #009900;">(</span><span style="color: #0000ff;">'Ymd'</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
<span style="color: #000088;">$host</span> <span style="color: #339933;">=</span> <span style="color: #990000;">trim</span><span style="color: #009900;">(</span><span style="color: #990000;">file_get_contents</span><span style="color: #009900;">(</span><span style="color: #0000ff;">'/etc/hostname'</span><span style="color: #009900;">)</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
<span style="color: #666666; font-style: italic;"># fichier contenant les chaines md5 de tous les fichiers sauvegardés
</span><span style="color: #000088;">$md5_file</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$archives_dir</span><span style="color: #339933;">.</span><span style="color: #0000ff;">'/'</span><span style="color: #339933;">.</span><span style="color: #000088;">$host</span><span style="color: #339933;">.</span><span style="color: #0000ff;">'-'</span><span style="color: #339933;">.</span><span style="color: #000088;">$date</span><span style="color: #339933;">.</span><span style="color: #0000ff;">'.md5'</span><span style="color: #339933;">;</span>
<span style="color: #000088;">$check_md5_ftp</span> <span style="color: #339933;">=</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">;</span>
 
<span style="color: #990000;">clearstatcache</span><span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
 
<span style="color: #000088;">$local_files</span> <span style="color: #339933;">=</span> getLocalFiles<span style="color: #009900;">(</span><span style="color: #000088;">$archives_dir</span><span style="color: #339933;">,</span> <span style="color: #000088;">$date</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
<span style="color: #b1b100;">if</span><span style="color: #009900;">(</span><span style="color: #990000;">empty</span><span style="color: #009900;">(</span><span style="color: #000088;">$local_files</span><span style="color: #009900;">)</span><span style="color: #009900;">)</span>
<span style="color: #009900;">{</span>
	<span style="color: #000088;">$output</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">' - Fichiers non présents en local (attention : cela peut venir d\'un problème de droit).'</span><span style="color: #339933;">.</span><span style="color: #0000ff;">"<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">;</span>
<span style="color: #009900;">}</span>
<span style="color: #b1b100;">else</span>
<span style="color: #009900;">{</span>
	<span style="color: #000088;">$output</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">' - Fichiers présents en local :'</span><span style="color: #339933;">.</span><span style="color: #0000ff;">"<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">;</span>
	<span style="color: #000088;">$total_size</span> <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// affichage de la liste des fichiers avec leur taille et un total global</span>
	<span style="color: #b1b100;">foreach</span><span style="color: #009900;">(</span><span style="color: #000088;">$local_files</span> <span style="color: #b1b100;">as</span> <span style="color: #000088;">$file</span><span style="color: #009900;">)</span>
	<span style="color: #009900;">{</span>
		<span style="color: #000088;">$output</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">'   # '</span><span style="color: #339933;">.</span><span style="color: #000088;">$file</span><span style="color: #009900;">[</span><span style="color: #0000ff;">'name'</span><span style="color: #009900;">]</span><span style="color: #339933;">;</span>
		<span style="color: #000088;">$output</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">' ('</span><span style="color: #339933;">.</span>formatBytes<span style="color: #009900;">(</span><span style="color: #000088;">$file</span><span style="color: #009900;">[</span><span style="color: #0000ff;">'size'</span><span style="color: #009900;">]</span><span style="color: #009900;">)</span><span style="color: #339933;">.</span><span style="color: #0000ff;">')'</span><span style="color: #339933;">;</span>
		<span style="color: #000088;">$output</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">"<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">;</span>
		<span style="color: #000088;">$total_size</span> <span style="color: #339933;">+=</span> <span style="color: #000088;">$file</span><span style="color: #009900;">[</span><span style="color: #0000ff;">'size'</span><span style="color: #009900;">]</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">}</span>
	<span style="color: #000088;">$output</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">"<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">.</span><span style="color: #0000ff;">'   # TOTAL : '</span><span style="color: #339933;">.</span>formatBytes<span style="color: #009900;">(</span><span style="color: #000088;">$total_size</span><span style="color: #009900;">)</span><span style="color: #339933;">.</span><span style="color: #0000ff;">"<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">;</span>
 
        <span style="color: #666666; font-style: italic;">// lance la vérification md5 des fichiers uploadés sur le serveur FTP</span>
	<span style="color: #000088;">$check_md5_ftp</span> <span style="color: #339933;">=</span> verifMd5Ftp<span style="color: #009900;">(</span><span style="color: #000088;">$md5_file</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_server</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_user_name</span><span style="color: #339933;">,</span> <span style="color: #000088;">$ftp_user_pass</span><span style="color: #339933;">,</span> <span style="color: #000088;">$filtre_date</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
	<span style="color: #b1b100;">if</span> <span style="color: #009900;">(</span><span style="color: #000088;">$check_md5_ftp</span> <span style="color: #339933;">===</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #009900;">)</span>
	<span style="color: #009900;">{</span>
		<span style="color: #000088;">$output</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">' - problème d\'intégrité dans les fichiers transmis sur le serveur FTP'</span><span style="color: #339933;">.</span><span style="color: #0000ff;">"<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">}</span>
	<span style="color: #b1b100;">else</span>
	<span style="color: #009900;">{</span>
		<span style="color: #000088;">$output</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">' - intégrité des fichiers sur le serveur FTP vérifiés.'</span><span style="color: #339933;">.</span><span style="color: #0000ff;">"<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">}</span>
<span style="color: #009900;">}</span>
 
<span style="color: #666666; font-style: italic;">// construction du sujet du mail</span>
<span style="color: #000088;">$subject</span> <span style="color: #339933;">=</span> <span style="color: #0000ff;">'['</span><span style="color: #339933;">.</span><span style="color: #000088;">$host</span><span style="color: #339933;">.</span><span style="color: #0000ff;">']'</span><span style="color: #339933;">;</span>
<span style="color: #b1b100;">if</span> <span style="color: #009900;">(</span><span style="color: #000088;">$check_md5_ftp</span> <span style="color: #339933;">===</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">)</span>
<span style="color: #009900;">{</span>
	<span style="color: #000088;">$subject</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">' backup ok'</span><span style="color: #339933;">;</span>
<span style="color: #009900;">}</span>
<span style="color: #b1b100;">else</span>
<span style="color: #009900;">{</span>
	<span style="color: #000088;">$subject</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">' backup ko'</span><span style="color: #339933;">;</span>
<span style="color: #009900;">}</span>
 
sendMail<span style="color: #009900;">(</span><span style="color: #000088;">$email_dest</span><span style="color: #339933;">,</span> <span style="color: #000088;">$subject</span><span style="color: #339933;">,</span> <span style="color: #000088;">$output</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
<span style="color: #000000; font-weight: bold;">?></span>
```

Vous pouvez copier ce script dans /etc/backup-manager-post.php et lui donner les droits :

```

chmod +x /etc/backup-manager-post.php
```

Pour ajouter le hook à backup-manager, vous devez modifier le fichier de configuration /etc/backup-manager.conf et ajouter :

```

export BM_POST_BACKUP_COMMAND="/etc/backup-manager-post.php" 
```
