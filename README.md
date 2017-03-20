[![Build Status](https://travis-ci.org/iut-lille/jersey-skeleton.svg?branch=master)](https://travis-ci.org/iut-lille/jersey-skeleton)

# Squelette d'application web pour la semaine agile @ Univ-Lille

La semaine agile conclut la formation de DUT Informatique du département Informatique de l'IUT "A" de l'Université de Lille - Sciences & Technologies. L'objectif de cette semaine est l'initiation à la démarche agile via la conception d'une application web reposant sur un serveur `REST`, un client web (HTML, CSS et *JavaScript*) et un client mobile (*Androïd*).

Ce projet implique plusieurs technologies permettant de mettre en oeuvre une intégration continue, c'est-à-dire une automatisation de la vérification (via des tests) et du déploiement du logiciel en production.

Le squelette d'application web proposé ici repose sur l'exploitation de plusieurs technologies facilitant la conception, la compilation, l'éxecution des tests et le déploiement.

Pour ce qui concerne la gestion du cycle de vie du logiciel, voici les principaux outils mobilisés :
- [maven](https://maven.apache.org) pour décrire les dépendances et automatiser la construction, les tests et l'exécution d'un projet *Java*,
- [Travis CI](https://travis-ci.org) pour la gestion de l'intégration continue (ie. l'exécution des tests et le déploiement en cas de succès)
- [Docker](https://www.docker.com) pour la gestion du contexte applicatif permettant le déploiement de l'application créée (ie. un UNIX avec un serveur HTTP afin de déployer le serveur),

Pour ce qui est des librairies utilisées pour le développement de l'application web, voici les principales technologies :
- [Jersey](https://jersey.java.net) pour développer le serveur `REST` en *Java*, cette librairie étant l'implémentation du standard `JAX-RS` définissant l'API `REST` pour *Java*,
- [jQuery](https://jquery.com) pour faciliter la manipulation de l'arbre `DOM` et les appels `AJAX`,
- [Boostrap](http://getbootstrap.com) pour faciliter la gestion d'IHM adaptatives (ou *responsive* pour utiliser le terme à la mode ;)), 
- [Java Database Binding Interface](http://jdbi.org) (JDBI) pour faciliter la transition entre objets et base de données,

Le but de ce squelette est de fournir une base facilitant la prise en main de ces multiples techologies afin de pouvoir déployer votre projet dès le premier *sprint* :)

# Création d'un projet en mode étudiant

Sur ``Gitlab`` ou ``github`` :

- faire un *fork* du projet 
- ajouter ses camarades dans le projet

Sur votre machine :

- cloner le projet dans `~/workspace/`
- modifier le nom du projet dans le `pom.xml`
- configurer le *proxy* pour `maven`
- importer le projet dans `eclipse` en tant que *Projet maven déjà existant*
- modifier les noms de paquetages

# Installation de `maven`
## Prérequis
### Java 1.8
Vous devez avoir un Java 1.8 minimum installé sur votre ordinateur.

Pour Ubuntu ou Debian :

    sudo apt-get install openjdk-8-jdk

Pour Windows/OS X : [https://www.java.com/fr/download](https://www.java.com/fr/download)

## Maven
### Linux
Pour installer maven depuis ubuntu ou debian, vous pouvez installer le paquet mvn directement depuis les dépots officiels :

    sudo apt-get install mvn


### OS X
Il est conseillé d'installer brew qui facilite la gestion d'outils UNIX en ligne de commande (et même graphiques): [https://brew.sh](https://brew.sh)

Ensuite, vous pouvez installer ``maven`` à l'aide de la commande:

    brew install maven

### Windows
Télécharger l'archive `maven` sur le site officiel : [http://maven.apache.org/download.cgi](http://maven.apache.org/download.cgi)

Décompressez l'archive dans le répertoire où vous souhaitez installer `maven`.

Je vous conseille ceci : 

     C:\Program Files\Apache\Maven

Voilà, vous avez installé `maven`. Il faut maintenant configurer les variables d'environnement de Windows pour qu'il l'utilise correctement :

      Panneau de Configuration > Système > Paramètres Avancés > Chercher Variable d'environnement

Une fois sur cette fenètre :

- Vérifiez que la variable `JAVA_HOME` existe et qu'elle pointe bien vers le java JDK installé sur votre ordinateur. Si elle n'existe pas, créez la.
- Créez deux nouvelles variables `M2_HOME` et `MAVEN_HOME` qui pointe vers le dossier d'installation de `maven`. (`C:\Program Files\Apache\Maven` ... si vous suivez les conseils)
- Et enfin, modifier la variable `PATH` en rajoutant ceci à la fin.

    `;%M2_HOME%/bin`

Vérifiez en passant que la variable `JAVA_HOME` est présente dans la variable `PATH`. Si ce n'est pa le cas, rajoutez ceci :

      ;%JAVA_HOME%/bin

Pour vérifier votre installation, ouvrez un terminal et taper :
  
      mvn -version


**/!\ Si vous êtes sur un ordinateur de l'IUT ou sur le réseau WIFI de Lille1, modifiez la configuration de `maven` en rajoutant les lignes pour paramètrer le *proxy* selon l'exemple. Le fichier de configuration devrait se trouver dans le répertoire `conf` du dossier d'installation de maven.**

# Configuration
## Maven

Créer ensuite un dossier `.m2` dans votre répertoire personnel s'il n'existe pas déjà. Il contiendra le fichier de configuration de `maven` :

    mkdir $HOME/.m2
    touch $HOME/.m2/settings.xml

Modifier ou créer le fichier `settings.xml` avec votre éditeur préféré (`emacs` / `vim` / `vi` :-)) et copiez cette configuration :

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <localRepository>/tmp/USER/mvn/repository</localRepository>
    <proxies>
      <proxy>
        <id>proxy</id>
        <active>true</active>
        <protocol>http</protocol>
        <host>cache.univ-lille1.fr</host>
        <port>3128</port>
      </proxy>
    </proxies>
</settings>
```

Pour vérifier votre installation, ouvrez un terminal et taper :
  
      mvn -version


**/!\ Si vous n'êtes pas sur les ordinateurs de l'IUT, ou sur le réseau WIFI de Lille1, passer le paramètre `proxy.active` à `false` !**

## Eclipse

Avec `Éclipse Mars`, le plugin est installé de base, l'importation peut donc se faire directement !

# Test du projet en local

Dans le répertoire du serveur, pour lancer le projet sur la machine du développeur et visiter les pages web sur [http://localhost:8080](http://localhost:8080)

    mvn jetty:run

Ce qui lance un serveur local.

# Liens utiles
- [Points de cours](doc/cours.md)
- [Documentation de `Jersey`](https://jersey.java.net/documentation/latest/index.html)
- [Explication de JAX-RS avec Jersey](http://coenraets.org/blog/2011/12/restful-services-with-jquery-and-java-using-jax-rs-and-jersey)
- [Aide sur les IHM en java avec Jersey](http://thierry-leriche-dessirier.developpez.com/tutoriels/java/client-swing-menus-filtres-rest-service/)
- [Framework HTML/CSS/JS Bootstrap](http://getbootstrap.com)
