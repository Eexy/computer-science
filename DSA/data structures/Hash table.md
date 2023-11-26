
Une **hash table** (aussi appelé **hash map**) est une structure très efficace pour stocker des données et les récupérer rapidement.

En effet un hash table est une structure qui implémente un [[Dictionary]] où l'on va associé une clé à un élément

Dans une hash table cette clé va être généré par une [[Hash function|fonction de hashage]]. 


## Implémentations

Il existe deux moyens d'implémenter une hash table :

- **Chaining**
- **Open addressing**

C'est deux méthodes existe car ce sont les deux moyens utiliser pour gérer les collisions. En effet les collision arrive lorsque deux éléments se retrouve avec la même clé. Cela arrivera forcement plus on aura d'éléments sauvegarder peu importe à quel point notre [[Hash function|fonction de hashage]] est bonne

### Chaining

Cette méthode se base sur des [[Linked List]] et des [[Array]]. C'est la méthode la plus simple à utiliser et à implémenter. 
Pour cela on va avoir un tableau de liste et la clé de chaque élément va définir dans qu'elle liste du tableau ont va ajouter l'élément. 
Dans ce cas ci si deux éléments possède la même clé alors le deuxième élément sera ajouté a la fin de la liste.

Le principale avantage de cette technique c'est que vu qu'on utilise des [[Linked List]] on peut ajouter autant d'élément que l'on souhaite. De plus comme dit précédemment c'est simple d'implémenter cette méthode

![[chaining.png]]
**astuce** : Si on utilise cette méthode alors il est plus intéressant d'utiliser une [[Doubly Linked List]]

### Open addressing

L'open addressing se base aussi sur un [[Array]]. La différence avec méthode précédente c'est qu'il n'y aura pas de second structure utilisé dans le cas de collision. 
En effet si on se retrouve avec un élément qui à la même clé alors on va venir lui donner la prochaine place disponible du tableau.

Le principale avantage d'utiliser cette technique c'est qu'on économise de la mémoire. En effet notre hash table ne grandira pas plus que la mémoire qu'on lui a allouer au début. Ce qui en fait aussi son principale désavantage

![[open addressing.png]]

