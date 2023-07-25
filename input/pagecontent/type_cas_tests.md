Différents niveaux de tests sont proposés sur l’espace de test de l’ANS afin d’aider les éditeurs dans leur préparation aux évènements de type projectathon.

Le niveau le plus bas permettra aux éditeurs de tester la conformité des messages unitaires qu’ils produisent. Le niveau intermédiaire permettra aux éditeurs de tester face à un autre système la conformité et l’interopérabilité des messages unitaires. Le niveau le plus élevé correspond aux scénarios proposés jusqu’à maintenant dans le cadre des projectathons et permettra aux éditeurs de tester des scénarios complexes face à un autre système.

### Niveau 1

Les tests de niveau 1 représentent les tests unitaires sans partenaire.
Chaque cas de test de niveau 1 correspond à un flux de la spécification technique.
L’objectif de ces cas de tests est de valider la ressource ou la requête produite par le système avec un validateur EVSClient indiqué dans le cas de test.
Les cas de test de niveau 1 sont notés N1 sous Gazelle.

### Niveau 2

Les tests de niveau 2 représentent les tests unitaires avec partenaire.
Pour être exécutés, il faut qu’au préalable les cas de test de niveau 1 indiqués en prérequis aient été exécutés par les 2 mêmes systèmes.
L’objectif de ces cas de test est de valider la ressource ou la requête construite ainsi que la capacité des systèmes à créer / intégrer ou requêter / envoyer des ressources.
Les cas de test de niveau 2 sont notés N2 sous Gazelle.

### Niveau 3

Les tests de niveau 3 représentent les tests avec partenaire basés sur l’enchaînement de différents tests unitaires avec partenaire (N2) en suivant un scénario complexe. Pour être exécutés, il faut qu’au préalable les cas de test de niveaux 1 et 2 indiqués en prérequis aient été exécutés entre les 2 mêmes systèmes.

L’objectif de ces cas de test est de créer un scénario complexe faisant appel aux différents flux de la spécification technique et ainsi créer un exemple d’usage.
Les cas de test de niveaux 3 sont notés N3 sous Gazelle.

Le proxy devra être utilisé pour les cas de tests de niveaux N2 et N3.
