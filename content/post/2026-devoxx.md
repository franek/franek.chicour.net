---
title: "Devoxx 2026"
date: 2026-05-01T14:34:13+01:00
cover:
    image: "/public/devoxx-2026/devoxx_2026.webp"
    alt: "Robot illustrant la Devoxx 2026"
    relative: false
tags: ["Devoxx", "2026", "conférence"]
---

Pour la seconde année ([voir mon compte-rendu 2025](/post/2025-devoxx/)), j'ai participé à la [Devoxx](https://www.devoxx.fr/), la plus grande conférence indépendante autour du développement et de la programmation.

Durant les 3 jours, c'est près de 5 000 personnes qui déambulent dans les couloirs du Palais de la musique et des congrès de Paris et assistent à différentes sessions (15 minutes, 30 minutes, 45 minutes, voire même des sessions longues de 2 ou 3 heures).

Toutes les composantes du développement logiciel (back, front, tests, gestion de projets, gestion des équipes, ...) sont représentées et c'est chouette de naviguer parmi tous ces sujets.

Étant donné que la conférence est indépendante et organisée par des bénévoles, il y a peu de conférences "Marketing" où des sociétés vont venir vanter leurs produits (ou en tout cas, je ne l'ai pas ressenti).

Chaque journée débute par 2 keynotes dans le grand Amphi Bleu. Malgré mon arrivée matinale, je n'ai jamais réussi à atteindre cet amphi. Les organisateurs nous proposent de suivre les sessions par écran interposé dans des salles "Overflow". C'est moins confortable et un peu dommage de venir sur place pour regarder une conférence sur un écran mais bon...

Toutes les Keynotes avaient pour thème (directement ou indirectement...) : l'IA...
Si vous ne deviez en regarder que 2, je vous conseille :
* "[Le développeur face à l'IA : du prototypage rapide à la fin des intermédiaires ?](https://m.devoxx.com/events/devoxxfr2026/talks/149102/le-dveloppeur-face-lia-du-prototypage-rapide-la-fin-des-intermdiaires-)" de Nicolas Grenié (Typeform)
* "[La course à l’IA : La France risque-t-elle de devenir un "territoire servant"?](https://m.devoxx.com/events/devoxxfr2026/talks/149104/la-course-lia-la-france-risquetelle-de-devenir-un-territoire-servant)" de Loup Cellard : J'ai beaucoup aimé cette conférence sur le développement des datacenters en France. Loup nous a expliqué pourquoi il pense que nous sommes actuellement dans une bulle spéculative (comme on a pu avoir une bulle spéculative pour l'immobilier d'entreprise). Il s'est attardé sur les villes de Marseille et Bordeaux, expliquant pourquoi ces villes avaient été choisies pour accueillir de nombreux datacenters (de nombreux câbles sous-marins arrivent dans ces villes). Il a terminé par expliquer qu'il y avait de plus en plus de conflits de ressources (eau, électricité) dans les villes où des datacenters sont créés et que les territoires doivent de plus en plus prendre des décisions concernant la fourniture de l'eau/électricité (vers la population ou vers les entreprises 😨 ?).

Après les keynotes, c'est le début des conférences avec plusieurs sessions en parallèle. Le choix est souvent difficile. C'est parti pour un condensé de quelques conférences auxquelles j'ai participé.

## La conférence sur une technologie qui fait tourner le web

En une quinzaine de minutes, Paul Jeannot nous a présenté [Comment le protocole BGP fait fonctionner Internet —et peut le faire disparaître](https://m.devoxx.com/events/devoxxfr2026/talks/91525/comment-le-protocole-bgp-fait-fonctionner-internet-et-peut-le-faire-disparatre). Paul nous a expliqué rapidement comment le routage d'Internet fonctionne. Il a notamment détaillé le rôle des [AS (Autonomous System)](https://fr.wikipedia.org/wiki/Autonomous_System). Tout le monde connait le rôle critique des DNS mais certains incidents récents sont dûs à BGP ([exemple Facebook en 2021](https://fr.wikipedia.org/wiki/Panne_de_Facebook_(2021))).
C'était une chouette conférence pour aborder le sujet.

## La conférence que j'aurais pu présenter

[Mirakl](https://www.mirakl.com/fr-FR), une société qui développe des solutions de synchro de catalogue et de gestion des ventes sur les principales Marketplace du marché (Leroy Merlin, ...) a dû migrer l'an passé sa solution d'envoi d'emails. Une migration qui aurait pu être vue comme technique et rapide s'est révélée bien plus complexe. 
Julien Goullon et Julien Eyraud nous racontent cette histoire de migration dans [Email at scale : comment on a survécu à 800M mails/an (et au DNS)](https://m.devoxx.com/events/devoxxfr2026/talks/65319/email-at-scale-comment-on-a-survcu-800m-mailsan-et-au-dns).

Ils nous expliquent avec franchise les galères qu'ils ont rencontrées au niveau de la configuration DNS (SPF, DKIM, DMARC) avec les particularités du protocole DNS (par exemple, le protocole DNS ne permet pas d'avoir à la fois un enregistrement TXT et un enregistrement CNAME pour le même nom de domaine), le préchauffage des IPs pour la réputation, le nettoyage des listes de contact afin de limiter les Bounces, ...

Ayant effectué une migration d'ampleur de ce type cette année (*Au revoir [Brevo](https://www.brevo.com/fr/), Bonjour [AirShip](https://www.airship.com/)*), cette conférence a pleinement raisonné chez moi.

## Les conférences qui donnent envie de tester de nouvelles choses

Plusieurs conférences présentaient des outils que j'ai bien envie d'approfondir.

Rémi Verchère dans [Mise : un multi-outil pour votre poste de Dev & Ops](https://m.devoxx.com/events/devoxxfr2026/talks/34401/mise-un-multioutil-pour-votre-poste-de-dev-ops) nous a présenté les outils [mise-en-place](https://mise.jdx.dev/) (qu'on pourrait voir comme un remplaçant de Makefile) et [fnox](https://github.com/jdx/fnox) (qu'on pourrait voir comme un remplaçant de direnv). J'avais déjà lu avec intérêt la [présentation de Julien Wittouck](https://codeka.io/2025/12/19/adieu-direnv-bonjour-mise/) sur mise-en-place ou de [Korben](https://korben.info/fnox-gestionnaire-de-secrets-dev.html) sur Fnox.

Entre temps, Rémi a publié un [article sur son blog synthétisant sa conférence](https://www.vrchr.fr/posts/2026/04/28/mise-en-place-fnox-setup-multi-projets/).

Les deux mainteneurs principaux de Docker Compose (Nicolas De Loof et Guillaume Lours) ont présenté les nouveautés de Docker Compose durant [Docker Compose votre Dev Toolkit pour AI & Cloud](https://m.devoxx.com/events/devoxxfr2026/talks/45204/docker-compose-votre-dev-toolkit-pour-ai-cloud). Ils ont parlé de [Docker Model Runner](https://docs.docker.com/ai/model-runner/) qui permet de simplifier le déploiement de modèle IA avec Docker et Docker Compose. Je n'avais pas suivi mais Docker Compose propose désormais [Compose Bridge](https://docs.docker.com/compose/bridge/) qui est un mécanisme permettant de déployer un projet Compose dans Kubernetes. En rédigeant ces notes, je me rends compte que Guillaume est derrière les [Docker Compose Tips](https://lours.me/posts/) 😄.

Thomas Rumas a, lors du dernier créneau du vendredi, présenté [DevContainers](https://containers.dev/). DevContainers est une solution développée par Microsoft qui permet de simplifier le démarrage d'un environnement local. C'est notamment la solution qui est derrière [GitHub Codespaces](https://github.com/features/codespaces). Thomas a montré comment il utilise cette technologie pour harmoniser les environnements de développement au sein d'[Adéo](https://www.adeo.com/) (la filiale informatique de Leroy Merlin).

## Une conférence sur la neutralité

J'aime beaucoup le [blog](https://eventuallycoding.com/) de Hugo Lassiège. Je ne pouvais donc pas passer à côté de sa conférence [Le mythe de la neutralité : quand la tech devient politique](https://m.devoxx.com/events/devoxxfr2026/talks/63923/le-mythe-de-la-neutralit-quand-la-tech-devient-politique).

Hugo est le fondateur de Malt (une plate-forme de mise en relation des freelances) qu'il a revendu depuis. Hugo a cherché à nous convaincre (l'étions-nous ?) que la technologie n'est pas neutre et qu'elle véhicule des biais.
Le numérique peut structurer la manière dont les personnes interagissent avec le monde. Il a évoqué l'importance de la souveraineté (à ne pas confondre avec l'autarcie). 

C'était chouette de l'entendre évoquer tout ça.

## La conférence Kubernetes

Avec des collègues, nous avons eu à plusieurs reprises des débats sur la manière de configurer les Limits et les Requests sur l'ensemble de nos applicatifs.
Suite à la lecture notamment de cet [article](https://home.robusta.dev/blog/stop-using-cpu-limits/?nocache=234), concernant la configuration des Requests et Limits, j'ai longtemps été partisan de définir :
* pour la mémoire, des Requests égales aux Limits 
* pour le CPU, des Requests mais pas de Limits pour éviter le throttling

Suite à des incidents sur notre infrastructure liés à des emballements de projets n'ayant pas de limits CPU et utilisant toutes les ressources de plusieurs noeuds, j'étais un peu revenu sur mes positions. 

Denis Germain et Quentin Joly, lors de la conférence [Limits, Requests, QoS, PriorityClasses, démystifions le scheduling dans K8s !](https://m.devoxx.com/events/devoxxfr2026/talks/2739/limits-requests-qos-priorityclasses-dmystifions-le-scheduling-dans-k8s-),  démystifient le sujet. C'est comme d'habitude avec Denis Germain très bien expliqué. Les démos sont parlantes. 

La conclusion est la suivante : 

![Takeaway de la conférence Kubernetes](/public/devoxx-2026/takeway-kubernetes.png)

Les slides sont [disponibles](https://blog.zwindler.fr/talks/2025-lrqppobcqvpsslsdk/lrqppobcqvpsslsdk_compressed.pdf).

## La conférence où on a pris le temps

Albane Fagot-Veyron nous pousse à questionner notre rapport au temps durant la conférence [⌛ Et si on débuguait notre rapport au temps ?](https://m.devoxx.com/events/devoxxfr2026/talks/32126/-et-si-on-dbuguait-notre-rapport-au-temps-). C'est interactif et assez amusant. Elle rappelle que notre cerveau n'est pas fait pour le multi-tâche, qu'il a besoin de pause pour se reconstruire. 

Denis résume bien sur [son blog la conférence](https://blog.zwindler.fr/2026/04/22/devoxxfr-2026-recap-jour-1/#-et-si-on-d%C3%A9buguait-notre-rapport-au-temps-) : 

> Ce que j’ai retenu :
> 
> - Le **temps perçu** n’est pas le temps réel. Enfant, le temps s’écoule lentement (tout est nouveau) ; adulte, il s’accélère. La maladie ralentit la perception. L’activité aussi.
> - On vit dans une **société de l’accélération** (Hartmut Rosa) : on remplit les espaces vides, on compresse le temps, on multitâche. Et on paie un prix fort : le context switching coûte jusqu’à 40 % de productivité, et laisse le cerveau épuisé en fin de journée au point que “la seule chose que j’arrive à faire, c’est scroller”. Je vois très bien ce qu’elle veut dire…
> - L’IA devait nous “faire gagner du temps” — et pourtant, les travaux exposés à l’IA constatent **+3h15 de travail par semaine en moyenne**. Là encore, je me retrouve à 100% dans ce constat. Je n’ai pas l’impression de travailler “moins” avec l’IA, au contraire.
> - Le **mode réseau par défaut** du cerveau (le “temps de rien”) est crucial. Sans lui, pas de récupération cognitive réelle. Le takeaway principal : **sanctuariser 5 minutes par jour, en silence, sans distraction**.
> - À l’échelle collective : interroger la culture de l’organisation, ses rythmes induits, pas juste ajouter de la flexibilité en surface. 


## Les conférences sur l'IA

Comme vous vous en doutez, il y avait beaucoup de conférences sur l'IA et l'Agentic Coding. J'ai beaucoup aimé la conférence de Doctolib [L'Agentic Coding, nouveau territoire du Platform Engineering](https://m.devoxx.com/events/devoxxfr2026/talks/51601/lagentic-coding-nouveau-territoire-du-platform-engineering) par Yanki Sesyilmaz et Julien Tanay. C'est pour moi l'une des meilleures de ces 3 jours. Elle était super inspirante en termes de pratique et d'organisation.
Yanki et Julien sont Platform Engineers chez Doctolib et conçoivent les outils permettant d'améliorer le quotidien des 600 développeurs du groupe. Ils expliquent qu'ils ont désormais une approche Agentic First. Ils ont fait le choix d'[Openspec](https://openspec.dev/) (en alternative à [speckit](https://github.com/github/spec-kit)) mais c'est une technologie qui serait facilement éjectable si le vent venait à tourner.
Afin de mesurer l'usage des nouveaux outils, ils mettent systématiquement en place de la télémétrie.
Tous les développeurs ont une licence Claude et ils partagent leurs skills via un plugin Claude (Marketplace).
Ils ont notamment une skill partagée pour la review (/review) qui permet d'intégrer le même niveau de qualité sur l'ensemble des projets.

## Les autres conférences que j'ai appréciées

La conférence de Sam Bellen [Bearer of Good News](https://m.devoxx.com/events/devoxxfr2026/talks/148101/bearer-of-good-news) sur les nouveautés de oauth 2.1 et ses extensions était chouette et mérite que j'approfondisse le sujet ([les slides](https://bearer.sambego.tech/#0)).

[Détectives de la prod : résoudre l’enquête avant le crash](https://m.devoxx.com/events/devoxxfr2026/talks/4018/dtectives-de-la-prod-rsoudre-lenqute-avant-le-crash) par Sébastien Ferrer donnait de nombreux tips intéressants pour améliorer la correction des problèmes liés au Run (vs Build).

[De développeur à hacker : savoir casser, c'est savoir protéger ⚔️](https://m.devoxx.com/events/devoxxfr2026/talks/19027/de-dveloppeur-hacker-savoir-casser-cest-savoir-protger-) par Florian Toulemont nous embarquait dans des outils pour approfondir la sécurité de nos applications.

## Conclusion

Vous l'aurez compris. J'ai à nouveau passé 3 jours riches à faire ma veille sur des sujets variés. C'était à nouveau un excellent cru. Je reviens avec de nouveaux outils à mettre en oeuvre ou des solutions à faire évoluer.

L'organisation était parfaite. Merci aux bénévoles qui assurent l'organisation. 

# Toutes les conférences auxquelles j'ai assisté :
## Mercredi 22 avril

* [Vous pensiez que la dette technique était le pire? Voici la dette de conception!](https://m.devoxx.com/events/devoxxfr2026/talks/4020/vous-pensiez-que-la-dette-technique-tait-le-pire-voici-la-dette-de-conception) par Julien Topçu et Josian Chevalier
* [Déployer d'abord, sécuriser jamais: l'IA entre productivité et chaos de sécurité](https://m.devoxx.com/events/devoxxfr2026/talks/85073/dployer-dabord-scuriser-jamais-lia-entre-productivit-et-chaos-de-scurit) par Houssem BELHADJ AHMED et Aymeric Lagier
* [Comment le protocole BGP fait fonctionner Internet —et peut le faire disparaître](https://m.devoxx.com/events/devoxxfr2026/talks/91525/comment-le-protocole-bgp-fait-fonctionner-internet-et-peut-le-faire-disparatre) par Paul Jeannot
* [⌛ Et si on débuguait notre rapport au temps ?](https://m.devoxx.com/events/devoxxfr2026/talks/32126/-et-si-on-dbuguait-notre-rapport-au-temps-) par Albane Fagot-Veyron
* [De zéro à des milliards de traces, le tracing distribué chez Winamax](https://m.devoxx.com/events/devoxxfr2026/talks/54230/de-zro-des-milliards-de-traces-le-tracing-distribu-chez-winamax) par Anthony Maffert et Nicolas Fidel
* [UDA (Unified Data Architecture) à Netflix](https://m.devoxx.com/events/devoxxfr2026/talks/44001/uda-unified-data-architecture-netflix) par Alexandre Bertails
* [Stop à la dette documentaire : Industrialisez vos ADRs et READMEs avec Spec-kit](https://m.devoxx.com/events/devoxxfr2026/talks/60505/stop-la-dette-documentaire-industrialisez-vos-adrs-et-readmes-avec-speckit) par Alexandre Guillemot et Axel Chauvin
* [Spécialisez vos Agents avec les Skills](https://m.devoxx.com/events/devoxxfr2026/talks/65339/spcialisez-vos-agents-avec-les-skills) par Tug Grall

## Jeudi 23 avril 

* [Gérer vos tickets support avec de l’IA mais sans cramer la planète](https://m.devoxx.com/events/devoxxfr2026/talks/45203/grer-vos-tickets-support-avec-de-lia-mais-sans-cramer-la-plante)par Matthieu Vincent et Philippe Charrière
* [L'Agentic Coding, nouveau territoire du Platform Engineering](https://m.devoxx.com/events/devoxxfr2026/talks/51601/lagentic-coding-nouveau-territoire-du-platform-engineering) par Yanki Sesyilmaz et Julien Tanay
* [Email at scale : comment on a survécu à 800M mails/an (et au DNS)](https://m.devoxx.com/events/devoxxfr2026/talks/65319/email-at-scale-comment-on-a-survcu-800m-mailsan-et-au-dns) par Julien Goullon et Julien Eyraud
* [Bearer of Good News](https://m.devoxx.com/events/devoxxfr2026/talks/148101/bearer-of-good-news) par Sam Bellen
* [Le mythe de la neutralité : quand la tech devient politique](https://m.devoxx.com/events/devoxxfr2026/talks/63923/le-mythe-de-la-neutralit-quand-la-tech-devient-politique) par Hugo Lassiège
* [Jujutsu, la cerise sur le git, oh !](https://m.devoxx.com/events/devoxxfr2026/talks/2719/jujutsu-la-cerise-sur-le-git-oh-) par Siegfried Ehret
* [Mise : un multi-outil pour votre poste de Dev & Ops](https://m.devoxx.com/events/devoxxfr2026/talks/34401/mise-un-multioutil-pour-votre-poste-de-dev-ops) par Rémi Verchère

## Vendredi 24 avril

* [Limits, Requests, QoS, PriorityClasses, démystifions le scheduling dans K8s !](https://m.devoxx.com/events/devoxxfr2026/talks/2739/limits-requests-qos-priorityclasses-dmystifions-le-scheduling-dans-k8s-) par Denis Germain et Quentin Joly
* [Docker Compose votre Dev Toolkit pour AI & Cloud](https://m.devoxx.com/events/devoxxfr2026/talks/45204/docker-compose-votre-dev-toolkit-pour-ai-cloud) par Nicolas De Loof et Guillaume Lours
* [Prolongez la vie de vos dashboards : Guide de survie anti-sapin de Noël](https://m.devoxx.com/events/devoxxfr2026/talks/9733/prolongez-la-vie-de-vos-dashboards-guide-de-survie-antisapin-de-nol) par Kamilla Giedrojc
* [Le DevOps est mort, vive le Platform Engineering !](https://m.devoxx.com/events/devoxxfr2026/talks/7899/le-devops-est-mort-vive-le-platform-engineering-) par Pierre Andrieux et Diogo Sobral
* [Détectives de la prod : résoudre l’enquête avant le crash](https://m.devoxx.com/events/devoxxfr2026/talks/4018/dtectives-de-la-prod-rsoudre-lenqute-avant-le-crash) par Sébastien Ferrer
* [De développeur à hacker : savoir casser, c'est savoir protéger ⚔️](https://m.devoxx.com/events/devoxxfr2026/talks/19027/de-dveloppeur-hacker-savoir-casser-cest-savoir-protger-) par Florian Toulemont
* [De la galère des setups locaux aux DevContainers : notre retour d'expérience.](https://m.devoxx.com/events/devoxxfr2026/talks/51650/de-la-galre-des-setups-locaux-aux-devcontainers-notre-retour-dexprience) par Thomas Rumas

