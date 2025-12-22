# Quick start IG - Documentation des guides d'implémentation de l'ANS v0.1.9

* [**Table of Contents**](toc.md)
* [**Doc Modeler**](doc_modeler.md)
* **Quick start IG**

## Quick start IG

### Mise en place du repo GitHub

Prérequis : suivre la [documentation](https://ansforge.github.io/Documentation) pour créer un compte GitHub et l’associer à l’organisation ANS.

Ce nouveau projet doit utiliser le GitHub template ansforge/IG-modele et doit respecter la convention de nommage indiquée dans la [documentation de création des répetoires GitHub](https://ansforge.github.io/Documentation/pages/docs/creationprojet.html) tout en étant préfixé par “IG-…” (Exemple : IG-fhir-partage-de-documents-de-sante). En cas de doute, l’équipe interopérabilité de l’ANS se tient disponible pour avis.

Une fois l’IG créé, il est nécessaire de le personnaliser pour le projet dédié.

### Paramétrage de l’IG

Lors de la création d’un IG, il y a une première phase de paramétrage à effectuer. Il faut remplir:

* Le fichier [sushi-config](https://fshschool.org/docs/sushi/configuration/), avec: 
* l’id, qui sera également l’id du package, qui doit s’appeler “ans.fhir.fr.[codeprojet]”
* l’url canonique, au format https://interop.esante.gouv.fr/ig/fhir/[codeprojet], avec [codeprojet] identique à celui du package id et en minuscule
* le nom, le titre …
 
* Rapporter les mêmes modifications dans package-list: 
* package-id, titre, url canonique, introduction descriptive…
 
* modifier le paramètre ig dans ig.ini pour qu’il soit de la forme fsh-generated/resources/ImplementationGuide-[package-id].json –> Cette étape est nécessaire, sans cela, il y aura des erreurs.
* Le fichier input/data/features.yml : mettre à jour le lien vers la github issue

Il faudra également mettre à jour le fichier readme.md à la racine du repository.

### Paramétrage du menu de navigation de l’IG

Une des plus importantes parties de l’IG est la documentation narrative, celle-ci est écrite en [kramdown](https://kramdown.gettalong.org/). Ces pages sont à ajouter dans input/pagecontent avec l’extension .md. A noter que ces pages doivent être directement contenues dans le dossier pagecontent et ne peuvent pas avoir d’arborescence de dossiers.

Une fois une page créée et rédigée, pour l’ajouter au menu, il faut éditer le fichier sushi-config.yaml. Celui-ci contient deux parties : la partie pages et la partie menu

#### La partie pages

La partie pages est optionnelle, mais elle permet de donner un titre aux pages (par défaut, c’est le nom du fichier qui est utilisé). A noter, il faut utiliser l’extension .md ici.

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

#### La partie menu

La partie menu permet de définir le menu de navigation dans le header. A noter, il faut utiliser l’extension .html.

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

### Développement de l’IG

Le développement de l’IG se fait essentiellement dans le dossier [input](https://build.fhir.org/ig/FHIR/ig-guidance/using-templates.html#igroot-input).

Lien vers quelques exemples : [https://github.com/HL7/US-Core/blob/master/sushi-config.yaml] [https://github.com/ansforge/FIG_ans-ig-PDSm/blob/main/sushi-config.yaml]

### Installer les dépendances

### Windows

Prérequis :

* Avoir les droits administrateur

#### Etape 1. Installer VS CODE et les plugins

https://code.visualstudio.com/

* [Requis] “[FHIR Shorthand](https://marketplace.visualstudio.com/items?itemName=FHIR-Shorthand.vscode-fsh)”
* [Requis] “[Markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)”
* [Optionnel] “[Markdown Preview Enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)”
* [Optionnel] “[Kodjin FHIR Profiler](https://marketplace.visualstudio.com/items?itemName=edenlabio.fhir-profiler-tool)”
* [Optionnel] “[codfsh](https://github.com/gematik/codfsh)”

1. Lancer VS Code
1. Aller dans le menu extension (les 4 carrés dont un qui se décolle à gauche), chercher et installer “FHIR Shorthand”

#### Etape 2. Installer NodeJS

[https://nodejs.org/en/]

La case “Automatically install the necessary tools” peut être cochée.

#### Etape 3. Installer SUSHI

1. Lancer l’invite de commande (windows > “invite de commande”)
1. Ecrire et lancer la commande`npm install -g fsh-sushi`

#### Etape 4. Installer les dépendances de l’IG Publisher

* JAVA JDK: https://www.oracle.com/fr/java/technologies/downloads/#jdk19-windows (installer, au format .exe)
* Ruby: https://rubyinstaller.org/downloads (with devkit). Installer le “MSYS2 base installation”.
* Jekyll et bundler: lancer l’invite de commande en mode administrateur et lancer la commande `gem install jekyll bundler`

#### Etape 5. Lancer l’IG Publisher

Télécharger le repository [ansforge/FIG_ans-ig-sample](https://github.com/ansforge/FIG_ans-ig-sample) : code > download zip. Décompresser le dossier, et le mettre dans un chemin où il n’y a pas d’espace (exemple : C:\Users\nriss\Documents).

Puis:

* lancer `_updatePublisher` (lancer `_updatePublisher.bat` dans le bon dossier sur l’invite de commande). Attention ! Il ne peut pas y avoir d’espace dans le path du dossier, ce qui peut engendrer des erreurs, notamment avec OneDrive.
* lancer `_genonce` (lancer `_genonce.bat` dans le bon dossier sur l’invite de commande)

Si tout s’est bien passé, le dossier output est apparu, il suffit de lancer `index.html` pour visualiser l’IG généré.

Vous pouvez maintenant commencer à développer votre implementation guide ! :)

* Documentation vers FSH : https://build.fhir.org/ig/HL7/fhir-shorthand/reference.html
* Documentation sur l’IG Publisher : https://confluence.hl7.org/pages/viewpage.action?pageId=35718627#IGPublisherDocumentation-QuickStart

### MAC / Linux

#### Prérequis : NodeJS, Java, Ruby et Jekyll

##### NodeJS

Pour installer [NodeJS](https://nodejs.org/), vous pouvez suivre la documentation d’installation officielle.

Sur une distribution Linux basée sur Debian (Debian, Ubuntu…), vous pouvez installer NodeJS [directement depuis votre package-manager](https://nodejs.org/en/download/package-manager#debian-and-ubuntu-based-linux-distributions) :

```
sudo apt install nodejs

```

Il est aussi possible de l’installer via [`nvm`(Node Version Manager)](https://github.com/nvm-sh/nvm), qui vous permettra de changer de version de NodeJS en fonction des requis de vos projets.

##### Java

Pour installer Java, vous pouvez vous tourner vers le [JDK officiel sur la page d’Oracle](https://www.oracle.com/fr/java/technologies/downloads/). Vous y trouverez un `.deb` ou un `.rpm` à installer facilement sur votre distribution. Vous pouvez aussi utiliser [`openjdk`](https://openjdk.org/) pour une implémentation open-source de la plateforme Java.

```
sudo apt install openjdk-17-jre

```

##### Ruby et Jekyll

Pour installer Ruby sur une distribution Linux basée sur Debian, vous pouvez le faire via votre package-manager :

```
sudo apt-get install ruby-full

```

Pour le faire sur Mac :

```
brew install ruby

```

Que ce soit sous Linux ou Mac, vous pouvez ensuite installer Jekyll avec la commande suivante :

```
gem install bundler jekyll

```

Vous trouverez davantage d’informations sur le [confluence d’hl7](https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation).

Des difficultés pour installer ruby et jekyll peuvent survenir sur mac M1, M2 : lancer le [terminal avec rosetta](https://apple.stackexchange.com/questions/428768/on-apple-m1-with-rosetta-how-to-open-entire-terminal-iterm-in-x86-64-architec) et suivre [cette procédure](https://github.com/jekyll/jekyll/issues/8576#issuecomment-798080994) permet de régler les problèmes.

#### Installer SUSHI

Sushi permet de convertir la [grammaire FSH](https://build.fhir.org/ig/HL7/fhir-shorthand/) pour générer des profils, extensions (StructureDefinition) et des exemples / instances FHIR. La prise en main est relativement facile lorsque l’on connaît bien FHIR. Sushi est développé en JavaScript sous forme de module npm.

```
npm install -g fsh-sushi

```

Pour information, [GoFSH](https://github.com/FHIR/GoFSH) permet de faire la transformation inverse : transformer une StructureDefinition au format FSH.

#### Générer l’IG

```
bash _updatePublisher.sh # Mise à jour du publisher java
bash _genonce.sh # Génère l'IG

```

### Publication d’une nouvelle version d’un guide d’implémentation

Une fois le guide d’implémentation prêt, il est nécessaire de le publier pour que celui-ci soit versionné, historisé, et publier dans le FHIR Package Registry.

#### Au sein de l’ANS

Pour publier une nouvelle version (release) d’un guide d’implémentation, il est nécessaire de remplir à la racine du répertoire GitHub un fichier publication-request.json dont [la documentation peut être trouvée ici](https://confluence.hl7.org/spaces/FHIR/pages/144970227/IG+Publication+Request+Documentation). Ensuite, il suffit de lancer le workflow de release sur GitHub.

#### En dehors de l’ANS

Pour publier des guides d’implémentation en dehors de l’ANS, il est nécessaire de :

* 1/ [optionnel] Créer un template adapté à votre organisation ([exemple de celui de l’ANS](https://github.com/ansforge/IG-template))
* 2/ [requis la première fois] Créer un répertoire GitHub qui va porter le contenu des pages web à publier ([exemple de celui de l’ANS](https://github.com/ansforge/IG-website-release)). Celui-ci doit avoir la bonne arborescence de dossiers avec les submodules et le fichier publication-setup bien paramétré.
* 3/ [requis à chaque publication d’IG] Créer un fichier publication-request.json à la racine du repository du guide d’implémentation pour définir la release en suivant cette [documentation](https://confluence.hl7.org/spaces/FHIR/pages/144970227/IG+Publication+Request+Documentation).
* 4/ [requis à chaque publication d’IG] Lancer l’IG publisher avec l’option -go-publish ([Documentation](https://confluence.hl7.org/spaces/FHIR/pages/104580055/Process+for+Publishing+a+FHIR+Implementation+Guide+for+non-HL7+IGs))

Lancer le publisher avec l’option -go-publish permet de publier votre IG avec les bonnes redirections pour que celui-ci soit prêt à être publié sur un serveur web. Les URLs canoniques doivent mimer le lien où sera publié le site web.

* 5/ [requis à chaque publication d’IG] Publier le contenu du dossier www dans le répertoire GitHub IG-website-release sur un serveur web
* 6/ [requis la première fois] Faire une Pull Request dans [ce repository](https://github.com/FHIR/ig-registry) pour ajouter votre flux rss (dans le fichier package-feeds.json)

Pour rappel, les bonnes pratiques imposent de respecter les modélisations faites au niveau national : [FrCore](https://hl7.fr/ig/fhir/core) et [guides d’implémentation de l’ANS](https://interop.esante.gouv.fr/ig/fhir/)

Liens vers les documentations internationales :

* [documentation sur les templates et bonnes pratiques](https://build.fhir.org/ig/FHIR/ig-guidance/index.html)

