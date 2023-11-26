Les vues sont des relations qui sont créer à partir d'un query mais qui ne sont pas enregistré dans la BDD. Ce sont des relations virtuelles. 
En effet les relations existe réellement càd que si on cherche dans les fichiers de la BDD on pourra trouver la relation tandis que ce n'est pas le cas des vues

## Utilisations des vues

Il existes plusieurs raison d'utiliser les vues

1. Amélioration de la sécurité : La personnes qui va effectuer un query sur la vue ne peut accéder qu'au donnée de la vue et ne peut pas accéder aux données des relations 
2. Cache la complexité : Les vues vont permettent de cacher la complexité lié au jointure des différentes relations qui la composent
3. Simplification des query : En utilisant une vue l'utilisateur n'a pas besoin de s'occuper des jointures etc... Il peut juste faire un query pour récupérer les données qui l'intéressent 
4. Sauvegarde d'un query complexe : Une vue peut cacher un query complexe. On a juste à le créer une fois et la BDD s'occupera de le recréer d'elle même à chaque appelle de la vue
5. Modification de la BDD : Une vue n'est pas une vrai relation mais on peut lui attribuer des nom d'attribut ce qui permet de venir modifier la BDD sans réellement la modifier

## Créer une vue

Pour créer une vue on utilise la commande suivante : `CREATE VIEW viewName AS sqlQuery`

La commande prend deux paramètres :

- Le nom de le vue
- Le query qui sera utilisé 

**exemple** : On souhaite créer une vue qui liste tous les films de Disney

```sql
CREATE VIEW DisneyMovies AS
	SELECT title, year
	FROM Movies
	WHERE studioName = "Disney"
```

## Effectuer un query sur une vue

Il est possible d'effectuer un query sur une vue de la même façon qu'on aurai fait un query sur une relation normal

**exemple** : On veut récupérer tous les films de notre vue sur Disney

```sql
SELECT *
FROM DisneyMovies
```

## Renommer les attributs

Lors de la création de la vue il est possible de renommer les attributs de la vue simplement en listant le nom des attribut

**exemple**

```sql
CREATE VIEW DisneyMovie(movieTitle, movieYear) AS
	SELECT title, year
	FROM Movies
	WHERE studioName = "Disney"
```

## Supprimer une vue

Pour supprimer une vue on utilise la commande `DROP VIEW viewName`

**exemple** : On supprime notre vue sur Disney

```sql
DROP VIEW DisneyMovie
```

## Modifier une vue

Il est possible de venir modifier une vue mais celle-ci doit répondre à certaines conditions

- La [[Les clauses|clause]] `WHERE` ne doit pas avoir un sous query qui implique R
- La [[Les clauses|clause]] `FROM` ne doit posséder qu'une seule occurrence de R et aucune autre relation
- La [[Les clauses|clause]] `SELECT` doit posséder assez d'attribut pour que les attribut manquant puisse être initialisé à `NULL` ou avec une valeur par défaut

### Insertion

Dans le cas d'une insertion par une vue le nouveau tuple sera inséré dans la relation de base mais pas forcément dans la vue. En effet si le nouveau tuple ne respecte pas les conditions pour être dans la vue alors il ne sera pas inclus

**exemple** : On souhaite insérer un nouveau film à partir de notre vue sur Disney

```sql
INSERT INTO DisneyMovies
VALUES ("test", 1970)
```

### Suppression

Dans le cas d'une suppression les conditions dans la clause `WHERE` vont venir être additionner au condition qui ont été utilisé pour créer la vue. De plus comme dans l'insertion cela va venir supprimé les éléments de la relation utilisait pour la création de la vue

