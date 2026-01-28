# Valider une ressource contre un profil - Documentation des guides d'implémentation de l'ANS v0.1.9

* [**Table of Contents**](toc.md)
* [**Doc Implementer**](doc_implementer.md)
* **Valider une ressource contre un profil**

## Valider une ressource contre un profil

Cette page a pour but d’expliquer comment valider qu’une instance de ressource est conforme à un profil. Elle est particulièrement utile lors de la phase de modélisation de nouveaux profils, ou lors de la création d’exemples.

Cette documentation est destinée aux:

* Développeurs qui veulent tester leurs instances contre un profil
* Rédacteurs de spécifications pour tester leurs profils élaborés à partir de forge ou de fsh

Pour tester les profils, il faudra avoir à disposition: 1. la / les StructureDefinition (des profils, des extensions …) qui indiquent les contraintes, 2. une ou plusieurs instances de ces profils à tester.

### Validation via Gazelle

La plateforme de test [Gazelle](https://interop.esante.gouv.fr/), et plus particulièrement EVSClient, est la plateforme à privilégier.

### Validation avec une interface graphique

Plusieurs projets open-source permettent de valider des ressources FHIR via l’interface graphique d’un site web :

* [FHIR Validator](https://validator.fhir.org)
* [Matchbox]([https://test.ahdis.ch/matchbox](https://test.ahdis.ch/matchbox/#/))

### Validation avec HAPI FHIR et l’opération $Validate

Le serveur HAPI utilise le validateur FHIR. Il est ainsi possible d’utiliser HAPI et l’opération $validate. Les urls définies ci-dessous pointent vers le serveur public d’HAPI, mais cette documentation reste valide sur tous les serveurs HAPI déployés en ligne ou en local.

#### Etape 1 : poster les StructureDefinition sur HAPI FHIR

Les StructureDefinition peuvent être accessibles sous deux formes:

* Sous forme d’un package pour un cas d’usage particulier, c’est sous cette forme qu’ils sont définis dans le [FHIR REGISTRY](https://registry.fhir.org/) (dans les ImplementationGuide, un package est systématiquement généré à l’adresse [url]/package.tgz, ex : [https://www.hl7.org/fhir/us/core/package.tgz])
* Le / les profils ne sont pas issus d’un contexte particulier et se présentent sous forme d’un ficher xml ou json (pratique à déconseiller)

##### Cas a : à partir d’un package

Les packages sont très intéressants pour valider les ressources, car ils contiennent l’intégralité des ressources d’un Implementation Guide, et plus particulièrement l’ensemble des StructureDefinition des extensions et des profils. Le package permet donc de s’assurer que tout ait bien été importé sur HAPI et que toutes les StructureDefinition de conformité soient bien à disposition pour valider les instances.

Pour importer un package issu d’un Implementation Guide, il suffit d’utiliser ce script python: [https://github.com/nmdp-bioinformatics/igloader]

##### Cas b : à partir d’un json

Prérequis : une StructureDefinition au format JSON ou XML avec le snapshot populé (dans forge, il y a une option persistante permettant de générer en permanence le snapshot).

Attention : Si vous utilisez ce cas b, assurez-vous que l’ensemble des StructureDefinition soient bien fournies, c’est à dire celles des extensions, des datatypes profilés, etc…

Pour exporter une StructureDefinition vers HAPI, il y a deux possibilités:

* via une requête HTTP POST vers `https://hapi.fhir.org/baseR4/StructureDefinition` en mettant la StructureDefinition dans le body de la requête.
* via l’interface graphique de HAPI `https://hapi.fhir.org/resource?serverId=home_r4&pretty=false&_summary=&resource=StructureDefinition` > CRUD Operations > Create (Note : limité à 10.000 caractères)

#### Etape 2 : valider une instance contre un profil

Prérequis : disposer d’une instance de ressource, l’url du profil doit être définie dans Resource.meta.profile

Lorsque l’ensemble des StructureDefinition (snapshot) nécessaires à la validation d’un profil (profils, extensions…) est importé dans HAPI, il devient possible de valider une instance contre un profil. Pour cela, il faudra utiliser l’opération [$validate](https://www.hl7.org/fhir/resource-operation-validate.html) définie par la spec FHIR.

Cette opération peut s’utiliser de deux façons:

* Via une requête HTTP POST vers `https://hapi.fhir.org/baseR4/[ResourceType]/$validate?_format=json&_pretty=true` en remplaçant ResourceType par le nom de la ressource à tester et en mettant l’instance dans le bundle
* Via l’interface graphique de HAPI `https://hapi.fhir.org/resource?serverId=home_r4&pretty=false&_summary=&resource=[ResourceType]` > CRUD Operations > validate

#### Ressources supplémentaires

* [Documentation officielle : valider une ressource](https://confluence.hl7.org/pages/viewpage.action?pageId=35718864#ProfileTooling-ValidatingResourcesagainstProfiles)
* [Documentation officielle : validateur FHIR](https://confluence.hl7.org/display/FHIR/Using+the+FHIR+Validator)

