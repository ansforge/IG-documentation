
La GitHub Action [ansforge/IG-workflows](https://github.com/ansforge/IG-workflows) fournit un pipeline clé en main pour compiler, tester et publier un guide d'implémentation FHIR via GitHub Actions. Elle encapsule les outils du cycle de vie d'un IG : Sushi, IG Publisher, validator_cli, génération PlantUML et publication sur GitHub Pages ou sur le site de publication ANS.

### Mise en place du workflow de CI

Dans le répertoire `.github/workflows/` du dépôt de l'IG, créer un fichier `fhir-workflows.yml` :

```yaml
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
          github_page_token: {% raw %}${{ secrets.GITHUB_TOKEN }}{% endraw %}
```

L'IG compilé est publié sur la branche `gh-pages` du dépôt, sous une sous-arborescence portant le nom de la branche source. La preview est accessible à l'adresse :

```text
https://ansforge.github.io/{nom-du-repo}/{nom-de-la-branche}/ig
```

### Paramètres disponibles

| Paramètre | Type | Défaut | Description |
| --- | --- | --- | --- |
| `repo_ig` | string | — | **Requis.** Chemin vers le répertoire source de l'IG |
| `ig-publisher-version` | string | `latest` | Version de l'IG Publisher (`latest` ou `x.y.z`) |
| `github_page` | boolean | `false` | Active la publication sur GitHub Pages |
| `github_page_token` | string | — | Token GitHub pour écrire sur la branche `gh-pages` |
| `bake` | boolean | `false` | Installe FrCore et Annuaire depuis Simplifier (via Firely Terminal) |
| `validator_cli` | boolean | `false` | Lance les tests avec le validator_cli HL7 |
| `generate_plantuml` | boolean | `false` | Génère un diagramme de classes PlantUML depuis le `package.db` |
| `generate_mapping_plantuml` | boolean | `false` | Génère les diagrammes de mapping PlantUML |
| `generate_testscript` | boolean | `false` | Génère des TestScript depuis le package de l'IG |
| `publish_repo` | string | `""` | Dépôt de publication pour les releases (ex. `ansforge/IG-website-release`) |
| `publish_repo_token` | string | `""` | Token avec droits d'écriture sur `publish_repo` |
| `publish_path_outpout` | string | `""` | Chemin cible dans le dépôt de publication (ex. `./IG-website-release/www/ig`) |

### Activer les dépendances Simplifier (bake)

Le paramètre `bake: "true"` est nécessaire pour les IGs qui dépendent de **FrCore** (`hl7.fhir.fr.core`) ou de l'**Annuaire** (`ans.annuaire.fhir.r4`), qui ne sont pas disponibles sur le serveur de packages HL7 standard.

```yaml
- uses: ansforge/IG-workflows@main
  with:
    repo_ig: "./igSource"
    github_page: "true"
    github_page_token: {% raw %}${{ secrets.GITHUB_TOKEN }}{% endraw %}
    bake: "true"
```

### Publier une release

La publication d'une release nécessite un accès au dépôt [ansforge/IG-website-release](https://github.com/ansforge/IG-website-release), qui héberge le registre et l'historique des IGs publiés sur [interop.esante.gouv.fr](https://interop.esante.gouv.fr). Le token `ANS_IG_API_TOKEN` doit être configuré dans les secrets du dépôt.

Créer un fichier `.github/workflows/a_release.yml` déclenché manuellement :

```yaml
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
          github_page_token: {% raw %}${{ secrets.GITHUB_TOKEN }}{% endraw %}
          bake: "false"
          validator_cli: "false"
          publish_repo: "ansforge/IG-website-release"
          publish_repo_token: {% raw %}${{ secrets.ANS_IG_API_TOKEN }}{% endraw %}
          publish_path_outpout: "./IG-website-release/www/ig"
```

Ce workflow :

1. Compile l'IG avec le publisher en mode `go-publish`
2. Pousse le résultat dans `IG-website-release` et crée un commit de release
3. Crée une GitHub Release avec `full-ig.zip` et `package.tgz` en pièces jointes

Les informations de release (version, chemin canonique) sont lues depuis `publication-request.json` à la racine de l'IG.

### Nettoyer les branches obsolètes dans gh-pages

Au fil du temps, la branche `gh-pages` accumule des sous-répertoires correspondant à d'anciennes branches supprimées. Un workflow dédié permet de nettoyer automatiquement ces entrées :

```yaml
name: Suppression des anciennes branches dans gh-pages

on:
  workflow_dispatch:

jobs:
  cleanup:
    runs-on: ubuntu-latest
    steps:
      - name: Supprimer les branches obsolètes
        run: |
          branches=()
          for branch in $(git for-each-ref --format='%(refname)' refs/heads/); do
            branches+="${branch#"refs/heads/"}"
          done
          git checkout gh-pages
          for dossier in ig; do
            [[ ! " $branches " =~ " ${dossier%/} " ]] && rm -r "$dossier"
          done
```
