L'une des forces des BDD relationnel ce sont les jointures. En effet on va pouvoir effectuer des query sur plusieurs [[Les tables|tables]] en même temps et venir récupérer les informations partager entre ces tables

**exemple** : On à une table $Movies$ qui regroupes tout les films et une table $Realisators$ qui contient tout les réalisateurs.

On souhaite récupérer tous les réalisateurs de Star Wars. Pour faire cela on a juste à récupérer dans notre table $Realisators$ tout les réalisateurs qui sont associé à un film Star Wars dans notre table $Movies$

```sql
SELECT name
FROM Movies, Realisators
WHERE title = "Star Wars" AND realisatorId = id
```

Ce query va venir récupérer tout les tuples dans notre table $Movies$ qui sont associé à un film Star Wars. Ensuite il va venir récupérer l'ID du réalisateur dans le tuple et venir dans notre table $Realisators$ récupérer tout les réalisateurs qui ont le même ID.

## Eviter les erreurs d'attribut partagé

Il se peut que l'on travail avec tes entités qui partagent un attribut ayant le même nom. Pour savoir à quelle propriété on fait référence on peut utiliser une notation par point.

En effet dans le query on peut peut acceder au nom de la table et de la propiété

**exemple** : On souhaite trouver tous les réalisateurs et acteurs qui partagent la même adresse

```sql
SELECT MovieStar.name, MovieExec.Name
FROM MovieStar, MovieExec
WHERE MovieStart.address = MovieExec.address
```

## Utilisation de variable

Il peut arriver que l'on doit travailler avec des jointure sur la même table. Pour eviter les erreurs et bien distinguer les differentes instances de la table on peut utiliser des variables

Pour utiliser des variables on à juste à définir notre variable après le nom de notre table dans la clause [[Recherche dans une BDD#FROM|FROM]]

**exemple** : On cherche à récupérer tous les acteurs qui habitent à la même adresse

```sql
SELECT Star1.name, Star2.name
FROM MovieStar Star1, MovieStar Star2
WHERE  Star1.address = Star2.address 
AND Star1.name < Star2.name
```

