Les décorateurs sont un pattern qui va permettre d'ajouter des comportements à nos objet pendant l'exécution du programme
Il faut les utiliser lorsque notre objet ne peut pas hérité comme par exemple dans le cas où il hérite déjà d'une classe ou lorsque cela deviens bizarre de lui ajouter un comportement

**Exemple** : On à un objet qui écris dans un fichier. En fonction des paramètre de l'utilisateur celui-ci pourra compressé le fichier ou encore l'encrypter. Pour cela on va venir écrire des decorateurs pour ses deux cas et venir les appliquer en fonction de la situation

```typescript
class DataSource {
	write(data) // write data from file
	read() // read data from file
}

abstract class DataSourceDecorator{
	original: DataSource; // object that have been wrapped

	constructor(original){
		this.original = original
	}

	abstract write(data) // metho that must been implemented by decorator and accept the same type of data that the original object and must return the same type of data also
	abstract read() // same as above
}

class EncryptDecorator extends DataSourceDecorator(){
	original: DataSource;

	constructor(original){
		this.original = original
	}

	write(data){
		// encryp data
		data = encrypt(data)
		return this.original.read(data)
	}

	// do samething with read
}

function writeData(data, encrypt){
	const source= new DataSource()

	if(encrypt){
		source = new EncryptDecorator(source)
	}

	source.write(data)
}
	
```