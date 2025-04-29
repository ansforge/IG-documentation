
Le guide d’implémentation est un support de publication des spécifications d’interopérabilité, combinant une documentation technique et une documentation narrative. Il n’est pas réservé aux seuls organismes de normalisation (comme InteropSanté ou l’ANS) : tout acteur peut en publier afin de rendre visibles ses spécifications, à condition qu’elles soient cohérentes avec l’écosystème français et compatibles avec les guides d’implémentation nationaux, notamment permis grâce au mécanisme d’héritage.

Ce guide d'implémentation "documentation" contient l'ensemble des bonnes pratiques de création de guides d'implémentation pour les FHIR modelers, ainsi que la documentation sur "comment lire un guide d'implémentation" pour un implémenteur.

L’objectif est d’encourager la participation de l’ensemble des parties prenantes. Bien qu’il existe déjà des publications versionnées, celles-ci ne sont pas définitives : elles restent ouvertes à l’évolution et peuvent être adaptées en fonction des contributions et des retours de l'ensemble des lecteurs.

### Les guides d'implémentation

Selon la documentation FHIR, un Implementation Guide contient un ensemble cohérent de ressources de conformité pour répondre à une problématique particulière.

Un implementation guide se présente sous forme d'un site web et d'un package contenant l'ensemble des ressources de conformité. Les implementation guides (site web, ressources de conformité et package) sont versionnés. L'ensemble des versions historiques seront toujours accessibles.

La meilleure pratique consiste à créer un Implementation Guide par projet bien spécifique, cela permet :

* De versionner séparément, on peut ainsi mettre à jour chacune des specs séparément sans avoir à mettre à jour celles qui ne sont pas concernées
* Chacune des specs gère ses dépendances indépendamment des autres (aux ressources du ci-sis, aux profils interopsanté), chacune de ces dépendances peuvent être mises à jour séparément
* Les urls sont claires, on sait directement de quelle spécification est issue chaque profil, et on peut directement accéder à l'IG en connaissant l'url canonique de l'IG
* Les documentations génériques peuvent être surspécifiées pour réutiliser certains profils pour un autre cas d'usage, en héritant de tout ou partie, ou pour décrire une implémentation précise
* L'IG doit obligatoirement hériter des profils FHIR réalisés par InteropSanté et/ou par l'ANS s'ils existent.

Documentation : [ImplementationGuide](https://www.hl7.org/fhir/implementationguide.html), [Packages](https://confluence.hl7.org/display/FHIR/NPM+Package+Specification)

### A qui est destiné ce wiki ?

Il est destiné à celles et ceux qui utilisent FHIR :

* Les FHIR modelers, qui créent ces guides et profilent des ressources
* Les FHIR implementers, qui lisent ces guides et développent des APIs
* Les experts fonctionnels, qui ont la vision métier et ont la capacité de challenger ces travaux. Les experts fonctionnels ont une plus value à connaître FHIR, la façon de profiler des ressources et de développer les APIs : ce sont les personnes qui connaissent le mieux le besoin métier qui seront le plus à même de juger le travail de modélisation effectué par les experts interopérabilité.

Pour plus d'informations sur la modélisation ou l'implémentation FHIR, il suffit de naviguer au sein du menu de ci-dessus.

### La liste des guides d'implémentation de l'ANS

La liste des guides d'implémentation est accessible [à cette adresse](https://interop.esante.gouv.fr/ig/).

### Reporter un problème ou une suggestion d'amélioration

Vous avez identifié une erreur sur un des guides ? L'onglet issue permet de signaler un problème sur un projet donné.

<img width="100%" alt="image" src="https://user-images.githubusercontent.com/48218773/215773144-31a47623-a853-4a4e-8ba0-ad1d66b29961.png">

Un lien est également disponible sous chaque guide d'implémentation pour accéder aux issues :
<img width="100%" alt="image" src="new_issue.png">

L'issue doit contenir un titre, et une description très détaillée avec une proposition de changement.

### Les outils utilisés dans ce guide

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

Des exemples d'Implementation Guide :

* Us-core : [Publication](https://hl7.org/fhir/us/core/), [GitHub](https://github.com/HL7/US-Core)
* mcode (qui se base sur uscore) : [Publication](http://hl7.org/fhir/us/mcode/), [GitHub](https://github.com/HL7/fhir-mCODE-ig)
* SDC, IG qui définit des profils de la ressource FHIR Questionnaire. Ces profils rajoutent des fonctionnalités de : préremplissage des champs, indiquer un design de formulaire, calcul automatique…) : [Publication](http://hl7.org/fhir/uv/sdc/index.html), [GitHub](https://github.com/HL7/sdc)

L'éditeur de profils FSH (Grammaire de définition de profils) : [getting started](https://fshschool.org/), [documentation](https://build.fhir.org/ig/HL7/fhir-shorthand/)

Autres :

* [IG publisher - documentation officielle HL7](https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation)
* [Clinical Quality Language (CQL)](https://cql.hl7.org/) (langage d'expression FHIR, permettant par ex de décrire le calcul de l'IMC), [Documentation](https://build.fhir.org/ig/HL7/cqf-measures/using-cql.html), [GitHub](https://github.com/HL7/cql)
