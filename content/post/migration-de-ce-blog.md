---
title: "Migration de ce blog"
date: 2021-01-02T21:34:13+01:00
cover:
    image: "/public/migration-blog-the-nigmatic-68RMbT06_ro-unsplash.jpg"
    alt: "Migration d'oiseaux"
    caption: "source: https://unsplash.com/photos/68RMbT06_ro"
    relative: false
tags: ["dotclear", "blog", "hugo", "markdown"]
---

Ce blog a longtemps été propulsé par le moteur de blog [Dotclear](http://www.dotclear.org), un moteur de blog écrit en PHP développé par des français (Olivier Meunier au départ, [Franck Paul](https://open-time.net/) désormais). Il est désormais propulsé par [Hugo](https://gohugo.io/).

J'ai beaucoup utilisé Dotclear, je l'ai beaucoup aimé. 
A l'époque l'organisation du code PHP de Dotclear était bien meilleure que celle de Wordpress (j'avoue n'avoir pas regardé le code de Wordpress aujourd'hui). Un effort particulier était fait sur l'accessibilité.
Plusieurs audits accessibilités avaient été réalisés sur le back-office et sur les principaux thèmes.

La communauté (proche de celle de Paris-Web) semblait chouette.

Le projet "Dotclear" est toujours maintenu. Des mises à jour continuent d'arriver (Merci Franck) mais personnellement, je souhaitais passer à autre chose. 

Dans un esprit "low-tech", je ne souhaitais plus dépendre d'un serveur PHP ou d'une base de données pour héberger un contenu qui ne bouge quasiment pas.

Les contenus de ce site sont désormais écrits dans des fichiers textes au format Markdown. Je dois lancer une moulinette (`hugo --minify`) pour générer ce site et quelques autres commandes git pour le publier.

Les pages générées sont hébergées sur Github via les [Github Pages](https://pages.github.com/) mais je pourrais très bien faire de l'auto-hébergement et l'héberger sur un minuscule serveur vu le peu de visiteurs et le peu de ressources nécessaires pour juste servir une page HTML et ses médias. Cela fera l'objet d'une future mission...

En passant à Hugo, je perds quelques fonctionnalités comme les commentaires. Si vous avez à me contacter, vous pouvez toujours utiliser le mail franek [à] chicour [point] net.

Pour ceux qui souhaiteraient migrer de Dotclear à Hugo, voici les quelques étapes que j'ai réalisées.

Il est à noter que Dotclear dispose de sa propre syntaxe "wiki2xhtml" pour écrire ses billets. Depuis plusieurs versions, il est possible d'écrire au format Markdown mais j'ai un historique d'articles qui étaient encore écrits dans ce format.

Il y a quelques années, je m'étais lancé dans l'écriture d'un plugin de conversion de "wiki2xhtml" vers Markdown mais je ne l'ai jamais terminé (ni vraiment commencé d'ailleurs).

Pour effectuer la migration, je suis donc parti du contenu HTML exposé dans le flux RSS pour générer l'ensemble des articles.
Il existe plusieurs scripts Python qui font ça mais tous ceux que j'ai testés avaient de petits problèmes (non support de certaines balises, ...) et je me retrouvais avec une perte d'informations dans certains billets. J'ai donc écrit rapidement mon propre [script de migration](https://github.com/franek/dotclear2hugo). Il n'est clairement pas parfait mais il a fonctionné pour moi.

En très rapide, les étapes que j'ai réalisées pour la migration sont : 

1. Configurer Dotclear afin que l'ensemble des articles soient exposés dans le flux ATOM

![Configuration dotclear](/public/migration-blog-conf-dotclear.png)

Les options importantes sont : 
 * "Afficher 200 billets par flux de syndication" (si vous avez plus de billets, vous devez augmenter cette valeur).
 * Décocher "Tronquer les flux de syndication"


2. Installer le script de migration

``` 
$ git clone git@github.com:franek/dotclear2hugo.git
$ cd dotclear2hugo
$ composer install
``` 

3. Exécuter le script afin d'exporter le contenu au format Markdown

``` 
php bin/console dotclear2hugo -f https://blog.domain.com/feed/atom
``` 

4. Installer `gohugo` et déplacer le répertoire `content/post` dans le répertoire `content` de l'installation de gohugo

5. Récupérer l'ensemble des médias de Dotclear et les copier dans le répertoire `static` de l'installation de gohugo.

6. Configurer Hugo et le déployer.

La peinture est fraîche, il reste encore des petites choses à faire mais le gros de la migration est fait.

Vous aurez peut-être la chance d'avoir d'autres billets de blog cette année 👋.
