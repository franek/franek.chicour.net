---
date: 2011-10-10T13:21:00+02:00
title: "Jenkins : Respect des conventions de codage Javascript avec JSLint"
author: "franek"
aliases: [/post/2011/10/10/Jenkins-%3A-Respect-des-conventions-de-codage-Javascript-avec-JSLint]
tags: ["développement web", "intégration continue", "jenkins", "jslint", "phing", "php"]
lastmod: 2011-10-23T17:00:15+02:00
---
Imaginons que vous disposez d'une plate-forme d'intégration continue (idéalement Jenkins ou Hudson) pour vos projets PHP (si ce n'est pas le cas, je vous invite à lire les excellents billets de Pascal Martin :[ Intégration continue avec Jenkins : installation et configuration de base](http://blog.pascal-martin.fr/post/integration-continue-jenkins-installation-configuration) et [Intégration continue d'un projet PHP avec Jenkins](http://blog.pascal-martin.fr/post/integration-continue-jenkins-projet-php)).

Imaginons que vous n'utilisez pas Ant comme outil d'automatisation (de build) mais plutôt Phing parce que vous maîtrisez cet outil.

Imaginons que vous souhaitez également vérifier la qualité de vos développement Javascript (Dans un projet PHP, vous avez sûrement un peu de Javascript, non ?) et que vous souhaitez disposer d'indicateur de suivi de la qualité dans Jenkins.

Il existe plusieurs outils pour vérifier la qualité de son code Javascript :

- [Jslint](http://www.jslint.com/) de Douglas Crockford
- [jslint4java](http://code.google.com/p/jslint4java/) un portage de jslint de Douglas Crockford en Java
- [Google Closure Linter](http://code.google.com/intl/fr/closure/utilities/) un outil développé par Google
- [JsHint](http://jshint.org/) un fork de Jslint
- [Javascript Lint](http://www.javascriptlint.com/) dit JSL est un portage de jslint en Python.

L'outil JSL n'a pas évolué depuis 2007. Il nécessite d'être installé en suivant l'[une de ces procédures](http://ioconnor.wordpress.com/2009/05/02/javascriptlint-vim-and-ubuntu/). Avantage, il existe une [tâche Phing pour exécuter JSL](http://www.phing.info/docs/guide/stable/chapters/appendixes/AppendixC-OptionalTasks.html#JslLintTask). Inconvénient, il n'est pas possible de générer un fichier XML compréhensible par Jenkins.

Je n'ai pas regardé Google Closure Linter.

JSHint semble intéressant. Mais à nouveau, il ne semble pas y avoir de mécanisme simple permettant de l'intégrer à Jenkins.

Jslint ne permet pas, a priori, nativement de générer un fichier XML compréhensible par Jenkins.

Je me suis donc tourné vers [jslint4java](http://code.google.com/p/jslint4java/). Je me suis inspiré du travail de [Stephen Rees](http://stephen.rees-carter.net/2011/05/jenkins-ci-jslint-javascript-quality-checking/) (qui utilise Ant) pour implémenter l'exécution de Jslint avec phing.

Voici le résultat :

```

    <!-- Fichier temporaire contenant la liste des fichiers JS à traiter avec JSLint -->
    <property name="temp_file_all_js" value="/tmp/${phing.project.name}/all_js.txt" override="true" />     

    <!-- Chemin vers Jslint4java -->
    <property name="jslint4java" value="/chemin/vers/jslint4java/jslint4java-2.0.0.jar" override="true" />     

    <!-- création d'un patternset contenant l'ensemble des fichiers JS à analyser -->
    <!-- on exclut les fichiers JQuery et les fichiers minimifiés -->
    <patternset id="js_files">
        <include name="public/js/**/*.js"/>
        <exclude name="public/js/**/*-min.js"/>
        <exclude name="public/js/jquery*.js"/>
    </patternset>

   <!-- ============================================  -->
    <!--   (jslint) Target: vérification syntaxe JS    -->
    <!-- attention à créer au préalable un patternset  -->
    <!-- ayant pour nom js_files                        -->
    <!-- ============================================  -->
    <target name="jslint">
        
        <!-- créer le repertoire de stockage du fichier temporaire -->
        <!-- s'il n'existe pas                                     -->
        <php function="dirname" returnProperty="temp_dir">
            <param value="${temp_file_all_js}"/>
        </php>
        <mkdir dir="${temp_dir}" />
        
        <!-- crée un fichier temporaire contenant la liste des fichiers JS à traiter -->
        <!-- cette liste se base sur le patternset refid=js_files -->
        <foreach param="filename" absparam="absfilename" target="_createFilesetText">
            <fileset dir="${install_dir}">
                <patternset refid="js_files" />
            </fileset>
        </foreach>
    
        <!-- on charge le contenu de temp_file_all_js dans la variable ${all_js} -->
        <loadfile property="all_js" file="${temp_file_all_js}"/>
        <echo>Fichiers analysés par JSLint : ${all_js}</echo>
        
        <!-- exécution de jslint4java                       -->
        <!-- browser permet de définir les variables du navigateur dans le contexte d'exécution -->
        <!-- prefed permet de définir les variables dans le contexte d'exécution -->
        <!-- voir : http://code.google.com/p/jslint4java/source/browse/jslint4java-docs/src/main/resources/cli.html -->
        <exec 
            command="java -jar ${jslint4java}
                     --browser --predef $,document,jQuery
                     --report xml
                     ${all_js} > ${builddir}/logs/jslint.xml" 
            passthru="true" 
        />
        
        <delete file="${temp_file_all_js}" />
    </target>

   <!-- ============================================  -->
    <!--   _createFilesetText Target:                  -->
    <!-- stocke la liste des fichiers JS à traiter     -->
    <!-- dans le fichier /tmp/all_js.txt               -->
    <!-- ============================================  -->
    <target name="_createFilesetText" >
        <echo file="${temp_file_all_js}" append="true">${absfilename} </echo>
    </target>

```

Vous devez ensuite appeler cette tâche dans votre tâche principale de build. Quelque chose comme ça :

```

<target name="build">
        <echo msg="tâche build" />
        <phingcall target="php-doc" />
        <phingcall target="pdepend"/>
        <phingcall target="phpmd"/>
        <phingcall target="phpcpd"/>
        <phingcall target="phploc"/>
        <phingcall target="php-cs" />
	<phingcall target="php-cb" />
	<phingcall target="phpunit" />
       <!-- on lance la vérification syntaxique de JS -->
        <phingcall target="jslint" />
 </target>
```

Vous pourrez ensuite configurer dans Jenkins l'appel du fichier de log (build/log/jslint.xml) : [![Jenkins - Configuration JSlint](https://franek.chicour.net/public/jenkins/.jenkins_configuration_m.jpg "Jenkins - Configuration JSlint, oct. 2011")](https://franek.chicour.net/public/jenkins/jenkins_configuration.png "Jenkins - Configuration JSlint")

Après l'exécution du build, vous devriez avoir dans le menu Violations, quelque chose comme ça : [![jenkins - violation JSLint](https://franek.chicour.net/public/jenkins/.jenkins_violation_m.jpg "jenkins - violation JSLint, oct. 2011")](https://franek.chicour.net/public/jenkins/jenkins_violation.png "jenkins - violation JSLint")
