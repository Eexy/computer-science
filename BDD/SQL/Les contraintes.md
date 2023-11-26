Les contraintes sont comme leur nom indique des contraintes qui vont être appliqué sur les attributs et qui vont se déclencher à la création/modification d'un tuple.
Cela est utile pour s'assurer que la nouvelle valeurs respectent certaines conditions afin d'être utiliser plus tard

Les contraintes sont directement stocké dans la BDD

## Clé primaire

Une clé primaire est une clé qui va être unique à un tuple dans une relation. Ainsi la clé primaire va permettre d'identifier un seule tuple dans toute la relation car aucun autre tuple ne pourra avoir la même valeur sur l'attribut qui à été défini en tant que clé primaire

**exemple** : On possède une table d'utilisateur. Une clé primaire pourrai être l'id de l'utilisateur ou son email. 
En faisant cela on s'assure qu'il n'existe pas deux utilisateurs avec le même email et si on vient à essayer de créer un utilisateur avec un email déjà existant dans notre relation alors on aura une erreur

On défini une clé primaire avec le mot clé `PRIMARY` ou `UNIQUE`

**exemple** : On crée une table d'utilisateur avec une contrainte sur l'email

```sql
CREATE TABLE Users (
	id INT
	email VARCHAR(255) PRIMARY KEY
);
```

## Clé étrangère

Les clé étrangère dans une relations vont permettre de référencer un autre tuple dans une autre relation en faisant référence à une clé primaire de l'autre relation.
Pour que l'insertion/modification soit valide la valeurs que l'on donne a notre clé étrangère doit être une valeur valide dans l'autre relation

C'est grâce au clé étrangère que l'on peut faire des jointures

**exemple** : On souhaite créer une table contenant les adresses de nos utilisateurs. Cela serai bien qu'on puisse récupérer dans notre programme toutes les adresses d'un utilisateur. Pour faire cela on pourrai dire que l'attribut `userId` fait référence à un `id` dans notre table `Users`

```sql
CREATE TABLE Adresses (
	id INT PRIMARY KEY
	userId INT REFERENCES Users(id)
)
```

La base de donnée va gérer les clé étrangère de différentes façon pour maintenir son intégrité :

- Default : Si on essaie de modifier la clé étrangère avec une valeur qui n'existe pas alors elle va créer une erreur et empêcher la modification
- `CASCADE` : Si on vient à modifier la clé de la relation auquel on fait référence la modification va venir se répercuter sur notre tuple. De plus cela veut aussi dire que si on vient à supprimer notre tuple auquel on fait référence alors la BDD va aussi supprimer tous les tuples qui lui font référence
- `NULL` : Dans ce cas-ci si on vient modifier l'attribut sur le tuple que l'on références tous les attributs de toutes les tables qui lui font référence vont prendre la valeur `NULL`. Cela implique aussi que si on vient à supprimer le tuple en question la valeur sera remplacé par `NULL`

**exemple** : On souhaite que si on supprime un utilisateur l'adresse qui lui fait référence prennent la valeur `NULL` pour son champs `userId`. De plus on souhaite que si on met à jour l'utilisateurs alors la mise à jours se répercutent sur les adresses

```sql
CREATE TABLE Adresses (
	id INT PRIMARY KEY
	user Id INT REFERENCES Users(id)
		ON DELETE SET NULL
		ON UPDATE CASCADE
)
```

## Contrainte sur les attributs et sur les tuples

### Contrainte `NOT NULL`

Cette contrainte permet de spécifier qu'une valeur n'a pas le droit d'être `NULL`

**exemple** : On cherche à précisé qu'une adresse doit toujours avoir un nom de rue

```sql
CREATE TABLE Adresses (
	id INT PRIMARY KEY
	streetName VARCHAR(255) NOT NULL
)
```

## Contrainte `CHECK`

Il est possible de définir des contrainte plus complexe en utilisant `CHECK`. En faisant cela on devra juste passer une condition sur notre attribut pour que l'insertion du tuples ou sa modification soit valide

**exemple** : On cherche à précisé qu'une le pays d'une adresses soit seulement la France

```sql
CREATE TABLE Adresses (
	id INT PRIMARY KEY
	streeName VARCHAR(255) NOT NULL
	countryName CHAR(2) CHECK (countryName = "FR")
)
```

Il est aussi possible de déclarer des contraintes `CHECK` seulement si notre tuple possèdent certaines valeurs. Dans ce cas si la vérification de la contrainte se fera unique si le tuple possède les valeurs requise

**exemple** : On attribut un genre à nos utilisateur celui ci doit être égale à `F` si notre utilisateur est une femme. Or si notre utilisateur est un homme son genre doit être `M`. 
On sait donc que pour que le genre soit valide soit on à `gender = "F"` soit le nom de la personne ne doit pas commencer par `Ms.`

```sql
CREATE TABLE Users(
	id INT PRIMARY KEY
	name VARCHAR(255) NOT NULL
	gender CHAR(1)
	CHECK(gender = "F" OR name NOT LIKE 'MS.%')
);
```

## Modification des contraintes

### Nommer les contraintes 

Avant de pouvoir modifier les contrainte il est important de la nommer. En effet si on nomme pas la contrainte alors on ne pourra pas la modifier

On nomme la contrainte avec la commande `CONSTRAINTE` suivi du nom de la contrainte et de la contrainte elle même

**exemple** :
```sql
gender CHAR(1) CONSTRAINT NoAndro CHECK (gender IN ("F", "M"))
```

### Supprimer une contrainte

Pour supprimer une contraindre on utilise la commande `DROP CONSTRAINTE`

**exemple**

```sql
ALTER TABLE Users DROP CONSTRAINTE NoAndro
```

### Ajouter une contrainte

Pour ajouter une contrainte on utilise la commande `ADD CONSTRAINTE`

**exemple**

```sql
ALTER TABLE Users ADD CONSTRAINTE NoAndro Check (gender in ('F', 'M'))
```