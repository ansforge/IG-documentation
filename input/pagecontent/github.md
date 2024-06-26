GitHub est une sorte de sharepoint, un repository versionné avec un système de branche pour travailler de manière collaborative sur du contenu textuel (code, écriture, grammaire ...)

Les branches:
Un repository (ou répertoire) Github contient une arborescence de branche, permettant d'individualiser le travail de chacun puis de pousser son travail dans la branche de travail commune : typiquement `main`.

### Reporter un problème (une issue)

Vous avez identifié une erreur sur un des guides ? L'onglet issue permet de signaler un problème sur un projet donné.

<div class="figure" style="width:100%;">
    <img style="height: auto; width: 100%;" alt="image" src="https://user-images.githubusercontent.com/48218773/215773144-31a47623-a853-4a4e-8ba0-ad1d66b29961.png">
</div>

Un lien est également disponible sous chaque guide d'implémentation pour accéder aux issues :
<div class="figure" style="width:100%;">
    <img style="height: auto; width: 100%;" alt="image" src="new_issue.png">
</div>

L'issue doit contenir un titre, et une description très détaillée avec une proposition de changement.

### Travailler sur un repository

GitHub peut s'utiliser de deux façons :  

- Via l'application GitHub Desktop
- Via l'invite de commande

#### Git clone xxx

La commande git clone permet de copier l'intégralité d'un repository en local.
Le xxx est à remplacer avec l'indication dans ssh :
<div class="figure">
    <img style="height: auto; width: 50%;" alt="image" src="https://user-images.githubusercontent.com/48218773/207010144-e80b05a0-9763-4026-bf59-debd8b2a2411.png">
</div>

#### Git checkout -b nom_travail_en_cours

Pour éviter que tout le monde travaille sur le même environnement, il faut créer une branche, et l'appeler par le nom du travail prévu dans cette branche .
A ce moment là, vous pouvez faire les modifications en local, ces modifications seront reportées sur github pour tout le monde à l'issue des prochaines étapes

#### Git add fichiers_à_ajouter

Une fois les modifications établies, il faut dire à Git quels fichiers on souhaite ajouter au répertoire distant en faisant git add et en rajoutant le chemin vers les fichiers à ajouter (la commande `git status` permet de voir quels fichiers ont été modifiés)

#### Git commit -m "message sur la nature des travaux effectués"

Une fois les travaux menés (tout ou partie), il faut faire des commit : c'est à dire valider une modification fonctionnelle, cohérente. Cette étape peut être répétée plusieurs fois.

#### Git push

Cette commande pousse l'ensemble des modifications validées avec des commit sur le GitHub global.

#### Faire une Pull Request (PR)

Ensuite, il faut aller sur l'interface graphique, dans l'onglet, "Pull Requests", et créer une nouvelle PR qui permet de dire : je veux intégrer les modifications que j'ai faites sur la branche x à la branche main.
Chaque PR doit être validée par quelqu'un d'autre pour : 

- Etre sûr que le savoir n'est pas concentré sur une personne
- Permettre une relecture pour éviter les erreurs

### Mettre en place un workflow de validation/génération/publication

Afin de faciliter les actions au regards des IG, l'ANS  met à disposition un [GitHub Action](https://github.com/ansforge/IG-workflows)  avec les fonctionnalités suivantes : 
- Lancement de sushi
- Tests avec le validateur_cli
- Incorporation des projets de simplifier (Methode bake)
- Publication des releases sur un repo github
- Génération du diagramme plantuml à partir de des données de l'IG
- Génération des diagrammes de mapping plantuml
- Génération des testscripts avec le projet testscript-generator
- Publication sur les pages github :
  - Diagramme de class plantuml généré à partir des données de l'IG
  - Rapport de validation du validator_cli

