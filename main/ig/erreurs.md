# Les erreurs courantes - Documentation des guides d'implémentation de l'ANS v0.1.9

* [**Table of Contents**](toc.md)
* [**Doc Modeler**](doc_modeler.md)
* **Les erreurs courantes**

## Les erreurs courantes

### Erreur NullPointerException

* java.lang.NullPointerException: Cannot invoke “org.hl7.fhir.r5.model.DataType.isPrimitive()” because “type” is null L’erreur vient du fait qu’il y a des fichiers qui ne finissent pas par .md ou par .xml dans pagecontent

### Erreur Missing Snapshot

FSH nécessite d’avoir des packages avec snapshot et differential. Il est possible de générer les snapshots dans le FHIR CACHE:

* Installer dotnet sdk : https://dotnet.microsoft.com/en-us/download
* Lancer la commande `dotnet tool install --global Firely.Terminal --version 3.0.0`

Exemples d’usage :

* `fhir bake --package hl7.fhir.fr.core`
* `fhir bake --package ans.annuaire.fhir.r4`
* `fhir bake --package ans.cisis.fhir.r4`

Source : https://fshschool.org/docs/sushi/running/#structure-definition-is-missing-snapshot-error

