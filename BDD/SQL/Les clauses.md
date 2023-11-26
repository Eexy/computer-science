### SELECT

La clause `SELECT` permet de définir quels sont les attributs que l'on souhaite garder dans les résultats

L'operateur `*` indique que l'on souhaite récupérer tous les attributs

**exemple** : Imaginons que l'on souhaite récupéré que le nom des films

```sql
SELECT title
FROM Movies
```

De plus lorsque l'on récupère les champs on va pour faire une opération la dessus comme par exemple les renommer avec l'operateur `AS`

**exemple** : On cherche à a récupérer le champ `title` en tant que nom

```sql
SELECT title As name
FROM Movies
```

Il est important de prendre en compte que les opérations effectuer ne vont pas venir modifier la base de donnée mais seulement notre résultat

**exemple** : On souhaite afficher la durée du film en heures

```sql
SELECT titla AS name, length*0.016667 AS lengthInHours
FROM Movies
```

### FROM

La clause `FROM` permet de définir [[Les tables]] que l'on souhaite utilisé pour notre recherche. Dans l'exemple donné on précise que l'on fait notre recherche sur la table $Movies$

Dans une recherche on peut travailler avec plusieurs tables. Si c'est le cas alors on les mettrais à la suite

**exemple** : On récupère les données de plusieurs tables

```sql
SELECT *
FROM Movies`, Actors...
```

### WHERE

La clause `WHERE` va permettre d'indiquer les conditions que nos tuples vont devoir respecter pour être sélectionner

**exemple** : On cherche à récupérer seulement les films produits par Disney

```sql
SELECT *
FROM Movies
WHERE studioName = "Disney"
```

#### AND

Il se peut qu'un tuple doit respecter plusieurs conditions en même temps pour être sélectionner. Pour effectuer cela on peut utiliser l'operateur `AND` que l'on peut enchainer

**exemple** : On cherche à récupérer tout les films de Disney produit avant 1999

```sql
SELECT *
FROM Movies
WHERE studioName = "Disney" AND year < 1999
```

### OR

L'operateur `OR` va lui aussi permettre d'appliquer des conditions à respecter pour nos tuples mais il correspond à un `OU` logique. Cela veut dire que les tuples sélectionner vont devoir respecter une condition ou un autre mais pas les deux en même temps

**exemple** On chercher à récupérer les films produit entre 1970 et 1999

```sql
SELECT *
FROM Movies
WHERE studioName = "Disney" AND (year >= 1970 OR year < 1999)
```

## GROUP BY

La clause `GROUP BY` permet de regrouper tous les tuples d'un résultats en fonction d'un attribut.
Celle-ci est utilisé pour appliquer un agrégateur sur le groupe.

**exemple** : On souhaite obtenir le nombre d'heure de film pour chaque studio

```sql
SELECT studioName, SUM(length)
FROM Movies
GROUP BY studioName
```

## HAVING

La clause `HAVING` est une clause similaire à la clause [[#WHERE]]. La différence c'est que celle-ci peut filtrer en utilisant [[Les agrégateurs]].

**exemple** : On souhaite faire la somme de la durée des films par réalisateurs mais on souhaite l'effectuer seulement pour les réalisateurs ayant sorti un film avant 1930

```sql
SELECT name, SUM(length)
FROM MovieExec, Movies
WHERE producerC# = cert#
GROUP BY name
HAVING MIN(year) < 1930
```

Dans son fonctionnement la clause `HAVING` va venir être appliqué pour chaque groupe créer