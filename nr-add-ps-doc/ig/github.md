# Usage de GitHub - Documentation des guides d'implémentation de l'ANS v0.1.9

* [**Table of Contents**](toc.md)
* [**Doc Modeler**](doc_modeler.md)
* **Usage de GitHub**

## Usage de GitHub

GitHub est l’équivalent d’un sharepoint, un répertoire (=repository) versionné avec un système de branche pour travailler de manière collaborative sur du contenu textuel (code, écriture, grammaire …).

### Premiers pas sur GiHub

Pour créer un compte GitHub et être enrôlé dans l’organisation ansforge, il suffit de suivre [cette documentation](https://ansforge.github.io/Documentation/)

### Création d’un nouveau projet

#### les règles de nommage

Des règles ont déjà été [définies](https://ansforge.github.io/Documentation/pages/docs/creationprojet.html) au niveau de l’organisation ANS. Celles-ci ont été sur-contraintes pour les projets liés à l’intéropérabilité

Le nom du repository devra être sous forme interop-[type]-[optionnel-format]-[optionnel-projet/produit]-[nom-descriptif] avec :

* [type] = ig / exemples / outil / termino…
* [optionnel-format] = fhir / cda / owl / …
* [optionnel-projet/produit] = drim / smt / nrc
* [nom-descriptif] = nom clair et concis sans acronyme séparé avec des tirets.

L’ensemble du nom devra être en minuscule.

Exemples : interop-ig-fhir-annuaire, interop-outils-cda

#### les règles de création de tags associés à un repository GitHub

Les tags sont des informations complémentaires au titre du repository. Ils doivent être en minuscule sans espace, sans tiret.

Exemples de tags qui peuvent être utilisés :

* Standard (fhir, cda, hl7v2, …)
* Termino (snomed, loinc, …)
* ci-sis
* Domaine IHE (domaine métier) / couloir ségur
* [optionnel] ancien nom si changement de nom de repo

Tags à éviter :

* implementation-guide (trop générique et dans le titre)
* HL7 (trop générique, risque d’être confondu avec hl7v2)
* volet (inutile, trop générique)
* Sous-ensemble du nom du répertoire

### Reporter un problème (une issue) sur un des repository GitHub

Vous avez identifié une erreur sur un des guides ? L’onglet issue permet de signaler un problème sur un projet donné.

Un lien est également disponible sous chaque guide d’implémentation pour accéder aux issues :

L’issue doit contenir un titre, et une description très détaillée avec une proposition de changement.

Cf. documentation officielle : https://docs.github.com/fr/issues/tracking-your-work-with-issues/using-issues/creating-an-issue

### Travailler sur un repository

GitHub peut s’utiliser de deux façons via l’application GitHub Desktop ou via l’invite de commande. Il est détaillé ci-dessous comment faire une modification via l’invite de commande.

#### Git clone xxx

La commande git clone permet de copier l’intégralité d’un repository en local. Le xxx est à remplacer avec l’indication dans ssh :

#### Git checkout -b nom_travail_en_cours

Les branches : un repository (ou répertoire) Github contient une arborescence de branche, permettant d’individualiser le travail de chacun puis de pousser son travail dans la branche de travail commune : typiquement `main`.

Pour éviter que tout le monde travaille sur le même environnement, il est nécessaire de créer une nouvelle branche, et de l’appeler par le nom du travail prévu dans cette branche. Le nom de la branche doit être en minuscule et commencer par son acronyme (ex : nr- pour Nicolas Riss).

Une fois la branche créée, il est possible de faire les modifications pour ensuite les reporter sur le repository GitHub distant pour revue.

#### Git add fichiers_à_ajouter

Une fois les modifications établies, il faut dire à Git quels fichiers on souhaite ajouter au répertoire distant en faisant git add et en rajoutant le chemin vers les fichiers à ajouter (la commande `git status` permet de voir quels fichiers ont été modifiés)

#### Git commit -m “message sur la nature des travaux effectués”

Une fois les travaux menés (tout ou partie), il faut faire des commit : c’est à dire valider une modification fonctionnelle, cohérente. Cette étape peut être répétée plusieurs fois.

#### Git push

Cette commande pousse l’ensemble des modifications validées avec des commit sur le GitHub distant.

#### Faire une demande de tirage ou Pull Request (PR)

Ensuite, il faut aller sur l’interface graphique, dans l’onglet, “Pull Requests”, et créer une nouvelle PR qui permet de dire : je veux intégrer les modifications que j’ai faites sur la branche x à la branche main.

Chaque PR doit être validée par quelqu’un d’autre pour :

* Etre sûr que le savoir n’est pas concentré sur une personne
* Permettre une relecture pour éviter les erreurs

Cf. documentation officielle : https://docs.github.com/fr/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request

### Mettre en place un workflow de validation/génération/publication

Afin de faciliter les actions au regards des IG, l’ANS met à disposition un [GitHub Action](https://github.com/ansforge/IG-workflows) avec les fonctionnalités suivantes :

* Lancement de sushi
* Tests avec le validateur_cli
* Incorporation des projets de simplifier (Methode bake)
* Publication des releases sur un repo github
* Génération du diagramme plantuml à partir de des données de l’IG
* Génération des diagrammes de mapping plantuml
* Génération des testscripts avec le projet testscript-generator
* Publication sur les pages github : 
* Diagramme de class plantuml généré à partir des données de l’IG
* Rapport de validation du validator_cli
 

