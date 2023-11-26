Il est possible de trier le résultat d'un query en utilisant la clause `ORDER BY`. Grâce à cette clause on va pouvoir modifier et trier le résultat d'un query en fonction des propriétés de nos tuples

**exemple** : On souhaite trier les films en fonction de leur longueur

```sql
ORDER BY length
```

De plus on va pouvoir utiliser plusieurs propriété pour le trie en les mettant les une à la suite des autres

**exemple** : On souhaite trier les films en fonction de leur longueur et les faire apparaitre dans l'ordre alphabétique

```sql
ORDER BY length, title
```

Par défaut le trie se fait de manière croissante mais il est possible de changer le comportement en utilisant `DESC` et `ASC`. 

- `DESC` permet d'effectuer le trie de manière décroissante
- `ASC` permet d'effectuer le trie de manière croissante (comportement par défaut)

La clause `ORDER BY` peut aussi prendre une expression. Ainsi on peut par exemple additionner les champs