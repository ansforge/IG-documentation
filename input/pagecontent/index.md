
Le guide d’implémentation est un support de publication des spécifications d’interopérabilité, combinant une documentation technique et une documentation narrative. Il n’est pas réservé aux seuls organismes de normalisation (comme InteropSanté ou l’ANS) : tout acteur peut en publier afin de rendre visibles ses spécifications, à condition qu’elles soient cohérentes avec l’écosystème français et compatibles avec les guides d’implémentation nationaux, notamment permis grâce au mécanisme d’héritage.

Ce guide d'implémentation "documentation" contient l'ensemble des bonnes pratiques de création de guides d'implémentation pour les FHIR modelers, ainsi que la documentation sur "comment lire un guide d'implémentation" pour un implémenteur.

L’objectif est d’encourager la participation de l’ensemble des parties prenantes. Bien qu’il existe déjà des publications versionnées, celles-ci ne sont pas définitives : elles restent ouvertes à l’évolution et peuvent être adaptées en fonction des contributions et des retours de l'ensemble des lecteurs.

### Les guides d'implémentation

Un guide d'implémentation se présente sous forme d'un site web contenant un ensemble cohérent de ressources de conformité pour répondre à une problématique particulière. Le guide d'implémentation est versionné (l'ensemble des versions reste accessible) et packagé.

La meilleure pratique consiste à créer un guide d'implémentation par projet bien spécifique, cela permet :

* De versionner séparément, on peut ainsi mettre à jour chacune des specs séparément sans avoir à mettre à jour celles qui ne sont pas concernées
* Chacune des specs gère ses dépendances indépendamment des autres (aux ressources du ci-sis, aux profils interopsanté), chacune de ces dépendances peuvent être mises à jour séparément
* Les urls sont claires, on sait directement de quelle spécification est issue chaque profil, et on peut directement accéder à l'IG en connaissant l'url canonique de l'IG
* Les documentations génériques peuvent être surspécifiées pour réutiliser certains profils pour un autre cas d'usage, en héritant de tout ou partie, ou pour décrire une implémentation précise
* L'IG doit obligatoirement hériter des profils FHIR réalisés par InteropSanté et/ou par l'ANS s'ils existent.

Documentation : [ImplementationGuide](https://www.hl7.org/fhir/implementationguide.html), [Packages](https://confluence.hl7.org/display/FHIR/NPM+Package+Specification)

### A qui est destiné cette documentation ?

Il est destiné à celles et ceux qui utilisent FHIR :

* Aux professionnels de santé et établissements de santé, qui ont la vision métier et ont la capacité de challenger ces travaux.
* Aux FHIR modelers, qui créent ces guides et profilent des ressources
* Aux FHIR implementers, qui lisent ces guides et développent des APIs

Pour plus d'informations sur la modélisation ou l'implémentation FHIR, il suffit de naviguer au sein du menu de ci-dessus.

### La liste des guides d'implémentation de l'ANS

La liste des guides d'implémentation est accessible [à cette adresse](https://interop.esante.gouv.fr/ig/).

### Reporter un problème ou une suggestion d'amélioration

Vous avez identifié une erreur sur un des guides ? Le lien `issue` permet de signaler un problème sur un projet donné.

<img width="100%" alt="image" src="https://user-images.githubusercontent.com/48218773/215773144-31a47623-a853-4a4e-8ba0-ad1d66b29961.png">

Un lien est également disponible sous chaque guide d'implémentation pour accéder aux issues :

<img width="100%" alt="image" src="new_issue.png">

L'issue doit contenir un titre, et une description la plus détaillée possible avec idéalement une proposition de changement pour faciliter et améliorer la qualité des modifications apportées.
