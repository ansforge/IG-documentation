### Le choix de la version FHIR

Avant de commencer à développer un guide d'implémentation, il faut choisir la version de FHIR sur laquelle se baser : R4, R4B, R5 ? 

A l'heure actuelle, l'écosystème français est en R4 (fr-core, IG ANS, Annuaire, ROR...). 

L'objectif étant d'avoir un écosystème uniforme et simple qui hérite systématiquement de fr-core pour avoir des modélisations les plus cohérentes possibles. Il est ainsi préférable d'utiliser R4, pour profiter de l'héritage de fr-core et des volets du ci-sis, et ne pas être "hors système".

Travailler sur R4 et R5 parallèlement engendre beaucoup de questions : doubles travaux de maintenance, nécessité de maintenir des mappings/connecteurs entre versions (R4 <-> R5, R4 <-> R6, R5 <-> R6), augmentation de la complexité de l'écosystème avec certains acteurs en R4, d'autres en R5...
Les ressources étant limitées, il est préférable de se concentrer sur l'amélioration de nos profils nationaux en R4 et de faire monter l'écosystème en compétences.

La release R5 reste cependant intéressante, notamment pour sa documentation et certaines ressources améliorées (Documentation FHIR Search, Ressources MedicinalProduct, ...). 
Ce choix n'est pas tranché, et il s'agit bien de l'écosystème qui dictera quelle version utiliser. Si vous ressentez un besoin d'utiliser R5 (notamment pour des cas d'usages internationaux ou profiter de ressources non matures en R4), nous vous invitons à nous le signaler pour réévaluer le bénéfice/risque de travailler sur FHIR R5.

A noter que FHIR R6, dont la première concertation est prévue mi-2024, apportera beaucoup de contenu normatif. Grahame Grieve a ainsi proposé de faire l'effort de transition sur R6.

### Mise en place du repo GitHub

Prérequis:
* Avoir un [compte GitHub](https://ansforge.github.io/Documentation/pages/docs/github.html)
* L'associer à l'[organisation ANS](https://ansforge.github.io/Documentation/pages/quick-start/biencommencer.html)
* Lire la documentation [best practice](https://build.fhir.org/ig/FHIR/ig-guidance/best-practice.html)

Tâche:
* Créer un [nouveau repository](https://github.com/organizations/ansforge/repositories/new) public en utilisant le template ansforge/FIG_ans-ig-sample.
* Nommer le repository pour qu'il soit facilement retrouvé et compréhensible par n'importe qui : Descriptif, lisible, cohérent, contextuel, extensible, réutilisable, bref. Il doit être préfixé par "IG-"[...]. Exemple : IG-fhir-partage-de-documents-de-sante. N'hésitez pas à demander avis à la team interop :)
* Mettre à jour le README selon le template proposé

L'IG est créé! Il faut maintenant le personnaliser

### Paramétrage de l'IG

Lors de la création d'un IG, il y a une première phase de paramétrage à effectuer. Il faut remplir:
* Le fichier [sushi-config](https://fshschool.org/docs/sushi/configuration/), avec:
   * l'id, qui sera également l'id du package, qui doit s'appeler "ans.fhir.fr.[codeprojet]"
   * l'url canonique, au format https://interop.esante.gouv.fr/ig/fhir/[codeprojet], avec [codeprojet] identique à celui du package id et en minuscule
   * le nom, le titre ...
* Rapporter les mêmes modifications dans package-list:
   * package-id, titre, url canonique, introduction descriptive...
* modifier le paramètre ig dans ig.ini pour qu'il soit de la forme fsh-generated/resources/ImplementationGuide-[package-id].json --> Cette étape est nécessaire, sans cela, il y aura des erreurs.
* Le fichier input/data/features.yml : mettre à jour le lien vers la github issue


### Paramétrage du menu de navigation de l'IG

Une des plus importantes parties de l'IG est la document narrative, celle-ci est écrite en [markdown](https://www.markdownguide.org/basic-syntax).
Ces pages sont à ajouter dans input/pagecontent avec l'extension .md. A noter que ces pages doivent être directement contenues dans le dossier pagecontent et ne peuvent pas avoir d'arborescence de fichiers.

Une fois une page créée et rédigée, pour l'ajouter au menu, il faut éditer le fichier sushi-config.yaml. Celui-ci contient deux parties : 

#### La partie pages

La partie pages est optionnelle, mais elle permet de donner un titre aux pages (par défaut, c'est le nom du fichier qui est utilisé). A noter, il faut utiliser l'extension .md ici.

La partie pages est de la forme:

```
pages:
    index.md:
        title: Accueil
    specifications_techniques.md:
        construction_des_flux.md:
        st_ajout.md:
            title: Ajout d'un lot de documents
```

Pour rédiger les pages, suivre la syntaxe [kramdown](https://kramdown.gettalong.org/syntax.html)

#### La partie menu

La partie menu permet de définir le menu de navigation dans le header. A noter, il faut utiliser l'extension .html.


La partie menu est de la forme:

```
menu:
  Accueil: index.html
  Spécifications techniques:
      Construction des flux: construction_des_flux.html
      Flux 01: st_flux1.html
      Flux 02: st_flux2.html
  Spécifications fonctionnelles:
```

### Développement de l'IG

Le développement de l'IG se fait essentiellement dans le dossier [input](https://build.fhir.org/ig/FHIR/ig-guidance/using-templates.html#igroot-input).


Lien vers quelques exemples :
https://github.com/HL7/US-Core/blob/master/sushi-config.yaml
https://github.com/ansforge/FIG_ans-ig-PDSm/blob/main/sushi-config.yaml