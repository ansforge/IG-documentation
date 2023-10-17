Il est important de noter qu'une spécification est en perpétuelle évolution. Au même titre qu'une application qui est déployée au grand public, des bugs peuvent être découverts, ou des suggestions d'amélioration peuvent être proposées. Or, les implémentations ne doivent pas être un frein à l'avancée de l'interopérabilité et de la maturité des spécifications.

C'est la raison pour laquelle, lors du développement d'une spécification, il faut :
* **Toujours** baser une implémentation sur une version spécifique d'un IG et donc d'un package FHIR, qui a été publié dans le [fhir package registry](https://registry.fhir.org). Cela permet de faciliter la traçabilité et d'indiquer la conformité.
* Anticiper les futures évolutions de l'API pour les rendre moins douloureuses. Pour cela, une des possibilité est de faire un mapping entre un modèle logique et une API FHIR. Un décalage entre les publications d'une spécification et une implémentation est possible, mais il est toujours préférable de le minimiser.

Les ressources exposées ou acceptées en lecture doivent être conformes aux profils proposés dans la spécification, téléchargeable dans le package.

Des serveurs FHIR open source (ex: [HAPI](https://hapifhir.io)) permettent de développer simplement une API FHIR supportant déjà la plupart des fonctionnalités (SearchParameter, Operation ...).
