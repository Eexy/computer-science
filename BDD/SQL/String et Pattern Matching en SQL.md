Dans une BDD une string est une chaine de caractère ayant le [[Les types en BDD|type]] $CHAR$ qui définit une taille fixe ou le type $VARCHAR$  qui défini une string de taille variable.

De plus on considère que deux chaines sont égaux si et seulement si elles respectent les conditions suivantes :

- Elles ont la même taille
- Elles sont composées des même caractères
- Leur caractère sont au même endroit

Pour rechercher un tuple dont la string doit correspondre à une valeur on utilise simplement l'operateur `=`

**exemple** : On cherche que le film Iron Man

```sql
...reste du query
WHERE title = "Iron Man"
```

## Pattern Matching

Dans une BDD on peut utiliser le pattern matching. Cela permet ainsi de récupérer tous les tuples dont la chaine de charactère va obéir à un pattern au lieu d'être exactement la même.

On utilise le pattern matching avec l'operateur `LIKE`

**exemple** : On souhaite récupérer tous les films Star Wars ou Star Trek

```sql
WHERE title LIKE 'Star ____'
```

Dans cette exemple nos résultat va correspondre a tous les films de 9 caractère qui commencent par 'Star'.

On peut aller encore plus loin avec le pattern Matching en utilisant l'operateur `%` pour matcher un nombre de caractère inconnu

**exemple** : On cherche a récupérer tous les films Star Wars or on ne sait pas à l'avance la taille de chaque titre.

```sql
WHERE title LIKE "Star Wars : %"
```

Si on souhaite faire l'inverse et matcher tous les films qui ne sont pas des films Star Wars on peut utiliser l'operateur `NOT`

**exemple** : On recherche tous les films qui ne sont pas des films Star Wars

```sql
WHERE title NOT LIKE "Star Wars : %"
```

## REGEX

Enfin pour matcher une expression on aussi utiliser une REGEX avec l'operateur `REGEXP`

**exemple** : On cherche a récupérer tous les films commençant par la lettre 'S'
```sql
WHERE title REGEXP '^S'
```