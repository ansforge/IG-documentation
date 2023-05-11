Il est important de noter qu'une spécification est en perpétuelle évolution. Au même titre qu'une application qui est déployée au grand public, des erreurs peuvent être découvertes ou des suggestions d'amélioration peuvent être proposées. Il est important que les implémentations ne soient pas un frein à l'avancée de l'interopérabilité et de la maturité des spécifications.

C'est la raison pour laquelle, lors du développement d'une spécification, il faut prévoir:

* D'aligner une spécification sur une version donnée de l'IG --> Toujours baser une implémentation sur un package fhir avec une version spécifique et publiée dans le fhir package registry
* Anticiper les futures évolutions de l'API (Pour cela, une des possibilité est de faire un mapping entre un modèle logique et une API FHIR). Les évolutions sont moins painful si elles sont anticipées.

Les ressources exposées ou acceptées en lecture doivent être conformes aux profils proposés dans la spécification, téléchargeable dans le package.

Des serveurs FHIR open source tel que HAPI permettent de développer simplement une API FHIR supportant déjà la plupart des fonctionnalités attendues.