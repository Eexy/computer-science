## Principe

La recherche locale (**local search**) est une méthode pour trouver une solutions dans un ensemble de solutions possible en cherchant les voisins de la solution actuelle

**exemple** : Imaginons que l'on souhaite trouver un plombier on pourrai utiliser la méthode [[Random Sampling]] et composer un numéro au hasard. 

Si la personne est un plombier alors on s'arête sinon on recommence mais cela pourrai prendre du temps.

Le mieux serai de demander à la personne qu'on à au téléphone si elle ne connait pas quelqu'un qui pourrai connaitre un plombier. On appellerai la personne donnée et on lui poserai la même question etc...

On utilise cette méthode dans les cas suivant :

- Quand il y a une grande cohérence dans l'ensemble des solution
- Quand le coup incrémental d'évaluer les différentes solution est beaucoup plus bas que l'évaluation global des solutions

**exemple** : On cherche à arriver au sommet d'une montagne en partant d'un point au hasard.

En appliquant le local search on regarderai les voisin de notre point qui ont une hauteur supérieur au notre on transite alors vers ce point et on recommence en permanence jusqu'à temps que les voisins de notre solution nous font régresser

