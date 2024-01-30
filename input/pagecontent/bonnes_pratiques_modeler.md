
La mise en place de niveaux de maturité des guides d'implémentation se basant sur le FMM (FHIR Maturity Model) est en cours de réflexion. En attandant la publication de ces niveaux de maturité, il est important de respecter au maximum les critères indiqués ci-dessous.

### Critères de qualité

* Respect des bonnes pratiques nationales tel que les règles de nommages indiquées ci-dessous
* Respect des [bonnes pratiques internationales](https://build.fhir.org/ig/FHIR/ig-guidance/best-practice.html)
* Publication de l'IG sans erreurs (cf session Q/A)

### Critères de maturité

* Ensemble des critères de qualité respectés
* Nombre d'implémentation obtenu par déclaration (par convergence ou par les DSI). Idéalement, publier des retours d'expérience sur l'implémentation des spécifications
* Nombre de tests réalisés lors de projectathon, et nombre de partenaires
* Nombre d'issues et résolutions sur le repo GitHub
* Nombre de commentaires lors des phases de concertation
* Publication du package avec des dépendances : les ressources héritées ne sont pas dupliquées
* L'ensemble des ressources de conformité doit avoir une description précise de son utilité

### Choix de la version de FHIR

Pour garantir la cohérence de l'écosystème, il faudra privilégier l'usage de R4. Si l'usage d'une autre version de FHIR est néanmoins nécessaire (cas d'usage international, évolution des ressources, ...), une étude de normes et standards devra être fournie pour justifier ce choix.

### Création des ressources de conformité

#### La définition des profils et des extensions

Pour être intéropérable, il faut tout d'abord éviter la sur-profilisation, c'est à dire créer des profils qui existent déjà. Pour cela, il est nécessaire d'hériter au maximum des profils internationaux, pour que les contraintes et modélisations soit partagées au maximum entre les acteurs répondant à un cas d'usage.

De la même manière, l'usage des extensions est à éviter au maximum. Si leur usage est nécessaire, il est préférable d'hériter d'extensions déjà créées.

Où chercher les profils-extensions déjà créés ?

* [Profils IHE](https://www.ihe.net/resources/profiles/)
* [FHIR Package Registry](https://registry.fhir.org/)
* [Extensions](https://www.hl7.org/fhir/R4/extensibility-registry.html) et [profils](https://www.hl7.org/fhir/R4/profilelist.html) définis dans FHIR core

#### La définition des ressources terminologiques (ValueSet et CodeSystem)

Ce paragraphe sera complété lorsque le FHIR Terminology Service sera en service.

<!-- FSH et l'IG publisher permet de générer ces ressources directement au sein des IG. Ainsi, le package de l'IG contiendra les [CodeSystem](https://www.hl7.org/fhir/R4/codesystem.html) (CS) et les [ValueSet](https://www.hl7.org/fhir/R4/valueset.html) (VS). 
Il se pose alors la question : est-ce que les CS et VS doivent le SMT ou dans les IGs ?

Il n'y a pas de réponse générique, mais il faut privilégier l'usage du SMT car c'est une source de vérité.

Dans certains cas, mettre les VS dans l'IG est possible, notamment pour les profils applicatifs, mais dans ce cas:
* Il faut favoriser l'inclusion des CodeSystem et des ValueSet entiers dans ce VS plutôt que d'inclure des codes individuels. Cela permet d'éviter des erreurs de divergence entre les versions des terminologies.
* Il faut préciser que l'expansion indiquée dans l'IG n'est pas forcément un reflet de la réalité : elle l'était à un instant T lors de la génération de l'IG, mais les CodeSystem ont pu évoluer entre temps. 

TODO : rajouter lien vers la procédure de création d'un VS
-->

### Règles de nommage des ressources de conformité

Ces règles de nommages ont été établies en s'inspirant des ressources us-core

| **Attribut** | **Description** | **Exemple us-core** |
| ----- | ----- | ----- |
| id | utiliser le format kebab-case, ex : fr-patient. (/!\ sur Forge, l'id n'est pas obligatoire, il est important de le rajouter !). Lors de la création d'un IG pour un projet en particulier, il est possible de préfixer l'ensemble des ressources de conformité par le trigramme du projet (ex : "ror-...") | us-core-patient |
| title | similaire au nom, avec espaces. Ex : Fr Patient | US Core Patient Profile |
| name | Utiliser le format PascalCase sans espace. Ex : FrPatient | USCorePatientProfile |
| url | [base]/[ResourceType]/[id] (généré automatiquement par sushi). A noter que [ResourceType] doit respecter le nom et la casse des ressources définies dans FHIR core (ex: StructureDefinition). | http://hl7.org/fhir/us/core/StructureDefinition/us-core-patient |
| SearchParameter.code | toujours en minuscule, mots séparés par des tirets "-" si besoin | - |
{: .grid }

Nom des slices:

* Prendre l'id de l'extension s'il s'agit d'une extension
* Sinon, lowerCamelCase

La documentation officielle se trouve sur le [confluence d'HL7](https://confluence.hl7.org/pages/viewpage.action?pageId=35718826#GuidetoDesigningResources-NamingRules&Guidelines)

### Les packages et les dépendances

L'id de package ne doit pas avoir de majuscule.

Le package doit toujours dépendre de fr-core, de l'annuaire santé et/ou les projets de l'ANS pour assurer une cohérence globale à l'échelle française. Ces packages sont publiés sur le FHIR Package Registry et doivent être indiqués dans le fichier `sushi-config.yaml`. La duplication des fichiers ou la référence par URL est une très mauvaise pratique car on perd tout l'intérêt du versioning.

### Les URL canoniques

L'URL canonique est un outil très puissant dans le standard HL7 FHIR, il permet d'identifier de manière unique chaque implementation guide (IG) et chaque profil.

#### L'URL canonique de l'IG

L'URL canonique de l'IG permet d'accéder à sa page web, c'est à dire la spécification narrative et technique (ex : https://www.hl7.org/fhir/us/core).
Dans le cas des IG de l'ANS, l'url canonique est https://interop.esante.gouv.fr/ig/[fhir/][code]

#### L'URL canonique des ressources de conformité

A partir de ce lien, il y a une API Rest FHIR, qui permet d'accéder aux ressources de conformité conformément à la FHIR search (https://www.hl7.org/fhir/search.html). On obtient ainsi les url canoniques de chaque profil (ex : http://hl7.org/fhir/us/core/StructureDefinition/us-core-patient).
L'URL canonique des profils est construite au format : [base]/[ResourceType]/[id] pour qu'elle corresponde à une requête FHIR Search

L'outil HL7 IG Publisher, combiné avec sushi, gère automatiquement certaines redirections et génère automatiquement les urls des profils à partir de l'url base indiquée.

Ainsi, l'url canonique d'un profil permet de facilement retrouver la spécification d'où elle est issue de manière très efficace et claire.

A noter le ResourceType doit respecter la même casse et le même nom que les ResourceName FHIR.

Documentation :

* [https://confluence.hl7.org/pages/viewpage.action?pageId=35718627#IGPublisherDocumentation-CanonicalURL]
* [https://confluence.hl7.org/pages/viewpage.action?pageId=81027536#MaintainingaFHIRIGPublication-CanonicalURLs]

### FSH / SUSHI

#### Factorisation

Sushi et FSH permettent de factoriser beaucoup d'informations, et de les centraliser afin d'en faciliter l'accès et la gestion.
Il est recommandé de faire bénéficier au maximum les projets de cette possibilité de centraliser les informations redondantes.

#### Configuration de sushi-config : status, version, releaseLabel

Le **status** devra être placé à draft lorsque celui-ci n'est pas officiellement publié. Il devra être placé à active lors de la première publication. Il est également possible de définir un status par profil si certaine partie de la spécification est en mode draft.

Le numéro de **version** doit respecter le processus semver, soit majeur.mineur.patch. Son usage est précisément défini dans la [documentation semver](https://semver.org/lang/fr/).

Le **releaseLabel** doit être systématiquement placé à trial-use pour l'instant. Des labels plus fins seront proposés dans le futur, établi en fonction de critères de maturité.
Il est possible de préciser la maturité sous forme de release notes en début de page index en utilisant la balise \<blockquote class=\"stu-note\"\>\<blockquote\>.

Le statut, la version le releaseLabel sont à renseigner dans le fichier [sushi-config.yaml](https://fshschool.org/docs/sushi/configuration/)

> status: active  
> version: 0.1.3
> releaseLabel: trial-use

#### Extensions et ValueSets

Il est recommandé de classer les extensions et les valueSets source (FSH) dans des sous-répertoires spécifiques, input\fsh\Extensions et input\fsh\ValueSets.
Les structure-definitions des profils seront placés dans input\fsh.

#### Gestion des alias

Les alias FSH sont des variables permettant de définir un raccourci pour une URL ou un OID. 

Par exemple, on peut ainsi définir l’alias $phdDevice pour représenter l’URL «http://hl7.org/fhir/uv/phd/StructureDefinition/PhdDevice» et l’utiliser de la manière suivante au sein d’un profil FSH :

> Alias: $PhdDevice = http://hl7.org/fhir/uv/phd/StructureDefinition/PhdDevice
> \* device only Reference($PhdDevice)

Par soucis de clarté, il est recommandé de rassembler tous les alias dans un fichier unique, appelé « aliases.fsh » et situé dans le répertoire racine (évite les redondances et facilite la gestion).

Exemple:
> Alias: $PhdDevice = http://hl7.org/fhir/uv/phd/StructureDefinition/PhdDevice
> Alias: $UCUM = http://unitsofmeasure.org
> Alias: $vitalsigns = http://hl7.org/fhir/StructureDefinition/vitalsigns
> Alias: $FrObservationBp = http://interopsante.org/fhir/StructureDefinition/FrObservationBp  
> Alias: $fr-patient = http://interopsante.org/fhir/StructureDefinition/FrPatient  

### Exemples de guides d'implémentation

Pour plus d'informations, consultez la [liste des guides d'implémentation](https://interop.esante.gouv.fr/ig/fhir/) à titre d'exemple.

### Le choix de la version FHIR

Avant de commencer à développer un guide d'implémentation, il faut choisir la version FHIR sur laquelle se baser : R4, R4B, R5 ? L'objectif étant d'avoir un écosystème uniforme et simple qui hérite systématiquement de fr-core pour avoir des modélisations les plus cohérentes possibles.

A l'heure actuelle, les spécifications des projets nationaux utilisent la R4 (fr-core, IG ANS, Annuaire, ROR...).  Or travailler sur R4 et R5 parallèlement engendre beaucoup de questions : travaux de maintenance doublés, nécessité de maintenir des mappings/connecteurs entre versions (R4 <-> R5, R4 <-> R6, R5 <-> R6, ...), augmentation de la complexité de l'écosystème avec certains acteurs en R4, d'autres en R5...
Les ressources étant limitées, il est préférable de se concentrer sur l'amélioration de nos profils nationaux en R4 et de faire monter l'écosystème en compétences.

La release R5 reste cependant intéressante, notamment pour l'amélioration de sa documentation et de certaines ressources (Documentation FHIR Search, Ressources MedicinalProduct...).
Ce choix n'est pas tranché, c'est l'écosystème qui dictera quelle version utiliser. Si vous ressentez un besoin d'utiliser R5 (notamment pour des cas d'usages internationaux ou profiter de ressources non matures en R4), nous vous invitons à nous le signaler pour réévaluer le bénéfice/risque de travailler sur FHIR R5. A noter que FHIR R6, dont la première concertation est prévue mi-2024, apportera beaucoup de contenu normatif, et sera peut-être l'objectif de transition.

La conclusion actuelle (octobre 2023) est de privilégier R4 pour ne pas être "hors système" et être cohérent avec fr-core et les IGs de l'ANS tant qu'il n'y a pas de socle commun à l'utilisation de R5. Utiliser R5 uniquement si l'écosystème l'exige (ex : héritage d'un IG international en R5, héritage de ressources retravaillées en R5...) et partager ce besoin en issue GitHub.

FHIR R6, dont la première concertation est prévue mi-2024, apportera beaucoup de contenu normatif, et sera peut-être l'objectif de transition.