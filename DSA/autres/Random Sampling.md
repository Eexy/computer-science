## Principe

La méthode Monte Carlo (**Random sampling**) est une méthode pour trouver une solution parmi un ensemble de solution à un problème plutôt simple.

En effet on va créer des solutions au hasard et on va les évaluer. Une fois qu'on à trouver une solutions assez bonne ou qu'on à assez attendu on s'arête et on renvoi la dernière solution trouvé.

Pour que cette méthode fonctionne il est capital qu'on puisse choisir une solution depuis l'ensemble des solutions de manière uniforme

Cette méthode est principalement utilisé dans les cas suivants :

- Quand il existe une haute proportion de solutions acceptable
- Quand il n'existe pas de cohérence dans notre ensemble de solutions. C'est à dire quand la notion de se rapprocher de la meilleur solution n'existe pas.

**exemple** : On chercher parmi notre groupe d'amis celui dont le numéro de sécurité social se termine par $00$.

Dans cet exemple la meilleur méthode est de choisir un ami au hasard et de lui demander et ainsi de suite car le numéro de sécurité social d'une personne ne va pas indiquer si le prochain sera plus proche ou non de la solution souhaité, il n'y a pas de cohérence.