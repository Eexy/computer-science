## Insertion

L'insertion en SQL se fait avec la command `INSERT INTO` en précisant la [[Les tables|tables]] et en énumérant toute les valeurs à inséré. Les valeurs seront inséré dans les colonnes en fonction de leur ordre d'apparition.
Ainsi la première valeur sera inséré dans la première colonnes et ainsi de suite

```sql
INSERT INTO R(A_1,...A_n) VALUES (v1,...,vn)
```

**exemple** : On souhaite inséré un nouveau film dans la tables $Movies$

```sql
INSERT INTO Movies VALUES (val1, val2,...valn)
```

Il est possible d'inséré seulement un sous-ensemble de valeur, d'ignorer certains attribut. Pour faire cela on doit énumérer les colonnes à remplir et les valeurs seront aussi inséré en fonction de leur ordre d'apparition
Si on fait cela les valeurs qui n'ont pas été précisé auront la valeur par défaut en fonction de leur type

**exemple** : On souhaite inséré un nouveau tuple contenant seulement le nom du film

```sql
INSERT INTO Movies(title) VALUES ("Star Wars")
```

Enfin on peut inséré plusieurs tuples à la fois en utilisant un [[Les sous queries|sous query]]. 

**exemple** : On souhaite inséré tous les studio de la table $Movies$ qui n'ont pas encore été inséré

```sql
INSERT INTO Studio(name)
	SELECT DISTINCT studioName
	FROM Movies
	WHERE studioName NOT IN (SELECT name FROM studio)
```

## Suppression

La suppression se fait en utilisant la command `DELETE FROM`. En utilisant cette command on va supprimer tous les tuples de la table correspondant à une condition, on ne peut pas préciser un tuple à supprimé

**exemple** : On souhaite supprimer tous les films Star Wars

```sql
DELETE FROM Movies
WHERE name = "%sStar Wars%s"
```

## Modification

La modification se fait en utilisant la command `UPDATE`. Comme la [[#Suppression]] on ne peut pas précisé un tuple spécifique mais on va plutôt définir les conditions à avoir pour que le tuple soit mis à jour

**exemple** : On souhaite venir modifier le nom des réalisateurs pour indiquer s'ils sont président du studio

```sql
UPDATE MovieExec
SET name = "PRES. " || name
WHERE cert# in (SELECT presC# from Studio)
```

En SQL l'operateur `||` permet de venir concaténer 2 string