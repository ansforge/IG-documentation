# Publier un IG externe - Documentation des guides d'implémentation de l'ANS v0.1.11

* [**Table of Contents**](toc.md)
* [**Quick start IG**](mod_nouvel_ig.md)
* **Publier un IG externe**

## Publier un IG externe

**Avant de publier un IG**

La publication d'un IG nécessite de respecter les
[bonnes pratiques de modélisation](mod_bonnes_pratiques.md). En particulier, tout IG destiné à l'écosystème français doit hériter des profils nationaux existants (FrCore, Annuaire…) plutôt que de remodéliser des concepts déjà standardisés. Publier un IG qui ignore les profils nationaux nuit à l'interopérabilité de l'ensemble de l'écosystème.

La GitHub Action [ansforge/IG-workflows](https://github.com/ansforge/IG-workflows) fournit un pipeline clé en main pour compiler, tester et publier un guide d’implémentation FHIR via GitHub Actions. Elle encapsule les outils du cycle de vie d’un IG : Sushi, IG Publisher, validator_cli, génération PlantUML et publication sur GitHub Pages ou sur un site de publication dédié.

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

S’assurer que le dépôt de l’IG contient bien `.github/workflows/fhir-workflows.yml` (présent par défaut dans un fork de `IG-modele`). Ce workflow déclenche le build sur chaque push et publie l’IG sur la branche `gh-pages`.

L’IG compilé est publié sur la branche `gh-pages` du dépôt, sous une sous-arborescence portant le nom de la branche source. La preview est accessible à l’adresse :

```
https://{organisation}.github.io/{nom-du-repo}/{nom-de-la-branche}/ig

```

### Paramètres disponibles

La liste complète et à jour des paramètres est maintenue dans le [README de ansforge/IG-workflows](https://github.com/ansforge/IG-workflows#inputs).

### Créer son propre dépôt de publication

Pour publier des releases versionnées, il faut d’abord créer un dépôt de publication analogue à `IG-website-release`. Le publisher IG utilise ce dépôt pour générer les pages versionnées et mettre à jour le registre.

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

### Publier une release

S’assurer que le dépôt de l’IG contient bien `.github/workflows/fhir-release.yml` (présent par défaut dans un fork de `IG-modele`), puis adapter les trois paramètres suivants pour pointer vers votre propre dépôt de publication :

```
          publish_repo: "{organisation}/mon-ig-website"
          publish_repo_token: ${{ secrets.MON_TOKEN }}
          publish_path_outpout: "./mon-ig-website/www/ig"

```

Ce workflow :

1. Compile l’IG avec le publisher en mode`go-publish`
1. Pousse le résultat dans le dépôt de publication et crée un commit de release
1. Crée une GitHub Release avec`full-ig.zip`et`package.tgz`en pièces jointes

Les informations de release (version, chemin canonique) sont lues depuis `publication-request.json` à la racine de l’IG.

