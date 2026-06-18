# Publier un IG externe - Documentation des guides d'implémentation de l'ANS v0.1.10

* [**Table of Contents**](toc.md)
* [**Quick start IG**](mod_nouvel_ig.md)
* **Publier un IG externe**

## Publier un IG externe

La GitHub Action [ansforge/IG-workflows](https://github.com/ansforge/IG-workflows) fournit un pipeline clé en main pour compiler, tester et publier un guide d’implémentation FHIR via GitHub Actions. Elle encapsule les outils du cycle de vie d’un IG : Sushi, IG Publisher, validator_cli, génération PlantUML et publication sur GitHub Pages ou sur le site de publication ANS.

### Dépôts de référence ANS

Trois dépôts forment l’outillage de base pour créer et publier un IG dans l’écosystème ANS :

* [ansforge/IG-modele](https://github.com/ansforge/IG-modele) — dépôt de démarrage à forker pour créer un nouvel IG. Il fournit la structure de répertoires, un `sushi-config.yaml` vierge, et les workflows GitHub Actions préconfigurés.
* [ansforge/IG-template](https://github.com/ansforge/IG-template) — charte graphique ANS appliquée lors de la compilation par l’IG Publisher (basée sur [HL7/ig-template-base](https://github.com/HL7/ig-template-base)). Référencé dans `ig.ini` via `template`. Ne pas modifier directement ; utiliser comme point de départ pour une charte personnalisée.
* [ansforge/IG-workflows](https://github.com/ansforge/IG-workflows) — GitHub Action réutilisable qui orchestre le pipeline de build et de publication (Sushi, IG Publisher, validator_cli, GitHub Pages, release). Détaillée dans les sections suivantes.

Pour une organisation externe souhaitant mettre en place la même infrastructure, voici ce qui doit être forké ou adapté :

| | |
| :--- | :--- |
| [ansforge/IG-modele](https://github.com/ansforge/IG-modele) | Point de départ pour chaque nouvel IG. Adapter le`sushi-config.yaml`, le`README`et les workflows selon vos besoins. |
| [ansforge/IG-template](https://github.com/ansforge/IG-template) | Remplacer le logo et les couleurs ANS par la charte de votre organisation. Mettre à jour la référence`template`dans`ig.ini`. |
| [ansforge/IG-website-release](https://github.com/ansforge/IG-website-release) | Adapter`publish.ini`(URL de votre site), les fichiers`templates/`(logo, navigation), et initialiser les sous-modules. Voir la section[Créer son propre dépôt de publication](#créer-son-propre-dépôt-de-publication). |

`IG-workflows` en revanche n’a pas besoin d’être forké : la GitHub Action est utilisable telle quelle depuis `ansforge/IG-workflows@main`.

### Mise en place du workflow de CI

Dans le répertoire `.github/workflows/` du dépôt de l’IG, créer un fichier `fhir-workflows.yml` :

```
name: Build et publication GitHub Pages

on:
  push:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          path: igSource

      - uses: ansforge/IG-workflows@main
        with:
          repo_ig: "./igSource"
          github_page: "true"
          github_page_token: ${{ secrets.GITHUB_TOKEN }}

```

L’IG compilé est publié sur la branche `gh-pages` du dépôt, sous une sous-arborescence portant le nom de la branche source. La preview est accessible à l’adresse :

```
https://{organisation}.github.io/{nom-du-repo}/{nom-de-la-branche}/ig

```

### Paramètres disponibles

| | | | |
| :--- | :--- | :--- | :--- |
| `repo_ig` | string | — | **Requis.**Chemin vers le répertoire source de l’IG |
| `ig-publisher-version` | string | `latest` | Version de l’IG Publisher (`latest`ou`x.y.z`) |
| `github_page` | boolean | `false` | Active la publication sur GitHub Pages |
| `github_page_token` | string | — | Token GitHub pour écrire sur la branche`gh-pages` |
| `bake` | boolean | `false` | Installe FrCore et Annuaire depuis Simplifier (via Firely Terminal) |
| `validator_cli` | boolean | `false` | Lance les tests avec le validator_cli HL7 |
| `generate_plantuml` | boolean | `false` | Génère un diagramme de classes PlantUML depuis le`package.db` |
| `generate_mapping_plantuml` | boolean | `false` | Génère les diagrammes de mapping PlantUML |
| `generate_testscript` | boolean | `false` | Génère des TestScript depuis le package de l’IG |
| `publish_repo` | string | `""` | Dépôt de publication pour les releases (ex.`ansforge/IG-website-release`) |
| `publish_repo_token` | string | `""` | Token avec droits d’écriture sur`publish_repo` |
| `publish_path_outpout` | string | `""` | Chemin cible dans le dépôt de publication (ex.`./IG-website-release/www/ig`) |

### Publier une release

La publication d’une release nécessite un accès au dépôt [ansforge/IG-website-release](https://github.com/ansforge/IG-website-release), qui héberge le registre et l’historique des IGs publiés sur [interop.esante.gouv.fr](https://interop.esante.gouv.fr). Le token `ANS_IG_API_TOKEN` doit être configuré dans les secrets du dépôt.

Créer un fichier `.github/workflows/a_release.yml` déclenché manuellement :

```
name: Publication release

on:
  workflow_dispatch:

jobs:
  run-release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          path: igSource

      - uses: ansforge/IG-workflows@main
        with:
          repo_ig: "./igSource"
          github_page: "true"
          github_page_token: ${{ secrets.GITHUB_TOKEN }}
          bake: "false"
          validator_cli: "false"
          publish_repo: "ansforge/IG-website-release"
          publish_repo_token: ${{ secrets.ANS_IG_API_TOKEN }}
          publish_path_outpout: "./IG-website-release/www/ig"

```

Ce workflow :

1. Compile l’IG avec le publisher en mode`go-publish`
1. Pousse le résultat dans`IG-website-release`et crée un commit de release
1. Crée une GitHub Release avec`full-ig.zip`et`package.tgz`en pièces jointes

Les informations de release (version, chemin canonique) sont lues depuis `publication-request.json` à la racine de l’IG.

### Créer son propre dépôt de publication

Pour publier un IG en dehors de l’infrastructure ANS, il faut créer un dépôt de publication analogue à `IG-website-release`. Le publisher IG utilise ce dépôt pour générer les pages versionnées et mettre à jour le registre.

#### Structure du dépôt

```
mon-ig-website/
├── ig-registry/                  # sous-module git → FHIR/ig-registry
├── fhir-ig-history-template/     # sous-module git → HL7/fhir-ig-history-template
├── templates/
│   ├── header.template
│   ├── preamble.template
│   └── postamble.template
├── www/
│   └── ig/                       # répertoire cible des IGs publiés
└── publish.ini

```

Initialiser le dépôt avec les sous-modules :

```
git init mon-ig-website && cd mon-ig-website
git submodule add https://github.com/FHIR/ig-registry ig-registry
git submodule add https://github.com/HL7/fhir-ig-history-template fhir-ig-history-template
mkdir -p www/ig templates

```

#### Configurer publish.ini

`publish.ini` définit l’URL racine du site de publication. Cette URL doit correspondre au champ `path` déclaré dans le `publication-request.json` de chaque IG publié.

```
[website]
style=fhir.layout
server=apache
url=https://{organisation}.github.io/{nom-du-repo-website}/ig
org=Mon organisation

[feeds]
package=www/package-feed.xml
publication=www/publication-feed.xml

```

#### Créer les templates

Les trois fichiers de `templates/` contrôlent l’entête HTML, le pied de page et le bandeau de navigation du site de publication. Copier les fichiers depuis [ansforge/IG-website-release/templates](https://github.com/ansforge/IG-website-release/tree/main/templates) comme point de départ, puis adapter le logo et les liens de l’ANS à votre organisation.

#### Déclarer l’IG dans le registre

Ajouter une entrée dans `ig-registry/fhir-ig-list.json` pour chaque IG à publier :

```
{
  "package-id": "mon.org.mon-ig",
  "title": "Mon Guide d'Implémentation",
  "canonical": "https://{organisation}.github.io/{nom-du-repo-website}/ig/mon-ig",
  "introduction": "Description courte de l'IG.",
  "category": "...",
  "language": "fr",
  "editions": []
}

```

La valeur `canonical` doit correspondre exactement au champ `canonical` du `sushi-config.yaml` de l’IG.

#### Adapter le workflow de release

Modifier le workflow de publication pour pointer vers votre propre dépôt et chemin :

```
- uses: ansforge/IG-workflows@main
  with:
    repo_ig: "./igSource"
    github_page: "true"
    github_page_token: ${{ secrets.GITHUB_TOKEN }}
    publish_repo: "{organisation}/mon-ig-website"
    publish_repo_token: ${{ secrets.MON_TOKEN }}
    publish_path_outpout: "./mon-ig-website/www/ig"

```

Le token `MON_TOKEN` doit avoir les droits `contents: write` sur le dépôt de publication. Le configurer dans **Settings → Secrets and variables → Actions** du dépôt de l’IG.

