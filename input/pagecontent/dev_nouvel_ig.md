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