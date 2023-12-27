Bienvenue dans la documentation des guides d'implémentation de l'ANS, elle concerne principalement les volets du CI-SIS au format FHIR mais ne se limite pas à ceux-ci. Cette documentation contient l'ensemble des informations à propos de la modélisation, des outils FSH et IG publisher, ainsi que des tips dans le contexte français.

Ces travaux se placent dans une démarche d'élaboration continue. L'objectif étant de profiter de l'intelligence collective pour faire évoluer les spécifications versionnées. 

### L'écosystème FHIR France


<div style="text-align: center;">{%include ecosystem.svg%}</div>

### Les guides d'implémentation

Selon la documentation FHIR, un Implementation Guide contient un ensemble cohérent de ressources de conformité pour répondre à une problématique particulière.

Un implementation guide est un ensemble cohérent regroupant une page web et une ressource FHIR [ImplementationGuide](https://www.hl7.org/fhir/R4/implementationguide.html). Le site web contient également de manière systématique un package, versionné, contenant l'ensemble des ressources de conformité.

La meilleure pratique consiste à créer un Implementation Guide par projet bien spécifique, cela permet:

* De versionner séparément, on peut ainsi mettre à jour chacune des specs séparément sans avoir à mettre à jour celles qui ne sont pas concernées
* Chacune des specs gère ses dépendances indépendamment des autres (aux ressources du ci-sis, aux profils interopsanté), chacune de ces dépendances peuvent être mises à jour séparément
* Les urls sont claires, on sait directement de quelle spec est issue chaque profil, et on peut directement accéder à l'IG facilement
* Les documentations génériques peuvent être surspécifiées pour réutiliser certains profils pour un autre cas d'usage, en héritant de tout ou partie, ou pour décrire une implémentation précise.
* L'IG doit obligatoirement hériter des ressources françaises définies par InteropSanté et/ou par les profils définis par l'ANS

Documentation : [ImplementationGuide](https://www.hl7.org/fhir/implementationguide.html), [Packages](https://confluence.hl7.org/display/FHIR/NPM+Package+Specification)

### A qui est destiné ce wiki ?

Il est destiné à celles et ceux qui utilisent FHIR !

* Les FHIR modelers, qui créent ces guides et profilent des ressources
* Les FHIR implementers, qui lisent ces guides et développent des APIs 
* Les experts fonctionnels, qui ont la vision métier et ont la capacité de challenger ces travaux.

Les experts fonctionnels ont également une plus value à connaître FHIR, la façon de profiler des ressources et de développer les APIs : c'est les personnes qui connaissent le mieux le besoin métier qui seront le plus à même de juger le travail de modélisation effectué par les experts interopérabilité.

### La liste des guides d'implémentation de l'ANS

La liste des guides d'implémentation est accessible [à cette adresse](https://interop.esante.gouv.fr/ig/fhir/).

### Reporter un problème ou une suggestion d'amélioration

Vous avez identifié une erreur sur un des guides ? L'onglet issue permet de signaler un problème sur un projet donné.

<img width="100%" alt="image" src="https://user-images.githubusercontent.com/48218773/215773144-31a47623-a853-4a4e-8ba0-ad1d66b29961.png">

Un lien est également disponible sous chaque guide d'implémentation pour accéder aux issues :
<img width="100%" alt="image" src="new_issue.png">

L'issue doit contenir un titre, et une description très détaillée avec une proposition de changement.

### Modeler : par où commencer ?

1/ Installer les dépendances grâce à la page "Installer les dépendances [Windows/mac]"

2/ Développer un Implementation Guide :

* Si vous souhaitez créer un Implementation Guide pour publication : suivre la procédure Développement d'un nouvel IG
* Si vous souhaitez modifier un Implementation Guide existant : cloner le GitHub repository désiré et proposer une Pull Request une fois le travail effectué
* Si vous souhaitez tester FSH et la génération d'Implementation Guide : cloner le GitHub repository IG-modele ou téléchargez-le au format zip

### Outils et vocabulaire

#### FSH

FSH est la grammaire de définition des ressources FHIR (instance, StructureDefinition, SearchParameter, CapabilityStatement, ImplementationGuide, ...)

#### SUSHI

Sushi est le logiciel permettant de générer les ressources au format json ou xml à partir de la grammaire FSH.
Il est disponible en ligne sur [le site FSHSchool](https://fshschool.org/) ou en [invite de commande](https://www.npmjs.com/package/fsh-sushi)

Par défaut, sushi ne génère que les differential. Pour générer les snapshots, il faut utiliser l'option `sushi -s .`

#### GOFSH

GoFSH permet de faire la transformation inverse StructureDefinition --> FSH. Il permet de faciliter la prise en main et la conversion d'anciens projets json dans la syntaxe FSH.
De la même manière qu'FSH, GoFSH est également disponible en ligne sur [le site FSHSchool](https://fshschool.org/) ou en [invite de commande](https://www.npmjs.com/package/gofsh)

Par défaut, GoFSH ne traite que les fichiers json. Il va falloir rajouter l'option `goFSH -t json-and-xml .` pour traiter les deux.

A noter, la fonction fshing-trip lancée avec la commande `gofsh --fshing-trip` permet de lancer goFSH puis sushi et de générer une comparaison entre le json initial et le json généré avec sushi visualisable sous la forme d'une page html.

#### IG Publisher

L'IG publisher est l'outil permettant de générer les pages web de l'implementation guide (usage de jekyll, java, ...).
Il prend en entrée une arborescence de dossiers / fichiers bien définis, contenant : des pages en markdown, des fichiers fsh, des ressources FHIR au format json ou xml, des images...

Vous pouvez vous référer à [la documentation officielle de l'IG publisher](https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation).

### Liens utiles

Des exemples d'ImplementationGuide:

* Us-core : [Publication](https://hl7.org/fhir/us/core/), [GitHub](https://github.com/HL7/US-Core)
* mcode (qui se base sur uscore) : [Publication](http://hl7.org/fhir/us/mcode/), [GitHub](https://github.com/HL7/fhir-mCODE-ig)
* SDC, IG qui définit des profils de la ressource FHIR Questionnaire. Ces profils rajoutent des fonctionnalités de : préremplissage des champs, indiquer un design de formulaire, calcul automatique…) : [Publication](http://hl7.org/fhir/uv/sdc/index.html), [GitHub](https://github.com/HL7/sdc)

L'éditeur de profils FSH (Grammaire de définition de profils) : [getting started](https://fshschool.org/), [documentation](https://build.fhir.org/ig/HL7/fhir-shorthand/)

Autres :

* [IG publisher - documentation officielle HL7](https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation)
* [Clinical Quality Language (CQL)](https://cql.hl7.org/) (langage d'expression FHIR, permettant par ex de décrire le calcul de l'IMC), [Documentation](https://build.fhir.org/ig/HL7/cqf-measures/using-cql.html), [GitHub](https://github.com/HL7/cql)
