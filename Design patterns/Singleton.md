Ce pattern sert à s'assurer qu'il y a toujours une seule instance de notre objet qui existe dans tous notre programme. Par exemple cela peut-être utile de l'utiliser pour représenter une connexion à une base de donnée ou pour la lecture d'un fichier afin de s'assurer qu'il y a toujours une seule connexion

**exemple** : Pour implémenter ce pattern on ne peut pas passer par la création d'un objet avec `new`. En effet a chaque fois qu'on appelle le constructor on à une nouvelle instance. Pour résoudre cela on va laisser le constructor en privé. Ainsi il ne pourra pas être appelé.
Ce que l'on va faire c'est que l'on va faire qu'on la créée une méthode static qui va nous renvoyé une instance de la class si elle existe sinon elle va en crée une

```typescript
class Database {
	private Datatabase database;

	private constructor(){
		// code to create database
	}

	static getInstance(){
		if(this.database) return this.database;

		this.database = new Databse()
		return this.database;
	}
}
```