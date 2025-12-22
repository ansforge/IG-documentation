# Documentation des professionnels de santé - Documentation des guides d'implémentation de l'ANS v0.1.9

* [**Table of Contents**](toc.md)
* **Documentation des professionnels de santé**

## Documentation des professionnels de santé

### L’interopérabilité en santé

L’interopérabilité désigne la capacité des logiciels de santé à **`partager et intégrer`** des données de santé.

Par exemple, les dates peuvent s’écrire dans différents formats : 22 décembre 2027, 22/12/2027, 22-12-2027, 12/22/2027 aux Etats-Unis, etc …

L’objectif de l’interopérabilité est de **désigner un format commun** pour les dates, les résultats de biologie, les pathologies, les symptômes, les données administratives, etc …

Capture d'écran du webinaire d'[introduction à l'interopérabilité](https://www.youtube.com/watch?v=JGmJWUkX1nU)

Dans votre pratique quotidienne, cela signifie que les informations patient que vous saisissez dans votre logiciel peuvent être partagées de manière sécurisée et structurée avec d’autres logiciels, et ainsi vous permettre de :

* Partager des données entre différents logiciels (par exemple, les données du serveur de résultats de biologie se retrouvent automatiquement dans votre logiciel de soin).
* Faire des projets de recherche (extraire automatiquement des informations d’intérêt)

Une mauvaise compréhension des données par les logiciels peut provoquer des erreurs dans la prise en charge des patients. Ainsi, l’objectif de l’interopérabilité est de garantir que ces données restent exploitables et compréhensibles par tous les acteurs du parcours de soins et de la recherche clinique, indépendamment des outils utilisés.

### Le rôle des professionnels de santé (PS) et établissements de santé (ES) dans l’interopérabilité

Les données de santé sont complexes et nécessitent une expertise métier forte pour les comprendre. Par exemple, la structure de la posologie : elle peut contenir un nombre de comprimé minimal, maximal, des conditions de prises (ex : si douleur), une durée, une fréquence, … Il est dans ce cas indispensable qu’un prescripteur détermine tout ce qui est attendu d’une structuration de posologie pour que les experts interopérabilité puissent décrire de manière concise et précis les objets contenant ces informations.

Idéalement, une spécification d’interopérabilité doit être construite de manière rapprochée entre un expert métier comme un professionnel de santé et un expert interopérabilité.

### Le standard FHIR

FHIR (Fast Healthcare Interoperability Resources) est un standard international développé par HL7 pour faciliter l’échange de données de santé. Concrètement, FHIR définit des “ressources” standardisées (Patient, Consultation, Prescription, etc.) qui représentent les concepts métier que vous utilisez quotidiennement. Grâce à FHIR, les informations que vous produisez peuvent être comprises par n’importe quel système compatible, permettant ainsi une meilleure coordination des soins et réduisant les ressaisies manuelles d’informations.

Ce standard est commun à tous les cas d’usages car il est international : recherche, biologie, administratif, …. Pour gagner en interopérabilité, il faut le spécialiser pour la France, pour l’Europe et pour chaque cas d’usages dans des guides d’implémentation.

### Les guides d’implémentation

Un guide d’implémentation (IG) est un document technique qui précise comment utiliser le standard FHIR dans un contexte spécifique, par exemple pour un programme national de santé ou un cas d’usage particulier. Il définit les règles et contraintes adaptées aux besoins métier français : quelles données sont obligatoires, quels formats utiliser, quelles nomenclatures respecter (CIM-10, CCAM, etc.). Pour vous, professionnels de santé, cela signifie que votre logiciel respecte des règles communes avec les autres systèmes, garantissant ainsi la qualité et la cohérence des échanges.

### Les modèles logiques

Un modèle logique est une représentation structurée et simplifiée des données métier, indépendante de toute technologie. Il décrit “ce qui doit être échangé” (par exemple : les informations essentielles d’une consultation) sans entrer dans les détails techniques du “comment”. Les modèles logiques servent de pont entre votre compréhension métier des soins et la représentation technique en FHIR. Ils permettent de valider que les spécifications techniques répondent bien à vos besoins professionnels avant leur mise en œuvre dans les logiciels.

