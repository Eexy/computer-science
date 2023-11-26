## AVG

L'agrégateur `AVG` permet de faire la moyenne d'une valeur

**exemple** : On souhaite faire la moyenne de la fortune des realisateurs

```sql
SELECT AVG(netWorth)
FROM MovieExec
```

## SUM

L'agrégateur `SUM` permet de faire la somme d'une valeur

**exemple** : On souhaite faire la somme des fortune des réalisateurs

```sql
SELECT SUM(netWorth)
FROM MovieExec
```

## COUNT

l'agrégateur `COUNT` permet de compter le nombre de tuples dans le résultats

**exemple** : On souhaite compter le nombre d'acteurs

```sql
SELECT COUNT(*)
FROM MovieStar
```

## MIN

L'agrégateur `MIN` permet d'obtenir la plus petite valeur d'un résultat

**exemple** : On souhaite obtenir la plus petite fortune d'un réalisateur

```sql
SELECT MIN(netWorth)
FROM MovieExec
```

## MAX

L'agrégateur `MAX` permet d'obtenir la plus grande valeur d'un résultat

**exemple** : On souhaite obtenir la plus grande fortune d'un réalisateur

```sql
SELECT MAX(netWorth)
FROM MovieExec
```

## DISTINCT

l'agrégateur `DISTINCT` va permettre d'éliminer les duplicats mais celui-ci ne fonctionne que de pair avec un autre agrégateur

**exemple** : On souhaite obtenir le nombre d'acteur différent dans la table `StarIn`

```sql
SELECT COUNT(DISTINCT name)
FROM StarIn
```