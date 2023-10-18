L'interopérabilité française doit se construire de manière collaborative avec un maximum d'acteurs (développeurs, experts métiers, experts interopérabilité...).

FHIR étant très générique de base pour correspondre à tous les cas d'usages, il faut le contraindre pour gagner en interopérabilité. Ces contraintes sont définis au sein des profils qu'il est nécessaire d'utiliser et d'améliorer de manière collaborative. Plusieurs types de profils existent déjà, avec une notion d'héritage :

* les profils fr core et annuaire santé, très génériques doivent être systématiquement hérités et utilisés en France;
* les profils par cas d'usage ([cf liste des guides ANS](https://interop.esante.gouv.fr/ig/fhir)) ou plus largement dans les [volets du ci-sis](https://esante.gouv.fr/offres-services/ci-sis/espace-publication) pour les autres standards.

Pour collaborer, implémenter une spécification, il faudra :

* Connaître l'écosystème français (connaître les différents guides d'implémentation ainsi que leurs héritages) ;
* Maîtriser les bonnes pratiques et connaître FHIR / FSH (comme indiqué dans ce guide) ;
* Utiliser GitHub (poster des issues ou des Pull Requests) : tous les travaux sont diffusés en open source pour faciliter la collaboration.

Si un sujet n'est pas encore traité en France, il est possible de proposer un nouveau sujet de travail pour poster un nouveau volet dans le cadre d'interopérabilité français en suivant la [démarche d'élaboration](https://esante.gouv.fr/offres-services/ci-sis/demarche-elaboration).

### Développement de guides d'intéropérabilité externe à vocation d'intégrer le CI-SIS

La création des guides d'implémentation FHIR ayant pour vocation d'intégrer le CI-SIS est ouverte à toute la communauté. On parlera ainsi d'Unité de Production (UP) externe.

Pour que cela soit possible, il convient de respecter plusieurs points :

* Le guide d'implémentation ne doit pas fournir d'avantage commercial à une société (pas de mention de produit / société)
* Les travaux doivent être menés en groupe de travail ouverts à n'importe quel participant
* L'ANS doit être informé de ces travaux avant leur début
* Les travaux doivent être en cohérence avec l'écosystème : pas de chevauchement avec l'existant, héritage des profils FrCore, annuaire santé
* Les <a href="bonnes_pratiques_modeler.html">bonnes pratiques</a> doivent être respectées, avec un maximum de critères de maturité.
* Une concertation de minimum trois mois doit être lancée sur la plateforme [participez](https://participez.esante.gouv.fr)
