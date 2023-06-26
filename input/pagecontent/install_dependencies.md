### Windows

Prérequis :

- Avoir les droits administrateur

#### Etape 1. Installer VS CODE et les plugins

https://code.visualstudio.com/

- [Requis] "[FHIR Shorthand](https://marketplace.visualstudio.com/items?itemName=MITRE-Health.vscode-language-fsh)"
- [Optionnel] "[Markdown Preview Enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)"
- [Optionnel] "[Kodjin FHIR Profiler](https://marketplace.visualstudio.com/items?itemName=edenlabio.fhir-profiler-tool)"
- [Optionnel] "[codfsh](https://github.com/gematik/codfsh)"

1. Lancer VS Code
2. Aller dans le menu extension (les 4 carrés dont un qui se décolle à gauche), chercher et installer "FHIR Shorthand"

#### Etape 2. Installer NodeJS

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

- lancer `_updatePublisher` (lancer `_updatePublisher.bat` dans le bon dossier sur l'invite de commande)

Attention ! Il ne peut pas y avoir d'espace dans le path du dossier, ce qui peut engendrer des erreurs, notamment avec OneDrive.

- lancer `_genonce` (lancer `_genonce.bat` dans le bon dossier sur l'invite de commande)

Si tout s'est bien passé, le dossier output est apparu, il suffit de lancer `index.html` pour démarrer l'IG généré.

Vous pouvez maintenant commencer à développer votre implementation guide ! :)

- Documentation vers FSH : https://build.fhir.org/ig/HL7/fhir-shorthand/reference.html
- Documentation sur l'IG Publisher : https://confluence.hl7.org/pages/viewpage.action?pageId=35718627#IGPublisherDocumentation-QuickStart

### MAC / Linux

#### Prérequis : NodeJS, Java, Ruby et Jekyll

##### NodeJS

Pour installer [NodeJS](https://nodejs.org/), vous pouvez suivre la documentation d'installation officielle.

Sur une distribution Linux basée sur Debian (Debian, Ubuntu...), vous pouvez installer NodeJS [directement depuis votre package-manager](https://nodejs.org/en/download/package-manager#debian-and-ubuntu-based-linux-distributions) :

```bash
sudo apt install nodejs
```

Il est aussi possible de l'installer via [`nvm` (Node Version Manager)](https://github.com/nvm-sh/nvm), qui vous permettra de changer de version de NodeJS en fonction des requis de vos projets.

##### Java

Pour installer Java, vous pouvez vous tourner vers le [JDK officiel sur la page d'Oracle](https://www.oracle.com/fr/java/technologies/downloads/). Vous y trouverez un `.deb` ou un `.rpm` à installer facilement sur votre distrubtion.
Vous pouvez aussi utiliser [`openjdk`](https://openjdk.org/) pour une implémentation open-source de la plateforme Java.

```bash
sudo apt install openjdk-17-jre
```

##### Ruby et Jekyll

Pour installer Ruby sur une distribution Linux basée sur Debian, vous pouvez le faire via votre package-manager :

```bash
sudo apt-get install ruby-full
```

Pour le faire sur Mac :

```bash
brew install ruby
```

Que ce soit sous Linux ou Mac, vous pouvez ensuite installer Jekyll avec la commande suivante : 

```bash
gem install bundler jekyll
```

Vous trouverez davantage d'informations sur le [confluence d'hl7](https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation).

Des difficultés pour installer ruby et jekyll peuvent survenir sur mac M1, M2 : lancer le [terminal avec rosetta](https://apple.stackexchange.com/questions/428768/on-apple-m1-with-rosetta-how-to-open-entire-terminal-iterm-in-x86-64-architec) et suivre [cette procédure](https://github.com/jekyll/jekyll/issues/8576#issuecomment-798080994) permet de régler les problèmes.

#### Installer SUSHI

Sushi permet de convertir la [grammaire FSH](https://build.fhir.org/ig/HL7/fhir-shorthand/) pour générer des profils, extensions (StructureDefinition) et des exemples / instances FHIR. La prise en main est relativement facile lorsque l'on connaît bien FHIR.
Sushi est développé en JavaScript sous forme de module npm.

```bash
npm install -g fsh-sushi
```

Pour information, [GoFSH](https://github.com/FHIR/GoFSH) permet de faire la transformation inverse : transformer une StructureDefinition au format FSH.

#### Générer l'IG

```bash
bash _updatePublisher.sh # Mise à jour du publisher java
bash _genonce.sh # Génère l'IG
```
