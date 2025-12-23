Le guide d’implémentation est un support de publication des spécifications d’interopérabilité, combinant une documentation technique et une documentation narrative sous format web pour définir de manière précise comment sont échangées les données de santé. 

### A qui est destiné cette documentation ?

Cette documentation est séparée en trois parties afin d'adapter le discours à chaque profil :

* Aux [professionnels de santé et établissements de santé](doc_ps.html), qui ont la vision métier et ont la capacité de challenger ces travaux.
* Aux [FHIR modelers](dev_nouvel_ig.html), qui créent ces guides et profilent des ressources
* Aux [FHIR implementers](demarrer_sur_fhir.html), qui lisent ces guides et développent des APIs

La création des guides d'implémentation n’est pas réservée aux seuls organismes de normalisation et de régulation (comme InteropSanté ou l’ANS) : tout acteur peut en publier afin de documenter un besoin métier identifier ou une interface, à condition qu’elles soient cohérentes avec l’écosystème français et compatibles avec les guides d’implémentation nationaux, notamment permis grâce au mécanisme d’héritage. L’objectif de ces guides est d’encourager la participation de l’ensemble des parties prenantes.

### L'intérêt des guides d'implémentation

Le guide d'implémentation est versionné (l'ensemble des versions reste accessible) et packagé. Une spécification n'est jamais figée : elles restent ouvertes à l’évolution et peuvent être adaptées en fonction des contributions et des retours de l'ensemble des lecteurs.

Chaque guide d'implémentation est associé à un périmètre, à un cas d'usage, à un métier, ce qui permet permet :

* De gérer les versions des guides de manière séparée : on peut ainsi mettre à jour chacune des specs séparément sans avoir à mettre à jour celles qui ne sont pas concernées
* De gérer les dépendances indépendamment des autres guides : dépendances aux ressources du ci-sis, aux profils interopsanté, ...
* Les urls sont claires, on sait directement de quelle spécification est issue chaque profil, et on peut directement accéder à l'IG en connaissant l'url canonique de l'IG
* Les documentations génériques peuvent être surspécifiées pour réutiliser certains profils pour un autre cas d'usage, en héritant de tout ou partie, ou pour décrire une implémentation précise
* L'IG doit obligatoirement hériter des profils FHIR réalisés par InteropSanté et/ou par l'ANS (s'ils existent) pour être conforme au cadre national.

### La liste des guides d'implémentation de l'ANS

La liste des guides d'implémentation est accessible [à cette adresse](https://interop.esante.gouv.fr/ig/).

### Reporter un problème ou une suggestion d'amélioration

Vous avez identifié une erreur sur un des guides ? Le lien `issue` permet de signaler un problème sur un projet donné.

<img width="100%" alt="image" src="https://user-images.githubusercontent.com/48218773/215773144-31a47623-a853-4a4e-8ba0-ad1d66b29961.png">

Un lien est également disponible sous chaque guide d'implémentation pour accéder aux issues :

<img width="100%" alt="image" src="new_issue.png">

L'issue doit contenir un titre, et une description la plus détaillée possible avec idéalement une proposition de changement pour faciliter et améliorer la qualité des modifications apportées.

### Documentation

* [ImplementationGuide](https://www.hl7.org/fhir/implementationguide.html)
* [Packages](https://confluence.hl7.org/display/FHIR/NPM+Package+Specification)