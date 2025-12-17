# Collaborons - Documentation des guides d'implémentation de l'ANS v0.1.9

* [**Table of Contents**](toc.md)
* **Collaborons**

## Collaborons

L’interopérabilité française doit se construire de manière collaborative avec un maximum d’acteurs (développeurs, experts métiers, experts interopérabilité…).

FHIR étant très générique de base pour correspondre à tous les cas d’usages, il faut le contraindre pour gagner en interopérabilité. Ces contraintes sont définies au sein des profils, qui doivent être réutilisés au maximum afin d’être amélioré de manière collaborative.

Plusieurs types de profils existent déjà, avec une notion d’héritage :

* les profils génériques, qui forment la base de l’écosystème FHIR français : FrCore et l’Annuaire Santé. Tous les autres profils doivent en dériver par héritage ;
* les profils définis pour des cas d’usages spécifiques ([cf catalogue des guides](https://interop.esante.gouv.fr/ig/fhir))

Pour créer une nouvelle spécification, il sera ainsi nécessaire de :

* Connaître l’écosystème français (connaître les différents guides d’implémentation ainsi que leurs héritages) ;
* Maîtriser les bonnes pratiques définies dans ce guide ;
* Utiliser GitHub (poster des issues ou des Pull Requests) pour diffusion des travaux en open source.

Si un sujet n’est pas encore traité en France, il est possible de proposer un nouveau sujet de travail pour poster un nouveau volet dans le cadre d’interopérabilité français en suivant la [démarche d’élaboration](https://esante.gouv.fr/offres-services/ci-sis/demarche-elaboration).

### Développement de guides d’intéropérabilité externe à vocation d’intégrer le CI-SIS

La création des guides d’implémentation FHIR ayant pour vocation d’intégrer le CI-SIS est ouverte à toute la communauté. On parlera ainsi d’Unité de Production (UP) externe.

Pour que cela soit possible, il convient de respecter plusieurs points :

* Le guide d’implémentation ne doit pas fournir d’avantage commercial à une société (pas de mention de produit / société)
* Les travaux doivent être menés en groupe de travail ouverts à n’importe quel participant
* L’ANS doit être informé de ces travaux avant leur début
* Les travaux doivent être en cohérence avec l’écosystème : pas de chevauchement avec l’existant, héritage des profils FrCore, annuaire santé
* Les [bonnes pratiques](bonnes_pratiques_modeler.md) doivent être respectées, avec un maximum de critères de maturité.
* Une concertation de minimum trois mois doit être lancée sur la plateforme [participez](https://participez.esante.gouv.fr)

Si des travaux ont déjà été entamés, contactez-nous via la l’adresse email du CI-SIS (ci-sis@esante.gouv.fr). Une solution sera établie pour retrouver le cycle de développement classique (transformation au format IG, mise en qualité, héritage FrCore / Annuaire, concertation, …) pour publication dans le CI-SIS.

### Projectathon

L’ANS organise régulièrement des projectathons pour permettre à un industriel de vérifier la conformité de l’implémentation des spécifications d’interopérabilité et de réaliser des tests d’interopérabilité avec d’autres éditeurs.

Vous serez informés par l’ANS des prochains projectathons (date, lieu,…) pour pouvoir y participer.

