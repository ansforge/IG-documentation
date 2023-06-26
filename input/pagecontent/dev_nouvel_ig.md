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