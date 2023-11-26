Les triggers sont des fonctions qui vont se déclencher lorsqu'un évènement dans la BDD se produits généralement lorsqu'une modification se produit comme la modification d'un tuple, une suppression ou un ajout.

**exemple** : Voici un trigger qui va venir empêcher de venir baisser le salaire d'un réalisateurs

```sql
CREATE TRIGGER NetWorthTrigger
AFTER UPDATE OF netWorth on MovieExec
REFERENCING 
	OLD ROW as OldTuple
	NEW ROW as NewTuple
FOR EACH ROW
WHEN (OldTupe.netWorth > NewTuple.netWorth)
	UPDATE MovieExec
	SET netWorth = OldTuple.netWorth
	WHERE cert# = NewTuple.cert#
```

## Ecriture d'un trigger

### Créer un trigger

Pour écrire un trigger on commence par le déclarer en lui donnant un nom avec la commande `CREATE TRIGGER`

```sql
CREATE TRIGGER name
```

### Spécifier un évènement

On va devoir ensuite lui donner un évènement pour qu'il se déclenche. Il y 3 événements :

1. `UPDATE`
2. `DELETE`
3. `INSERT`

et précisé si on veut qu'il se déclenche sur la modification d'un attribut ou sur toute la table.

Si on veut qu'il se déclenche sur la modification d'un attribut on doit venir le précisé

```sql
AFTER UPDATE OF attributName on tableName
```

Si on veut qu'il se déclenche sur toute la relation alors on lui passe juste le nom de celle-ci

```sql
AFTER UPDATE OF tableName
```

De plus on peut précisé si il se déclenche avant ou après la modification du tuple avec les mots clé `BEFORE` et `AFTER`

Ainsi on peut créer un trigger qui va se déclencher avant que le tuple soit inséré

```sql
BEFORT INSERT ON Movies
```

### Référencer les états avant/après modification

Il nous faut maintenant référencer la table ou le tuple avant et après sa modification. Pour cela on utilise la commande `REFERENCING`

```sql
REFERENCING
	NEW ROW as NewRow
	OLD ROW as OldRow
```

```sql
REFERENCING
	NEW TABLE as NewTable
	OLD TABLE AS OldTable
```

### Boucler sur les tuples

Pour boucler sur les tuples sur lesquels on travail on utilise la command

```sql
FOR EACH ROW
```

### Déclarer la condition

La condition pour que le trigger viennent interagir avec les tuples est déclarer avec la command `WHEN`. Si aucune condition n'est fourni (pas de commande `WHEN`) alors le trigger sera déclenché pour tous les tuples

Une fois la condition déclarer on peut lui passer les action à réaliser dans un bloc qui commence par `BEGIN` et se termine par `END`  dans le cas ou on va enchainer plusieurs opération sinon on peut ne pas les utiliser

```sql
WHEN (OldTupe.netWorth > NewTuple.netWorth)
BEGIN
	UPDATE MovieExec
	SET netWorth = OldTuple.netWorth
	WHERE cert# = NewTuple.cert#
END
```