Une transaction est une suite d'opération qui seront exécuté les unes à la suite des autres de manière atomique (soit elle est exécuté correctement soit on annule tout)

## Pourquoi utiliser les transactions ?

### Sérialisation

Dans le monde réel il se peut que plusieurs client vont essayer de venir modifier le même tuple en même temps. Par exemple si on réserve une place dans un avion il se peut qu'une autre personne essaye de réserver le même siège en même temps que nous.
Cela pourrait provoquer une erreur car on se retrouverai avec deux personnes ayant la même place à la fin.
Il est donc important de sérialiser les opérations. Lorsque l'on sérialise les opérations la BDD va les effectuer les une à la suite de l'autre.
Ainsi dans notre exemple une fois que la première opérations aura été effectué alors le siège ne sera plus disponible on aura donc aucun soucis lorsque la seconde sera traité.

Pour sérialiser une opération on utilise donc les transactions. La transaction va venir poser un $lock$ sur le tuple qui est en train d'être traité et toute les transactions qui vont essayer de venir y accéder vont être mis en attente les unes à la suite des autres.

### Atomicité

L'autre avantage des transactions c'est qu'elles vont apporté l'**atomicité**. Dans le monde réel on peut venir enchainer les opération à la suite des autres or il se peut que l'une de nos opérations créer une erreur ce qui va forcément impacter le reste. Avec les transactions on évité cela.
Par exemple si on fait un transfert d'argent et que l'on se retrouve avec un crash alors on 
risque de propager les erreurs au opérations suivante mais en utilisant une transaction on évite cela.
En effet dans une transaction soit tous les opérations sont effectuées soit aucunes ne l'est. Ainsi si ce cas viens arriver tous les opérations effectuer jusque la dans la transaction seront annulé et ce sera comme si rien était arrivé : c'est le concept d'atomicité

## Créer une transaction

Les transactions sont effectuer avec la commande `BEGIN TRANSACTION` et ce termine avec le mot clé `COMMIT` si on souhaite effectuer les modifications ou `ROLLBACK` si on souhaite les annulé

**exemple** : On souhaite retiré 10€ à un compte seulement si celui-ci possède plus de 10€

```sql
BEGIN TRANSACTION
UPDATE Accounts
SET balance = balance - 10
WHERE balance > 10
COMMIT
```

Si on souhaité annulé la modification alors on a juste a remplacer `COMMIT` par `ROLLBACK`

## Isolation de transaction

Il existe plusieurs niveau d'isolation pour nos transaction afin de les optimiser et de spécifier à la BDD comment les traité

## Read Only

Imaginons que notre transaction doit seulement venir lire un tuple et ne rien faire d'autre. Par exemple on reprend notre exemple de réservation de place. Lorsque notre client va venir réserver un siège on va d'abord lui faire la liste de tous les sièges disponibles. Chaque client va seulement lire le tuple correspondant au sièges dans la base de donnée.

On peut donc utiliser une transaction pour cela or on sait que en faisant cela on va venir les exécuter une par une. Etant donnée qu'on ne viens pas modifier la base de donnée il serai plus intéressant de les exécuter en parallèle. Dans le pire des cas un client verrai le siège vide mais ne pourrai pas finir la réservation à la fin.

On est donc dans le cas d'une transaction en lecture seule. Pour effectuer ce type de transaction il faut venir le précisé au début

```sql
SET TRANSACTION READ ONLY;
BEGIN TRANSACTION
COMMIT
```

Une fois cela fait notre BDD pourra venir optimisé notre query et exécuter les transactions en parallèle pour gagner du temps

### Dirty Read

On parle de dirty read quand une transaction essaye de lire un tuple qui est en train d'être utiliser par une autre transaction.

Cela peut-être très utile dans certain cas. Si on reprend l'exemple de réservation de place peut-être que notre transaction peut venir lire les donnée des siège qui sont en train d'être modifié. Dans tous les cas la transaction de fin qui vient à réserver et payé va venir revérifier les disponibilités donc si le siege n'est pas disponible le client devra simplement choisir une autre place

Pour spécifier que l'on peut venir lire les donnée qu'une transaction est en train doit le préciser au début de la transaction,

```sql
SET TRANSACTION READ WRITE
	ISOLATION LEVEL READ UNCOMMITTED
```