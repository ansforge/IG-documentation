# Bonnes pratiques - Documentation des guides d'implémentation de l'ANS v0.1.9

* [**Table of Contents**](toc.md)
* [**Doc Implementer**](doc_implementer.md)
* **Bonnes pratiques**

## Bonnes pratiques

### Gestion des versions

Il est important de prendre en compte qu’une spécification est en **perpétuelle évolution**. Au même titre qu’une application déployée au grand public, des bugs peuvent être découverts, ou des suggestions d’amélioration peuvent être proposées.

C’est la raison pour laquelle, lors du développement d’une spécification, il est conseillé de :

* **Toujours** baser une implémentation sur une version spécifique d’un IG et donc d’un [package FHIR](https://hl7.org/fhir/packages.html) publié dans le [fhir package registry](https://registry.fhir.org). Cela permet à la solution d’indiquer sa conformité à une version donnée d’une spécification. Les ressources traitées par la solution doivent ainsi être conformes aux ressources de conformité indiquées dans une version donnée de l’IG.
* **Anticiper** les futures évolutions de l’API pour les rendre moins douloureuses. Pour cela, une des possibilité est de faire un mapping entre un modèle de base de données et une API FHIR. Lorsqu’une API doit être mise à jour, il est conseillé de maintenir l’ancienne version pendant une durée précise (par ex. un an) avant de la rendre obsolète et de maintir uniquement une nouvelle version.

Une spécification ne peut pas s’arrêter d’évoluer pour une implémentation donnée, le système de versioning permet à chaque implémentation de choisir sa feuille de route pour évoluer vers la dernière release. Un décalage entre la version courante de la spécification et une implémentation est possible, mais il est toujours préférable de le minimiser.

