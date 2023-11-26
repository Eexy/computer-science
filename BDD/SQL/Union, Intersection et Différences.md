Les BDD relationnel fonctionnent comme des ensemble ainsi il est possible d'utiliser les opérations des ensembles que sont

- L'Union 
- L'intersection
- La différence

## L'intersection

Il est est possible de récupérer les valeurs appartenant à une intersection de plusieurs [[Les tables|tables]] avec le mot clé `INTERSECT`

**exemple** : On souhaite récupéré le nom et l'adresses des actrices qui sont aussi réalisatrices et qui gagne plus de $10.000.00€$

```SQL
(
SELECT name, address
FROM MovieStar
Where gender = "F"
)
INTERSECT
(
SELECT name, address
FROM MovieExec
WHERE netWorth > 10000000
)
```

## La différence

Il est possible de récupérer les valeurs n'appartenant pas à l'intersection de deux tables avec le mot clé `EXCEPT`

**exemple** : On souhaite récupérer le nom et adresse des acteurs qui ne sont pas aussi des réalisateur

```sql
(SELECT name, adress FROM MovieStart)
EXCEPT
(SELECT name, address FROM MovieExec)
```

## L'union

Il est possible de faire un union de plusieurs table avec le mot clé `UNION`

**exemple** : On souhaite récupérer tous les acteurs et réalisateurs dans la base de donnée

```sql
(SELECT name FROM MovieStart)
UNION
(SELECT name FROM MovieExec)
```