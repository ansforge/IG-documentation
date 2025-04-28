Nos guides d'implémentation se basent sur la norme HL7 FHIR. Ils utilisent la terminologie, les notations et les principes de conception propres à FHIR. Avant de lire le guide d'implémentation, il est important de se familiariser avec certains des principes de base de FHIR ainsi qu'avec des conseils généraux sur la façon de lire les spécifications FHIR. Les lecteurs qui ne connaissent pas FHIR sont encouragés à lire (ou au moins à survoler) ce qui suit avant d'explorer plus en avant nos guides d'implémentation.

Liste des implémentations open source :

<ul>
  <li>
   <a href="https://hl7.org/fhir/R4/implsupport-module.html">Implementation Support Module</a>
  </li>
    <li>
   <a href="https://confluence.hl7.org/display/FHIR/Open+Source+Implementations">Implémentations open source</a>
  </li>
    <li>
   <a href="https://foundry.hl7.org">FHIR Foundry</a>
  </li>
</ul>

Documentation FHIR :

<ul>
  <li>
   <a href="http://hl7.org/fhir/R4/overview.html">Vue d'ensemble de FHIR</a>
  </li>
  <li>
   <a href="http://hl7.org/fhir/R4/overview-dev.html">Introduction pour les développeurs</a>
  </li>
  <li>
   <a href="http://hl7.org/fhir/R4/datatypes.html">Types de données FHIR</a>
  </li>
  <li>
   <a href="http://hl7.org/fhir/R4/terminologies.html">Utilisation des codes</a>
  </li>
  <li>
   <a href="http://hl7.org/fhir/R4/references.html">Références entre ressources</a>
  </li>
  <li>
   <a href="http://hl7.org/fhir/R4/formats.html">Comment lire les définitions des ressources et des profils</a>
  </li>
  <li>
   <a href="http://hl7.org/fhir/R4/resource.html">Ressource de base</a>
  </li>
  <li>
   <a href="http://hl7.org/fhir/R4/http.html">Opérations RESTful</a>
  </li>
  <li>
   <a href="http://hl7.org/fhir/R4/search.html">Recherche</a>
  </li>
 </ul>

N'hésitez pas à explorer d'autres aspects de la spécification FHIR qui vous semblent pertinents ou intéressants par rapport à vos besoins.

### Le Serveur Multi Terminologies

Les artifacts terminologiques (Terminologies et Jeux de Valeurs) pour usage français sont accessibles par consultation du [Serveur Multi Terminologies (SMT)](https://smt.esante.gouv.fr) de l'ANS. Le SMT permet d'accéder à ces artifacts de différentes manières : par API FHIR, par interface graphique, par des requêtes SPARQL ... Ce service est complémentaire aux guides d'implémentation en permettant d'obtenir, via des jeux de valeurs (ValueSet), l'ensemble des concepts codés pour un contexte particulier.

Ces jeux de valeurs peuvent reprendre des concepts définis dans des terminologies de deux manières : via l'ajout de concept unitaire, ou via l'ajout de règles logiques (Exemple : l'ensemble des pathologies du système nerveux de la terminologie CIM-10).

Pour accéder à la liste de codes associés à un jeu de valeurs indiqué en utilisant une règle logique, il existe une opération FHIR appelée [$expand](https://www.hl7.org/fhir/R4/valueset-operation-expand.html) permettant d'obtenir l'ensemble des codes par expansion. Cette opération est permise par le FHIR Terminology Service du Serveur Multi Terminologique dans les cas où les terminologies sont disponibles.
