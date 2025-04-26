---
title: "Devoxx 2025"
date: 2025-04-26T14:34:13+01:00
cover:
    image: "/public/devoxx-2025/accueil-devoxx.png"
    alt: "Logo de la page d'accueil de la Devoxx"
    relative: false
tags: ["Devoxx", "2025", "conférence"]
---

Pour la première fois, j'ai participé la semaine dernière à la [Devoxx](https://www.devoxx.fr/), la plus grande conférence indépendante autour du développement. 

Toutes les thématiques qu'un développeur rencontre dans son quotidien étaient représentées (de l'IA, au front, en passant par le DevOps, le platform engineering, le cloud, le quantique ou encore le management). C'était très riche. Comme d'habitude dans ce genre d'événement, j'aimerais disposer du don d'ubiquité afin de pouvoir assister aux différentes sessions qui ont lieu simultanément. Ce n'est pas encore mon cas, mais j'y travaille ! 🙂

L'événement, qui dure 3 jours, regroupe **4 500 personnes** par jour. Il y a donc du monde, beaucoup de monde.

La Devoxx a initialement été créée par l'association [Paris Java User Group (JUG)](https://www.parisjug.org/). Les "JAVA-istes" sont donc sur-représentés. Je ne viens pas de cette communauté, mais j'ai quand même trouvé énormément de matières intéressantes.

Il est à noter qu'en plus des sessions, une [zone "Exposants"](https://www.devoxx.fr/sponsors/sponsors-2025/) regroupe une centaine d'entreprises ou de partenaires.

Durant les 3 jours, j'ai assisté à une trentaine de conférences (d'une durée de 15 minutes à 45 minutes). Il était possible de participer à des sessions d'approfondissement de 2h ou 3h, mais j'ai préféré privilégier des sessions plus courtes.  
Ayant, par le passé, participé à beaucoup de conférences, j'ai trouvé la qualité globale des conférenciers excellente. Je n'ai en tête que deux conférences où la forme était décevante. Il est vrai que j'ai privilégié les grosses salles, et les organisateurs avaient sûrement été attentifs au choix des conférenciers dans ces salles.

C'est parti pour un compte-rendu rapide des différentes sessions.

# Jour 1

Luc Julia, co-créateur de Siri, l'assistant vocal d'Apple, lance la première keynote avec un sujet sur l'IA : ["L’Intelligence Artificielle n’existe pas"](https://www.devoxx.fr/agenda-2025/talk/l-intelligence-artificielle-n-existe-pas/).  
Nous ne pouvons qu'adhérer à son discours mêlant histoire de l'évolution des technologies autour de l'Intelligence Artificielle et anecdotes personnelles (parfois sur le ton de l'humour).  
Selon lui, l'IA n'est qu'un outil qu'il faut apprendre à manier. L'IA n'est pas créative par essence, mais créative grâce au maniement de ce nouvel outil par les humains. Il rappelle également les problématiques de copyright autour des données utilisées pour l'entraînement.

Changement de contexte, je pars écouter Clément de Tastes ["Coder avec peu : les bons tuyaux de Mario"](https://www.devoxx.fr/agenda-2025/talk/coder-avec-peu-les-bons-tuyaux-de-mario/), qui nous plonge dans le fonctionnement de Super Mario Bros sur NES et comment les développeurs ont créé ce jeu malgré de fortes contraintes matérielles (peu de CPU, peu de RAM, voire peu de stockage). C'est didactique et très intéressant, j'apprends plein de choses.  
Si vous souhaitez vous plonger dans cet univers avant la publication des vidéos, Clément de Tastes avait déjà présenté [cette conférence](https://blog.sciam.fr/2024/05/30/Coder-avec-peu-les-bons-tuyaux-de-Mario.html).

Durant les 3 jours, la thématique de l'observabilité était bien représentée. Alexandre Moray et Florian Meuleman de la société Takima nous ont fait un [retour d'expérience](https://www.devoxx.fr/agenda-2025/talk/l-observabilite-pour-les-devs-outils-cle-pour-survivre-quand-la-prod-plantera/) sur l'intégration d'OpenTelemetry sur leurs projets en présentant les outils permettant de faire de l'instrumentation automatique ou du filtrage des données d'observabilité via le Collector OpenTelemetry.

Les métriques étaient envoyées dans une solution open-source, [Signoz](https://signoz.io/). Signoz est une alternative à NewRelic ou Datadog, mais uniquement orientée OpenTelemetry. Il est possible d'héberger ses propres instances de Signoz.  
À titre professionnel, je n'ai pas encore basculé sur OpenTelemetry, mais cette présentation m'a de nouveau donné envie de m'y intéresser. La technologie semble de plus en plus mature.

Durant le déjeuner, [Denis Germain](https://blog.zwindler.fr/) nous propose en quelques minutes son approche pour sauvegarder ses photos de vacances ["Ne perdez plus vos photos de vacances 🔥🏠🔥 (ou tout autre fichier important)"](https://www.devoxx.fr/agenda-2025/talk/ne-perdez-plus-vos-photos-de-vacances-ou-tout-autre-fichier-important/).  
Son support de présentation est [disponible](https://blog.zwindler.fr/talks/2025-3-2-1/index.html#2). Je retiens de mon côté de tester la solution [Duplicati](https://github.com/duplicati/duplicati).

L'après-midi débute avec l'intervention de Damien Lucas ["Vol au-dessus d'un nid de vulnérabilités"](https://www.devoxx.fr/agenda-2025/talk/vol-au-dessus-d-un-nid-de-vulnerabilites). Il nous rappelle les solutions disponibles pour générer des SBOM (Software Bills Of Materials) à partir de nos builds ainsi que les différences entre les différents formats (SPDX soutenu par la Linux Foundation et CycloneDX par l'OWASP).  
Ces SBOMs peuvent être exploités par des solutions comme [DependencyTrack](https://dependencytrack.org/).

[Daniel Garnier-Moiroux](https://garnier.wf/) présente ["OAuth2 & OpenID : sous le capot"](https://www.devoxx.fr/agenda-2025/talk/oauth2-openid-sous-le-capot). En quelques minutes, Daniel code en JAVA une authentification basée sur un fournisseur d'identité OIDC (ici Google, mais il montre que le code fonctionne pour d'autres fournisseurs d'identité). C'est didactique et super clair. J'avais vu l'an passé la conférence de Julien Topçu "[OAuth 2.1 expliqué simplement (même si tu n'es pas un dev)](https://www.youtube.com/watch?v=vuJl27bOmV0)". Ces deux conférences sont complémentaires et je les recommande vivement.

En 45 minutes, Alain Reignier nous présente les nouveautés de Kubernetes ["Kubernetes en 2025"](https://www.devoxx.fr/agenda-2025/talk/kubernetes-en-2025/). Alain Reignier est CTO de la société "Kubo Labs", qui développe :  
* [KuboScore](https://www.kuboscore.io/client#iss=https%3A%2F%2Fklas.kubolabs.io%2Frealms%2Fmain), un outil permettant de détecter des problèmes de configuration sur les clusters Kubernetes  
* [KuboVisor](https://www.kubovisor.io/), un centre de contrôle de l'ensemble de vos clusters qui s'appuie sur KuboScore (j'imagine)

Dans les nouveautés, je retiens :  
* NGINX a annoncé le passage en maintenance du NGINX Ingress Controller. Cela signifie que l'Ingress Controller le plus utilisé ne va plus recevoir de nouvelles versions. Cela devrait avoir pour incidence d'accélérer le passage à la [Gateway API](https://gateway-api.sigs.k8s.io/). La Gateway API a de chouettes fonctionnalités. Il va falloir planifier la migration.  
![](/public/devoxx-2025/20250426144750.png)  
* [Kueue](https://kueue.sigs.k8s.io/docs/overview/)  
![](/public/devoxx-2025/20250426144736.png)

Avant-dernière session de la journée, [Christophe Furmaniak](https://www.devoxx.fr/agenda-2025/talk/introduction-aux-tests-avec-terraform-test) introduit le framework de tests "terraform test" et compare les différentes solutions disponibles pour tester les scripts Terraform.  
C'est une découverte et cela ouvre des perspectives pour améliorer son code Terraform.

Enfin, pour terminer, [Antoine Mayer](https://www.devoxx.fr/agenda-2025/talk/exegol-le-hacking-a-base-de-conteneurs) nous partage son amour pour Exegol. [Exegol](https://exegol.readthedocs.io/en/latest/) est une alternative à la distribution de sécurité [Kali Linux](https://www.kali.org/) basée sur Docker. La solution semble facile à prendre en main et j'ai hâte de la tester pour vérifier la sécurité de nos applications. 🙂

# Jour 2

Le deuxième jour, j’espérais pouvoir assister à la keynote depuis l'amphi bleu, la plus grande salle. Bien que j'arrive 15-20 minutes avant le début des festivités, je me retrouve dans une des salles "Overflow" qui diffusent la keynote. 🙂
J'essaierais de faire mieux le lendemain.

Je passe sur les keynotes qui étaient très bien mais difficiles à synthétiser en quelques mots.

Je pars assister au retour d'expérience de Criteo ["Evolution continue de clusters Kubernetes/NOSQL supportant 300 Millions de QPS"](https://www.devoxx.fr/agenda-2025/talk/evolution-continue-de-clusters-kubernetes-nosql-supportant-300-millions-de-qps/). L'infrastructure de Criteo repose sur environ 11 000 noeuds Kubernetes, près de 100 000 containers. Les intervenants détaillent les solutions utilisées pour mettre à jour les 11 000 noeuds en limitant au maximum les impacts.
Il présente notamment leur [Node Disruption Controller](https://github.com/criteo/node-disruption-controller) permettant de s'assurer que la maintenance sur un noeud pourra être réalisée en limitant les impacts sur les applications utilisant des PVC. Intéressant mais mon cluster de production avec 40 noeuds en pic de charge fait pâle figure. 

![](/public/devoxx-2025/20250423220418.png)

Je reste dans la thématique Kubernetes et je pars écouter Denis Germain (encore) nous dévoiler "[Kubernetes : 5 façons créatives de flinguer sa prod 🔫](https://www.devoxx.fr/agenda-2025/talk/kubernetes-5-facons-creatives-de-flinguer-sa-prod/)".
Ses slides sont [disponibles](https://blog.zwindler.fr/talks/2025-kubernetes-5-facon-de-flinguer-prod/index.html).
Super conférence, il arrive à rendre simple de vrais problèmes qui ont dû être complexes à régler. J'aurais aimé avoir encore plus d'anecdotes. J'ai découvert l'intérêt de [Talos](https://www.talos.dev/), qui permet d'avoir un OS dédié à Kubernetes minimal et immutable (coucou Martin Fowler - [Immutable Server](https://martinfowler.com/bliki/ImmutableServer.html)).

![](/public/devoxx-2025/20250423220708.png)

Je profite de la pause de midi pour aller écouter ["Maîtrisez son infrastructure mail en 2025 : anti-spam et auto-hébergement"](https://www.devoxx.fr/agenda-2025/talk/maitrisez-son-infrastructure-mail-en-2025-anti-spam-et-auto-hebergement/) par Guillaume LAPIERRE. Guillaume LAPIERRE nous rappelle les éléments à prendre en compte pour améliorer la délivrabilité des mails. A l'issue de la présentation, SPF, DKIM, DMARC n'avaient plus de secrets pour les auditeurs.
![](/public/devoxx-2025/20250423222223.png)

Je découvre ensuite le retour d'expérience de Bedrock sur l'utilisation de [Gatling](https://gatling.io/) afin d'effectuer des tests de charge sur la plate-forme M6+ ["Load-testons M6+ pour préparer l’Euro 2024 !"](https://www.devoxx.fr/agenda-2025/talk/load-testons-m6-pour-preparer-l-euro-2024/).

Thierry Chantier nous embarque ensuite dans le merveilleux monde des interfaces utilisateur textuelles (Textual User Interface - TUI): ["Quand le Terminal dévore la UI : TUI pour tout le monde !"](https://www.devoxx.fr/agenda-2025/talk/quand-le-terminal-devore-la-ui-tui-pour-tout-le-monde/).
La conférence est super fluide. Il nous partage quelques librairies en Python, Go ou Rust pour développer des TUI. Cela semble relativement simple et ça donne vraiment envie de développer ce type d'interface.

Retour dans l'amphi Bleu pour écouter "[Vos requêtes SQL jusqu'à 10000 plus rapides, durablement](https://www.devoxx.fr/agenda-2025/talk/vos-requetes-sql-jusqu-a-10000-fois-plus-rapides-durablement)" par Alain Lesage de la société [Dalibo](https://www.dalibo.com/). A nouveau, super conférence sur les performances des bases de données. Alain rappelle qu'optimiser une base de données est un vrai métier (DBA) et que ce métier tend à disparaître alors qu'il est essentiel pour la pérennité du modèle de données ou les performances.
Il partage des ressources développées par Dalibo : 
 * [explain.dalibo.com](https://explain.dalibo.com/): un outil permettant de visualiser un EXPLAIN PLAN
 * [kb.dalibo.com](https://kb.dalibo.com/): la base de connaissance de Dalibo autour de PostgreSQL

J'assiste au [quizz d'Aurélie Vache et Sherine Khoury sur le containers](https://www.devoxx.fr/agenda-2025/talk/question-pour-un-conteneur-quiz-sur-les-images-les-conteneurs-oci-docker/) puis je pars découvrir "[Infisical : Le meilleur ami des devs pour des secrets bien gardés !](https://www.devoxx.fr/agenda-2025/talk/infisical-le-meilleur-ami-des-devs-pour-des-secrets-bien-gardes/)" par Julien Briault.
[Infisical](https://infisical.com/) est une alternative à Hashicorp Vault qui semble pertinente suite au changement de licences de Hashicorp Vault. A tester au retour au travail. 

Le mercredi soir, la Devoxx propose une nocturne "Meet & Greet" avec des sessions organisées par les associations communautaires mais j'ai d'autres engagements.

# Jour 3

Le troisième jour débute avec, à nouveau, 2 keynotes. 

Comme les jours précédents, malgré mes 20-25 minutes d'avances, je me retrouve dans une salle "Overflow" à suivre les keynotes par écran interposé. 

La première session nous plonge dans l'univers de l'informatique Quantique ["Plongez dans l’Ère Quantique : décryptez et anticipez la révolution à venir"](https://www.devoxx.fr/agenda-2025/talk/plongez-dans-l-ere-quantique-decryptez-et-anticipez-la-revolution-a-venir/). Fanny Bouton nous synthétise en quelques minutes où nous en sommes autour de l'informatique Quantique (Spoiler: il nous reste encore 10-15 ans à attendre afin que la technologie se démocratise). Elle nous invite à s'intéresser au sujet afin de ne pas louper le coche.
Je repars 20 ans en arrière. Lorsque durant mes études j'avais dû faire une synthèse de 2 pages sur cette future révolution. 😊

Je passe sur la deuxième keynote qui ne m'a pas marqué.

Je reste dans ce superbe "Amphi bleu" pour assister à ["Astro GitOps - Press ⓧ to start"](https://www.devoxx.fr/agenda-2025/talk/astro-gitops-press-to-start/) par Kévin DAVIN. En quelques minutes, Kévin nous partage sa vision du GitOps. Ses slides sont [disponibles](https://download.davinkevin.fr/presentations/astrogitops/devoxxfr-2025/slides.pdf). Cela va vite, peut-être trop vite. Il faut s'accrocher.
Pour lui, simplement stocker des scripts Bash dans Git n'est pas une pratique GitOps (of course!) car cela ne gère pas un state et donc un état immutable.

Je découvre [Google Config Connector](https://cloud.google.com/config-connector/docs/overview) chez GKE en alternative à [Crossplane](https://www.crossplane.io/) afin de gérer ses ressources GCP depuis des manifests Kubernetes.
Il nous recommande de ne pas utiliser de Vault (comme Hashicorp Vault) mais de plutôt stocker ses secrets directement en les chiffrant avec [Mozilla SOPS](https://getsops.io/). La conférence était très chouette.

Je reste dans l'"Amphi Bleu" pour écouter ["Platform Engineering : DevOps est maintenant majeur"](https://www.devoxx.fr/agenda-2025/talk/platform-engineering-devops-est-maintenant-majeur/) par des représentants de la société [WeScale](https://www.wescale.fr/). Je suis persuadé que le "Platform Engineering" est une évolution des pratiques "DevOps". Le sujet m'intéresse mais je reste sur ma fin. Le rythme est trop lent malgré la parfaite connaissance du sujet des intervenants.
Je reste marqué par l'introduction : 
> DevOps: the devs run their shit
> 
> Platform : a guy creates stuff to let the devs run their shit

C'est déjà la pause déjeuner et Sébastien Ferrer nous présentre ["Une identité pour les fédérer toutes !"](https://www.devoxx.fr/agenda-2025/talk/une-identite-pour-les-federer-toutes/) une synthèse en 15 minutes du fonctionnement des protocoles SAML et OIDC.

Fin de la pause déjeuner, je participe à l'une des meilleures conférences des 3 jours "[Staff Engineer : Les défis, les galères, et comment les surmonter](https://www.devoxx.fr/agenda-2025/talk/staff-engineer-les-defis-les-galeres-et-comment-les-surmonter/)". La conférence est parfaite. Ane Naiz en a fait une synthèse en image:

![](/public/devoxx-2025/20250425215300.png)
(source : https://bsky.app/profile/ane-naiz.bsky.social/post/3lnfacvc4dc25)

Je rejoins "[Retour d'expérience : migrer une application critique vers le cloud](https://www.devoxx.fr/agenda-2025/talk/retour-d-experience-migrer-une-application-critique-vers-le-cloud/)". Antoine Irisson et Bernard Pons nous content avec beaucoup d'humour la migration du système de réservation d'ACCOR vers AWS. On rigole beaucoup. Antoine et Bernard nous rappellent qu'un projet migration est un long chemin semé d'embûches mais qui en général se termine bien.

Retour dans l'"Amphi Bleu" pour écouter "[Au secours ! Mon manager me demande des KPIs !](https://www.devoxx.fr/agenda-2025/talk/au-secours-mon-manager-me-demande-des-kpis/)" puis direction "[Du full text search dans PostgreSQL !](https://www.devoxx.fr/agenda-2025/talk/du-full-text-search-dans-postgresql/)" afin de terminer les 3 jours denses du Devoxx. 
Cette dernière session me permet de découvrir les fonctionnalités de recherche de PostgreSQL que je peux mettre en parallèle avec les implémentations que nous avons pu faire avec Elasticsearch. C'est une bonne introduction à l'outil.


# Conclusion

En 3 jours, j'ai fait ma veille technique sur plein de sujets. 
J'ai néanmoins quelques regrets. 

J'ai loupé les conférences de:
* Julien Briault "[Comme nous avons transformé les Restos du Coeur en Cloud Provider](https://speakerdeck.com/ju_hnny5/devoxx-france-2025-comment-transformons-nous-les-restos-du-coeur-en-cloud-provider)", 
* d'Olivier Poncet "[Anatomie d'une faille](https://www.devoxx.fr/agenda-2025/talk/anatomie-d-une-faille/)", 
* de Jérôme Pettazoni et Sandra Ahlgrimm "[Déployer une app de genAI sur Kubernetes sans perdre le contrôle de ses données](https://www.devoxx.fr/agenda-2025/talk/deployer-une-app-de-genai-sur-kubernetes-sans-perdre-le-controle-de-ses-donnees/)" 
* et sûrement plein d'autres. 

Il faudra que je prenne le temps de les regarder en replay (Spoiler: je ne le fais jamais).

J'ai découvert tardivement que d'autres copainnngggs étaient présents sur le site et je n'ai pas pu les croiser.

En attendant le début d'une conférence, mes oreilles indiscrètes ont capté une conversation (vraisemblablement) de dev JAVA critiquant le langage PHP. Je ne suis pas intervenu, il y avait une réelle méconnaissance des évolutions du langage (qui se rapproche de plus en plus de JAVA). 
L'informatique, c'est une autre histoire de religions, avec ses différentes chapelles (les devs JAVA, les devs PHP, les fans de Windows, Linux ou Apple, les Product Owners, les sysadmins, ...). 

La Devoxx arrive à regrouper tout ce joli monde et le fait plutôt bien.

Bravo aux organisateurs (bénévoles). C'était cool. Je reviendrais. 

# Pour en savoir plus

D'autres retours sur la conférence, on était écrit : 
* [Zwindler"s Reflection](https://blog.zwindler.fr/2025/04/17/devoxxfr-2025-recap-jour-1/)
* [JoliCode](https://jolicode.com/blog/devoxx-2025-3-jours-intenses-pour-parler-de-securite-cloud-ux-et-ia) 👋
* [Julien Wittouck](https://codeka.io/2025/04/24/devoxx-2025-bilan/)
* ...


