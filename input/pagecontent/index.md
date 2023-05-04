Bienvenue dans la documentation des guides d'implémentation de l'ANS, elle concerne principalement les volets du CI-SIS qui concernent le format FHIR mais ne se limitent pas à ceux-ci. Celui-ci contient toutes les informations à propos de la modélisation, des outils FSH et IG publisher, ainsi que des tips dans le contexte français.

Ces travaux se placent dans une démarche d'élaboration continue. L'objectif étant de profiter de l'intelligence collective pour faire évoluer les spécifications versionnées. 

### Les guides d'implémentation

Selon la documentation FHIR, un Implementation Guide contient un ensemble cohérent de ressources de conformité pour répondre à une problématique particulière.

Un implementation guide est un ensemble cohérent regroupant une page web et une ressource FHIR. Il contient également de manière systématique un package, versionné, contenant l'ensemble des ressources de conformité.


La meilleure pratique consiste à créer un Implementation Guide par projet bien spécifique, cela permet:
- De versionner séparément, on peut ainsi mettre à jour chacune des specs séparément sans avoir à mettre à jour celles qui ne sont pas concernées
- Chacune des specs gère ses dépendances indépendamment des autres (aux ressources du ci-sis, aux profils interopsanté), chacune de ces dépendances peuvent être mises à jour séparément
- Les urls sont claires, on sait directement de quelle spec est issue chaque profil, et on peut directement accéder à l'IG facilement
- Ca permet aux éditeurs de surspécifier pour réutiliser certains profils pour un autre cas d'usage, en héritant de tout ou partie

Documentation : 
- https://www.hl7.org/fhir/implementationguide.html
- https://confluence.hl7.org/display/FHIR/NPM+Package+Specification

### A qui est destiné ce wiki ?

Il est destiné à celles et ceux qui utilisent FHIR !

- Les FHIR modelers, qui créent ces guides et profilent des ressources
- Les FHIR implementers, qui lisent ces guides et développent des APIs 
- Les experts fonctionnels, qui challengent ces travaux.

Les experts fonctionnels ont également une plus value à connaître FHIR, la façon de profiler des ressources et de développer les APIs : c'est les personnes qui connaissent le mieux le besoin métier qui seront le plus à même de juger le travail de modélisation effectué par les experts interopérabilité.

### Reporter un problème (une issue)

Vous avez identifié une erreur sur un des guides ? L'onglet issue permet de signaler un problème sur un projet donné.

<img width="1541" alt="image" src="https://user-images.githubusercontent.com/48218773/215773144-31a47623-a853-4a4e-8ba0-ad1d66b29961.png">

Un lien est également disponible sous chaque guide d'implémentation pour accéder aux issues :
<img width="1541" alt="image" src="new_issue.png">

L'issue doit contenir un titre, et une description très détaillée avec une proposition de changement.

### Par où commencer ?

1/ Installer les dépendances grâce à la page "Installer les dépendances [Windows/mac]" de ce wiki

2/ Développer un Implementation Guide :
* Si vous souhaitez créer un Implementation Guide pour publication : suivre la procédure Développement d'un nouvel IG
* Si vous souhaitez modifier un Implementation Guide existant : cloner le GitHub repository désiré
* Si vous souhaitez tester FSH et les Implementation Guide : cloner le GitHub repository FIG_ans-ig-sample ou téléchargez-le au format zip


### Outils et vocabulaire 

#### FSH

FSH est la grammaire de définition des ressources FHIR (instance, StructureDefinition, SearchParameter, CapabilityStatement, ImplementationGuide, ...)

#### SUSHI

Sushi est le logiciel permettant de générer les ressources au format json ou xml à partir de la grammaire FSH.
Il est disponible en ligne : https://fshschool.org/
Ou bien en invite de commande : https://www.npmjs.com/package/fsh-sushi

Par défaut, sushi ne génère que les differential. Pour générer les snapshots, il faut utiliser l'option `sushi -s .`

#### GOFSH

GoFSH permet de faire la transformation inverse StructureDefinition --> FSH.
Il est disponible en ligne : https://fshschool.org/
Ou bien en invite de commande : https://www.npmjs.com/package/gofsh

Par défaut, GoFSH ne traite que les fichiers json. Il va falloir rajouter l'option `goFSH -t json-and-xml .` pour traiter les deux


#### IG Publisher

L'IG publisher est l'outil permettant de générer les pages web de l'implementation guide (usage de jekyll, java, ...).
Il prend en entrée une arborescence de dossiers / fichiers bien définis, contenant : des pages en markdown, des fichiers fsh, des ressources FHIR au format json ou xml, des images...

La documentation est disponible ici : https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation

### Liens utiles

Des exemples d'ImplementationGuide:
- Us-core https://hl7.org/fhir/us/core/
    - https://github.com/HL7/US-Core
- mcode https://build.fhir.org/ig/HL7/fhir-mCODE-ig/ (qui se base sur uscore)
    - https://github.com/HL7/fhir-mCODE-ig
- SDC, IG qui définit des profils de la ressource FHIR Questionnaire. Ces profils rajoutent des fonctionnalités de : préremplissage des champs, indiquer un design de formulaire, calcul automatique…)   
    - http://hl7.org/fhir/uv/sdc/index.html

Les éditeurs de profils :
- FSH (Grammaire de définition de profils)
    - https://fshschool.org/
    - https://build.fhir.org/ig/HL7/fhir-shorthand/
 
- Forge (définition de profils via interface graphique)
    - https://simplifier.net/forge
 
Autres :
- IG publisher documentation (officiel HL7):
    - https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation
- Doc CQL (langage d'expression FHIR, permettant par ex de décrire le calcul de l'IMC) :
    - https://build.fhir.org/ig/HL7/cqf-measures/using-cql.html
    - https://cql.hl7.org/