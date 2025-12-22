# Quick start FHIR - Documentation des guides d'implémentation de l'ANS v0.1.9

* [**Table of Contents**](toc.md)
* [**Doc Implementer**](doc_implementer.md)
* **Quick start FHIR**

## Quick start FHIR

Nos guides d’implémentation se basent sur la norme HL7 FHIR. Ils utilisent la terminologie, les notations et les principes de conception propres à FHIR. Avant de lire le guide d’implémentation, il est important de se familiariser avec certains des principes de base de FHIR ainsi qu’avec des conseils généraux sur la façon de lire les spécifications FHIR. Les lecteurs qui ne connaissent pas FHIR sont encouragés à lire (ou au moins à survoler) ce qui suit avant d’explorer plus en avant nos guides d’implémentation.

Liste des implémentations open source :

*  [Implementation Support Module](https://hl7.org/fhir/R4/implsupport-module.html) 
*  [Implémentations open source](https://confluence.hl7.org/display/FHIR/Open+Source+Implementations) 
*  [FHIR Foundry](https://foundry.hl7.org) 

Documentation FHIR :

*  [Vue d'ensemble de FHIR](http://hl7.org/fhir/R4/overview.html) 
*  [Introduction pour les développeurs](http://hl7.org/fhir/R4/overview-dev.html) 
*  [Types de données FHIR](http://hl7.org/fhir/R4/datatypes.html) 
*  [Utilisation des codes](http://hl7.org/fhir/R4/terminologies.html) 
*  [Références entre ressources](http://hl7.org/fhir/R4/references.html) 
*  [Comment lire les définitions des ressources et des profils](http://hl7.org/fhir/R4/formats.html) 
*  [Ressource de base](http://hl7.org/fhir/R4/resource.html) 
*  [Opérations RESTful](http://hl7.org/fhir/R4/http.html) 
*  [Recherche](http://hl7.org/fhir/R4/search.html) 

N’hésitez pas à explorer d’autres aspects de la spécification FHIR qui vous semblent pertinents ou intéressants par rapport à vos besoins.

### Le Serveur Multi Terminologies

Les artifacts terminologiques (Terminologies et Jeux de Valeurs) pour usage français sont accessibles par consultation du [Serveur Multi Terminologies (SMT)](https://smt.esante.gouv.fr) de l’ANS. Le SMT permet d’accéder à ces artifacts de différentes manières : par API FHIR, par interface graphique, par des requêtes SPARQL … Ce service est complémentaire aux guides d’implémentation en permettant d’obtenir, via des jeux de valeurs (ValueSet), l’ensemble des concepts codés pour un contexte particulier.

Ces jeux de valeurs peuvent reprendre des concepts définis dans des terminologies de deux manières : via l’ajout de concept unitaire, ou via l’ajout de règles logiques (Exemple : l’ensemble des pathologies du système nerveux de la terminologie CIM-10).

Pour accéder à la liste de codes associés à un jeu de valeurs indiqué en utilisant une règle logique, il existe une opération FHIR appelée [$expand](https://www.hl7.org/fhir/R4/valueset-operation-expand.html) permettant d’obtenir l’ensemble des codes par expansion. Cette opération est permise par le FHIR Terminology Service du Serveur Multi Terminologique dans les cas où les terminologies sont disponibles.

