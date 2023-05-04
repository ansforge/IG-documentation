### Windows

Prérequis:
- Avoir les droits administrateur

#### Etape 1. Installer VS CODE et les plugins 

https://code.visualstudio.com/

- [Requis] "FHIR Shorthand"
- [Optionnel] "Markdown Preview Enhanced"
- [Optionnel] "Kodjin FHIR Profiler"

1. Lancer vs code
2. Aller dans le menu extension (les 4 carrés dont un qui se décolle à gauche), chercher et installer "FHIR Shorthand"

#### Etape 2. Installer Node JS

https://nodejs.org/en/
La case "Automatically install the necessary tools" peut être cochée.

#### Etape 3. Installer SUSHI

1. Lancer l'invite de commande (windows > "invite de commande")
2. Ecrire et lancer la commande `npm install -g fsh-sushi`

#### Etape 4. Installer les dépendances de l'IG Publisher

- JAVA JDK: https://www.oracle.com/fr/java/technologies/downloads/#jdk19-windows (installer, au format .exe)
- Ruby: https://rubyinstaller.org/downloads (with devkit). Installer le "MSYS2 base installation".
- Jekyll et bundler: lancer l'invite de commande en mode administrateur et lancer la commande `gem install jekyll bundler`


#### Etape 5. Lancer l'IG Publisher

Télécharger le repository [ansforge/FIG_ans-ig-sample](https://github.com/ansforge/FIG_ans-ig-sample) : code > download zip.
Décompresser le dossier, et le mettre dans un chemin où il n'y a pas d'espace (exemple : C:\Users\nriss\Documents).

Puis:
- lancer _updatePublisher (lancer _updatePublisher.bat dans le bon dossier sur l'invite de commande)

Attention! Il ne peut pas y avoir d'espace dans le path du dossier, ce qui peut engendrer des erreurs, notamment avec onedrive.


- lancer _genonce (lancer _genonce.bat dans le bon dossier sur l'invite de commande)

Si tout s'est bien passé, le dossier output est apparu, il suffit de lancer index.html pour démarrer l'IG généré


Vous pouvez maintenant commencer à développer votre implementation guide ! :)
- Documentation vers FSH : https://build.fhir.org/ig/HL7/fhir-shorthand/reference.html
- Documentation sur l'IG Publisher : https://confluence.hl7.org/pages/viewpage.action?pageId=35718627#IGPublisherDocumentation-QuickStart


### MAC / Linux


#### Prérequis : sushi, java, ruby et jekyll

Sushi permet de convertir la [grammaire FSH](https://build.fhir.org/ig/HL7/fhir-shorthand/) pour générer des profils, extensions (StructureDefinition) et des exemples / instances FHIR. La prise en main est relativement facile lorsque l'on connaît bien FHIR.
Sushi est développé en javascript sous forme de module npm. 

```
npm install -g fsh-sushi
```
Pour information, [GoFSH](https://github.com/FHIR/GoFSH) permet de faire la transformation inverse : transformer une StructureDefinition au format FSH.

Une fois ses outils installés, il faut installer les dépendances de l'IG publisher :
Installation de [java](https://www.java.com/fr/download/help/download_options.html), [ruby](https://www.ruby-lang.org/fr/documentation/installation/) et [jekyll](https://jekyllrb.com/docs/installation/).
Sur Linux :
```
sudo apt-get install ruby-full
gem install bundler jekyll
```

Sur Mac :
```
brew install ruby
gem install bundler jekyll
```
Vous trouverez davantage d'informations sur le [confluence d'hl7](https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation)

Des difficultés pour installer ruby et jekyll peuvent survenir sur mac M1, M2: lancer le [terminal avec rosetta](https://apple.stackexchange.com/questions/428768/on-apple-m1-with-rosetta-how-to-open-entire-terminal-iterm-in-x86-64-architec) et suivre [cette procédure](https://github.com/jekyll/jekyll/issues/8576#issuecomment-798080994) permet de régler les problèmes.

#### Générer l'IG
```
bash _updatePublisher.sh // Mise à jour du publisher java
bash _genonce.sh // Génère l'IG
```
