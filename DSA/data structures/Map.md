Une map est une structure qui ressemble fortement à une [[Hash table]]. En effet comme une hash table on va associer une clé à une valeur.
La seul différence c'est qu'on ne va pas générer une clé par une [[Hash function]]. 
Dans le cas d'un map on lui fourni directement la clé que l'on souhaite utilisé pour sauvegarder notre donnée.

Une map doit supporter les opérations suivante :

- insert($k,v$) : $k$ est la clé que l'on souhaite définir et $v$ la valeur
- delete($k$) : On supprime l'élément qui a la clé $k$
- get($k$) : On récupère l'élément qui à la clé $k$