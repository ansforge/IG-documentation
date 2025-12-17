# Tests - Documentation des guides d'implémentation de l'ANS v0.1.9

* [**Table of Contents**](toc.md)
* **Tests**

## Tests

### Organisation des tests

#### Espace de test

L’espace de test est composé de deux outils :

* EVSClient, qui permet de vérifier la conformité : des documents CDA, des archives IHE_XDM.ZIP utilisées pour les échanges, des ressources FHIR…
* Gazelle Test Management, qui permet de tester des scénarios complets avec plusieurs interactions d’échanges de données.

Ces outils sont accessibles en ligne sur le site [https://interop.esante.gouv.fr/](https://interop.esante.gouv.fr/) et notamment utilisés lors des Projectathons organisés par l’ANS pour les éditeurs.

### Matchbox

Matchbox est un outil permettant notamment de valider des instances de ressources FHIR contre un profil. L’outil matchbox est [open source](https://github.com/ahdis/matchbox).

#### Accès à Matchbox et à la validation

L’instance matchbox de l’ANS est accessible via [cette URL](https://interop.esante.gouv.fr/matchboxv4).

Cette instance permet de faire des vérification au regard :

* Des guides d’implémentation de l’ANS
* Des guides d’implementation d’InteropSanté
* Du FHIR Terminology Service (FTS) du Serveur Multi Terminologique ([SMT](https://smt.esante.gouv.fr/)).

Pour valider une ressource FHIR contre un profil, il suffit de cliquer sur le bouton “Validate ressource”

#### Chargement de la ressource FHIR à valider

Sur cette deuxième page, il suffira de déposer le fichier contenant la ressource FHIR à valider. Optionnellement, il est possible de sélectionner le numéro de version du guide d’implémentation ainsi que le profil à valider. A défaut, le profil à valider sera défini automatiquement à partir de l’attribut meta.profile.

#### Résultat de la validation

Vous obtiendrez ainsi le résultat de la validation, à noter que les codes et les displays sont validés par le FHIR Terminology Service (FTS) du Serveur Multi Terminologique ([SMT](https://smt.esante.gouv.fr/)).

Une fois validé, les messages d’erreurs sont accessibles en-dessous :

Un détail par ligne est également accessible :

### Gazelle

Gazelle est un outil de tests qui s’appuie sur des validateurs tel que matchbox pour FHIR pour établir des scénarios de tests complets.

### Les niveaux des scénarios gazelle

Différents niveaux de tests sont proposés sur l’espace de test de l’ANS afin d’aider les éditeurs dans leur préparation aux évènements de type projectathon.

Le niveau le plus bas permettra aux éditeurs de tester la conformité des messages unitaires qu’ils produisent. Le niveau intermédiaire permettra aux éditeurs de tester face à un autre système la conformité et l’interopérabilité des messages unitaires. Le niveau le plus élevé correspond aux scénarios proposés jusqu’à maintenant dans le cadre des projectathons et permettra aux éditeurs de tester des scénarios complexes face à un autre système.

##### Niveau 1 (N1)

Les tests de niveau 1 sont des tests unitaires sans partenaire. Chaque cas de test de niveau 1 correspond à un flux de la spécification technique. L’objectif de ces cas de tests est de valider la ressource ou la requête produite par le système avec un validateur EVSClient indiqué dans le cas de test.

##### Niveau 2 (N2)

Les tests de niveau 2 sont des tests unitaires avec partenaire. Pour être exécutés, il faut qu’au préalable les cas de test de niveau 1 indiqués en prérequis aient été exécutés par les 2 mêmes systèmes. L’objectif de ces cas de test est de valider la ressource ou la requête construite ainsi que la capacité des systèmes à créer / intégrer ou requêter / envoyer des ressources. Les cas de tests de type N2 correspondent généralement à un flux spécifique.

##### Niveau 3 (N3)

Les tests de niveau 3 sont des tests avec partenaire basés sur l’enchaînement de différents tests unitaires avec partenaire (N2) en suivant un scénario complexe. Pour être exécutés, il faut qu’au préalable les cas de test de niveaux 1 et 2 indiqués en prérequis aient été exécutés entre les 2 mêmes systèmes.

L’objectif de ces cas de test est de créer un scénario complexe faisant appel aux différents flux de la spécification technique et ainsi créer un exemple d’usage.

#### Les types d’étapes de cas de tests

Les étapes de cas de tests pourront avoir plusieurs types.

| | |
| :--- | :--- |
| [TRANSACTION] | Ce type d’étape concerne une transaction entre un serveur et un client |
| [PREUVE] | Ce type d’étape est une demande de preuve (screenshot, lien permanent…) à l’attention du moniteur |
| [INFORMATION] | Message informatif à l’attention de l’editeur concernant le fonctionnement du cas de test |
| [VALIDATION] | Ce type d’étape est une demande de validation d’une ressource sur EVSClient |
| [INSTRUCTION] | Ce type d’étape est une action demandée à l’éditeur sans preuve exigée |

#### Usage du proxy

Le proxy sert à intercepter les messages entre le client et le serveur, pour validation par le moniteur. Celui-ci devra être utilisé pour les cas de tests de niveaux N2 et N3.

### HAPI FHIR

Ce serveur FHIR open source est particulièrement utile pour importer des profils et tester la validité des ressources générées contre les profils.

