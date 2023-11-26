Les index sont un moyen d'optimiser les performances de la BDD en sauvegardant l'emplacement des tuples qui répondent à une certaines condition sur l'un de leur attributs.
Ainsi en faisant cela lorsque l'on cherchera à les récupérer au lieu de devoir regarder chaque tuples et sélectionner les bon la BDD aura juste à les récupérer avec leur emplacement

L'implémentation d'un Index se fait avec un [[B-Tree]]
## Creer un index

Pour créer un index on utilise la commande

```sql
CREATE INDEX indexName ON Relation(...attribut)
```

**exemple** : On souhaite créer un index afin de récupérer d'améliorer les performances de notre BDD lorsque l'on utilise un query qui va venir récupérer le nom d'un film

```sql
CREATE INDEX MovieTitle ON Movies(title)
```

## Supprimer un Index

Pour supprimer un index on utilise la commande

```sql
DROP INDEX IndexName
```

## Performance

Les index servent à retrouver les tuples beaucoup plus facilement et donc plus rapidement mais cela à aussi un coût. En effet si on viens inserer/supprimer/modifier un tuple de l'index alors c'est tous l'index qui doit être mis à jour il est donc important de bien choisir notre index
De plus si notre index doit chargé énormément de données qui se trouve à plusieurs endroit alors il va perdre énormément de performance.

Voici quelque cas où il est intéressant de créer un index

### Index utiles

Le plus utile des index que l'on peut mettre sur une relation c'est un index sur sa clé cela est dû à deux raison. (Une clé est une valeur qui va permettre d'identifier un tuple)

1. Les query sur une clé spécifique sont courant donc ils vont être énormément utilisé
2. Vu qu'il existe qu'une seule paire $(clé \space value)$ l'index va alors soit rien retourné soit un seule tuple donc ça va être rapide  

Dans le cas où notre index n'est pas sur une clé cela est peut quand même être utiles dans les cas suivant

1. Si l'attribut est presqu'une clé : Dans le cas où il y à relativement peu de tuple partageant la même valeur alors la BDD devrait pouvoir vite les chargé
2. Si il existe un cluster pour cette attribut (tous les tuples qui ont la même valeur sont stocké au même endroit)
