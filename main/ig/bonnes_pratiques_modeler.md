# Bonnes pratiques - Documentation des guides d'implémentation de l'ANS v0.1.9

* [**Table of Contents**](toc.md)
* [**Doc Modeler**](doc_modeler.md)
* **Bonnes pratiques**

## Bonnes pratiques

La mise en place de niveaux de maturité des guides d’implémentation se basant sur le FMM (FHIR Maturity Model) est en cours de réflexion. En attendant la publication de ces niveaux de maturité, il est important de respecter au maximum les critères indiqués ci-dessous.

### Critères de qualité

* Respect des bonnes pratiques nationales tel que les règles de nommages indiquées ci-dessous
* Respect des [bonnes pratiques internationales](https://build.fhir.org/ig/FHIR/ig-guidance/best-practice.html)
* Respecter le stratégie nationale des choix de version FHIR
* Chaque ressource de conformité doit avoir une description
* L’ensemble des ressources de conformité doit avoir une description précise de son usage
* Publication de l’IG sans erreurs (cf session Q/A)

### Critères de maturité

* Respect de l’ensemble des critères de qualité mentionnés ci-dessus
* Nombre d’implémentations obtenu par déclaration (par convergence ou par les DSI). Idéalement, publier des retours d’expérience sur l’implémentation des spécifications
* Nombre de passage en projectathons, nombre de tests réalisés lors de projectathon, et nombre de partenaires
* Nombre d’issues et résolutions sur le repo GitHub
* Nombre de commentaires lors des phases de concertation

### Création des ressources de conformité

#### La définition des profils et des extensions

Pour être intéropérable, il faut tout d’abord éviter la multiplication des profils qui conduit à créer des profils qui existent déjà. Pour cela, il est primordial de se raccrocher à l’écosystème national. Le package doit toujours dépendre de fr-core, de l’annuaire santé et/ou des projets de l’ANS pour assurer une cohérence globale à l’échelle française.

De plus, il est également nécessaire d’hériter des profils internationaux pour profiter de l’intelligence collective des groupes de travail internationaux et harmoniser au maximum les travaux. De la même manière, l’usage des extensions est à éviter au maximum. Si leur usage est nécessaire, il est préférable d’hériter de rechercher des extensions déjà créées dans l’écosystème FHIR.

Où chercher les profils-extensions déjà créés ?

* [Profils IHE](https://www.ihe.net/resources/profiles/)
* [FHIR Package Registry](https://registry.fhir.org/)
* [Extensions](https://www.hl7.org/fhir/R4/extensibility-registry.html) et [profils](https://www.hl7.org/fhir/R4/profilelist.html) définis dans FHIR core

#### La définition des ressources terminologiques (ValueSet et CodeSystem)

Ce paragraphe sera complété lorsque le FHIR Terminology Service sera en service.

### Règles de nommage des ressources de conformité

Ces règles de nommage ont été établies en s’inspirant des ressources us-core et des bonnes pratiques indiquées [ici]([https://build.fhir.org/ig/HL7/crmi-ig/artifact-conventions.md](https://hl7.org/fhir/uv/crmi/STU1/)).

| | | | |
| :--- | :--- | :--- | :--- |
| id | ressources de conformité  | utiliser le format kebab-case, ex : fr-core-patient. (/!\ sur Forge, l’id n’est pas obligatoire, il est important de le rajouter !). Lors de la création d’un IG pour un projet en particulier, il est possible de préfixer l’ensemble des ressources de conformité par le trigramme du projet (ex : “ror-…”) | us-core-patient |
| title | ressources de conformité  | similaire au nom, avec espaces. Ex : Fr Core Patient | US Core Patient Profile |
| name | ressources de conformité  | Utiliser le format PascalCase sans espace. Ex : FrCorePatient | USCorePatientProfile |
| url | ressources de conformité  | [base]/[ResourceType]/[id] (généré automatiquement par sushi). A noter que [ResourceType] doit respecter le nom et la casse des ressources définies dans FHIR core (ex: StructureDefinition). | http://hl7.org/fhir/us/core/StructureDefinition/us-core-patient |
| code | SearchParameter | toujours en minuscule, mots séparés par des tirets “-“ si besoin | - |
| name | slice | utiliser l’id de l’extension s’il s’agit d’une extension sinon utiliser le format lowerCamelCase | us-core-genderIdentity |
| id | package | utiliser des minuscules | hl7.fhir.us.core[lien vers la documentation](https://confluence.hl7.org/display/FHIR/NPM+Package+Specification) |

La documentation officielle se trouve sur le [confluence d’HL7](https://confluence.hl7.org/pages/viewpage.action?pageId=35718826#GuidetoDesigningResources-NamingRules&Guidelines)

### Les URL canoniques

L’URL canonique est un outil très puissant dans le standard HL7 FHIR, il permet d’identifier de manière unique chaque implementation guide (IG) et chaque profil.

L’**URL canonique de l’IG** permet d’accéder à sa page web, c’est à dire la spécification narrative et technique (ex : https://www.hl7.org/fhir/us/core). Dans le cas des IG de l’ANS, l’url canonique est https://interop.esante.gouv.fr/ig/[fhir/][code]

L’**URL canonique des ressources de conformité** permet d’identifier de manière unique chaque ressource de conformité. A partir de ce lien, il y a une API Rest FHIR, qui permet d’accéder aux ressources de conformité conformément à la FHIR search (https://www.hl7.org/fhir/search.html). On obtient ainsi les url canoniques de chaque profil (ex : http://hl7.org/fhir/us/core/StructureDefinition/us-core-patient). L’URL canonique des profils est construite au format : [base]/[ResourceType]/[id] pour qu’elle corresponde à une requête FHIR Search

L’outil HL7 IG Publisher, combiné avec sushi, gère automatiquement certaines redirections et génère automatiquement les urls des profils à partir de l’url base indiquée.

Ainsi, l’url canonique d’un profil permet de facilement retrouver la spécification d’où elle est issue de manière très efficace et claire.

A noter le ResourceType doit respecter la même casse et le même nom que les ResourceName FHIR.

Documentation :

* [https://confluence.hl7.org/pages/viewpage.action?pageId=35718627#IGPublisherDocumentation-CanonicalURL]
* [https://confluence.hl7.org/pages/viewpage.action?pageId=81027536#MaintainingaFHIRIGPublication-CanonicalURLs]

### FSH / SUSHI

Sushi et FSH permettent de factoriser beaucoup d’informations, et de les centraliser afin d’en faciliter l’accès et la gestion. Il est recommandé de faire bénéficier au maximum les projets de cette possibilité de centraliser les informations redondantes.

### Release d’un IG FHIR

Le **statut** devra être placé à draft lorsque celui-ci n’est pas officiellement publié. Il devra être placé à active lors de la première publication. Il est également possible de définir un status par profil si certaines parties de la spécification sont en mode draft. Le statut doit se placer dans l’attribut “status” du fichier sushi-config

Le numéro de **version** doit respecter le processus semver, soit majeur.mineur.patch. Son usage est précisément défini dans la [documentation semver](https://semver.org/lang/fr/). Le statut doit se placer dans l’attribut “version” du fichier sushi-config et dans l’attribut “version du fichier publication-request

Le **label de publication** doit contenir “ci-build”, “ballot”, “trial-use” ou “final-text” en fonction des cas qui seront détaillés dans le cycle de vie des spécifications bientôt publiés. Il est possible de préciser la maturité sous forme de release notes en début de page index en utilisant la balise <blockquote class="stu-note"><blockquote>. Le label de publication doit se placer dans l’attribut “label” du fichier “publication-request” et dans l’attribut releaseLabel du fichier sushi-config

Le **mode de publication** permet de paramétrer la release. Celui-ci doit être indiqué dans l’attribut “mode” du fichier publication-request.

Les travaux de mise à jour actuelle vont définir de nouveaux statuts pour les guides d’implémentation, voici la correspondance entre les statuts pressentis et les paramètres de publication :

| | | | |
| :--- | :--- | :--- | :--- |
| draft | draft | ci-build | N/A |
| public-comment | draft | ballot | working |
| for implementation | active | trial-use | milestone |
| final-text | active | final-text | milestone |
| withdrawn ou deprecated | retired | resp. withdrawn ou retired | withdrawal |

#### Extensions et ValueSets

Il est recommandé de classer les extensions et les valueSets source (FSH) dans des sous-répertoires spécifiques, input\fsh\Extensions et input\fsh\ValueSets. Les structure-definitions des profils seront placés dans input\fsh.

#### Gestion des alias

Les [alias FSH](https://build.fhir.org/ig/HL7/fhir-shorthand/reference.html#defining-aliases) sont des variables permettant de définir un raccourci pour une URL ou un OID. Par souci de clarté, il est recommandé de rassembler tous les alias dans un fichier unique, appelé « aliases.fsh » et situé dans le répertoire racine (évite les redondances et facilite la gestion).

Exemple:

> Alias: $PhdDevice = http://hl7.org/fhir/uv/phd/StructureDefinition/PhdDevice Alias: $UCUM = http://unitsofmeasure.org Alias: $vitalsigns = http://hl7.org/fhir/StructureDefinition/vitalsigns Alias: $FrObservationBp = http://interopsante.org/fhir/StructureDefinition/FrObservationBp
Alias: $fr-patient = http://interopsante.org/fhir/StructureDefinition/FrPatient

### Exemples de guides d’implémentation

Pour plus d’informations, consultez la [liste des guides d’implémentation](https://interop.esante.gouv.fr/ig/fhir/) à titre d’exemple.

### Le choix de la version FHIR

Pour garantir la cohérence de l’écosystème, il faudra privilégier l’usage de R4. Si l’usage d’une autre version de FHIR est néanmoins nécessaire (cas d’usage international, évolution des ressources, …), une étude de normes et standards devra être fournie pour justifier ce choix.

Avant de commencer à développer un guide d’implémentation, il faut choisir la version FHIR sur laquelle se baser : R4, R4B, R5 ? L’objectif étant d’avoir un écosystème uniforme et simple qui hérite systématiquement de fr-core pour avoir des modélisations les plus cohérentes possibles.

A l’heure actuelle, les spécifications des projets nationaux utilisent la R4 (fr-core, IG ANS, Annuaire, ROR…). Or travailler sur R4 et R5 parallèlement engendre beaucoup de questions : travaux de maintenance doublés, nécessité de maintenir des mappings/connecteurs entre versions (R4 <-> R5, R4 <-> R6, R5 <-> R6, …), augmentation de la complexité de l’écosystème avec certains acteurs en R4, d’autres en R5… Les ressources étant limitées, il est préférable de se concentrer sur l’amélioration de nos profils nationaux en R4 et de faire monter l’écosystème en compétences.

La release R5 reste cependant intéressante, notamment pour l’amélioration de sa documentation et de certaines ressources (Documentation FHIR Search, Ressources MedicinalProduct…). Ce choix n’est pas tranché, c’est l’écosystème qui dictera quelle version utiliser. Si vous ressentez un besoin d’utiliser R5 (notamment pour des cas d’usages internationaux ou profiter de ressources non matures en R4), nous vous invitons à nous le signaler pour réévaluer le bénéfice/risque de travailler sur FHIR R5. A noter que FHIR R6, dont la première concertation est prévue mi-2024, apportera beaucoup de contenu normatif, et sera peut-être l’objectif de transition.

La conclusion actuelle (octobre 2023) est de privilégier R4 pour ne pas être “hors système” et être cohérent avec fr-core et les IGs de l’ANS tant qu’il n’y a pas de socle commun à l’utilisation de R5. Utiliser R5 uniquement si l’écosystème l’exige (ex : héritage d’un IG international en R5, héritage de ressources retravaillées en R5…) et partager ce besoin en issue GitHub.

FHIR R6, dont la première concertation est prévue mi-2024, apportera beaucoup de contenu normatif, et sera peut-être l’objectif de transition.

### Règles d’utilisation de GitHub

Règles d’utilisation de GitHub :

* Toutes modifications d’une spécification sur GitHub doit se faire au niveau d’une branche.
* Le nom de la branche doit être préfixé par les initiales de l’auteur (ex : “sb-“ pour Sébastien Brunelle) suivi de la description des travaux (ex : “sb-ajout-bonnespratiques-github)
* Lorsque les travaux de modifications sont effectués, il est nécessaire de créer une Pull Request (PR) qui doit être validée par au moins un autre membre de l’ANS.
* Une fois la Pull Request validée, c’est à l’auteur des modifications de fusionner (=merge) la pull request avec la branche principale “main”.

A noter qu’aucune modification doit être faite directement dans main.

