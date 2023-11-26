En SQL on peut utiliser un query A pour construire un query B. On dit alors que A est un sous query de B.

De plus on peut créer un autre sous query C qui va servir a créer le sous query A et ainsi de suite. On peut utiliser autant de sous query que l'on souhaite

## Production de valeur scalaire

Les sous queries vont nous permettre de produire des **valeur scalaire**.
Un valeur scalaire est une valeur qui peut peut une valeur de l'un de nos attribut.

Etant donné que ces valeurs scalaires peuvent être une valeur d'un attribut alors on peut les utiliser dans les clause [[Recherche dans une BDD#WHERE|WHERE]]

**exemple** : On souhaite récupérer tous les réalisateurs de film Star Wars

Ce que l'on peut faire c'est de récupérer tous les films Star Wars pour ensuite récupérer l'ID du réalisateur. Une fois cela fait on peut alors chercher dans notre table de réalisateurs tout les réalisateur ayant un ID inclus dans le résultat de notre sous query.

```sql
SELECT name
FROM MovieExec
WHERE id = (
	SELECT ExecId
	FROM Movies
	WHERE title = "Star Wars"
)
```

## Utiliser des conditions sur des relations

On peut utilisers des operateurs qui vont produire des booléens sur une relation $R$. Or le seuls moyens de les utilisers et que la relation $R$ soit exprimer avec un sous query

Voici la liste des operateurs

- $EXIST$ : condition qui est vrai si et seulement si $R$ n'est pas vide
- $IN$ : condition qui est vrai si notre valeur $s$ est inclus dans $R$
- $NOT\quad IN$ : Inverse de $IN$
- $>\quad ALL\quad R$ : Condition vrai si et seulement si notre valeur $s$ est plus grande que toute les valeur de $R$
- $>\quad ANY\quad R$ : condition vrai si et seulement si notre valeur $s$ est plus grande qu'au moins une valeur de $R$

**exemple** : On souhaite récupérer tous les producteurs des film d'Harrison Ford

```sql
SELECT name
FROM MovieExec
WHERE id IN
	(
		SELECT producerC#
		FROM Movies
		WHERE (title, year) IN
			(
				SELECT movieTitle, movieYear
				FROM StarsIn
				WHERE starName = "Harrison Ford"
			)
	)
```

## Les sous query corrélé

La plupart du temps on a besoin qu'un sous query ne soit évalué qu'une seule fois mais il peut arriver qu'on ai besoin de le réévaluer pour chaque tuple de notre table.

Dans le cas où notre sous query doit être réévaluer on l'appelle un sous query corrélé.

**exemple** On cherche dans notre table $Movies$ le titre des films qui ont eu un remake donc qui ont une version qui est sorti plus tard

```sql
SELECT title
FROM Movies Old
WHERE year < ANY 
	(
		SELECT year
		FROM Movies
		WHERE title = Old.title
	)
```

## Utilisation de sous queries dans une clause `FROM`

Il est possible d'utiliser un sous query dans une clause [[Recherche dans une BDD#FROM|FROM]]. Pour cela il suffit juste de lui donner un nom

**exemple** : 

```sql
SELECT name
FROM MovieEXEC, (
	SELECT producerC#
	FROM Movies, StarIn
	WHERE title = MovieTitle AND
			year = MovieYear AND
			startName = "Harrison Ford"
	) Prod
WHERE cert# = Prod.producerC#
```