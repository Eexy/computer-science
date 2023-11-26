Docker compose est un outil pour permettre de lancer/gérer plusieurs container à la fois.
En effet au lieu d'aller chercher chaque dockerfile à la fois et lancer chaque container un par un docker compose va nous permettre de faire cela dans un seul et même fichier
Il va aussi nous fournir d'autre fonctionnalité comme le fait de pouvoir redémarrer tous les containers en même temps, de fournir un ordre de démarrage etc...

## Configuration de Docker compose

La configuration de docker compose se fait à partir d'un fichier qui est en générale à la racine du projet. Il est généralement nommé `compose.yaml`

### Définition des services

Dans notre ficher docker compose le plus important est la définition des services. Cela correspond au différent containers qui vont être lancé. On va ainsi pouvoir définir leur nom, les images à utiliser, les ports, les variables d'environnement comme dans un ficher dockerfile

**exemple** : On défini un service qui va utiliser l'image de redis

```yaml
services : 
	redis : 
		image : "redis:alpine"
		ports : 5000:5000
```

chaque services est défini après le terme `services`. Ensuite on va lui définir un nom. Par exemple ici on a donné comme nom `redis`.
Par la suite on peut définir les différents paramètre comme dans un dockerfile

### Utiliser un docker file

Dans notre docker compose on peut définir comme construire une image mais on peut aussi utiliser un docker file déjà créer et ainsi pouvoir utiliser tous les fonctionnalité comme les [[Les images#Multi-stage image|multi-stages]].
Pour utiliser notre dockerfile il nous suffit de préciser le chemin vers celui-ci pour le service avec la commande `build`

**exemple** : On souhaite utiliser une dockerfile spécifique pour le frontend de notre application

```yaml
services : 
	frontend :
		build : ./frontend
	
	redis : 
		image : "redis:alpine"
		ports : 5000:5000
```

Dans cette exemple docker va aller chercher le dockerfile contenu dans le répertoire `frontend`

On peut aussi spécifier une dockerfile précis dans le cas ou on en a plusieurs avec les paramètres `context` et `dockerfile`

**exemple** : On souhaite définir le dockerfile précisément de notre projet frontend

```yaml
services : 
	frontend :
		build : 
			context : frontend
			dockerfile : ./frontend.Dockerfile
	
	redis : 
		image : "redis:alpine"
		ports : 5000:5000
```

Le paramètre `context` indique dans quel dossier notre dockerfile se trouve et le paramètre `dockerfile` permet d'indiquer le nom du dockerfile

### Utiliser des variables d'environnement

Pour utiliser des variables d'environnement dans notre docker compose on peut lui spécifier notre fichier contenant nos variables d'environnement avec le paramètre `env_file` qui doit être placé en haut de notre docker compose

**exemple** : On cherche à importer nos variable d'environnement depuis notre fichier `.env`

```yaml
env_file : .env

services :
	frontend :
		build : frontend
		ports: ${PORT}:3000
```

Si on a plusieurs fichier contenant des variables d'environnements alors on peut venir spécifier le nom du fichier à l'exécution avec la commande `--env-file`

### Définir un ordre de lancement

Il est possible avec docker compose de définir un ordre de lancement des container pour s'assurer qu'un container B dépendant d'un container A se lance après ce dernier

**exemple** : On souhaite que notre frontend se lance après que notre backend soit lancé

```yaml
services :
	frontend :
		build : frontend
		ports: 5000:3000
		depends_on : backend

	backend :
		build : backend
		ports: 3000:3000
```

Ici notre service frontend est défini comme dépendant de `backend` il démarrera qu'une fois que backend ai entièrement démarré

## Le CLI

### Obtenir la liste de commande

Pour obtenir la liste de commande pour docker compose il suffit d'exécuter la commande

```bash
docker compose --help
```

### Lancer docker compose

Pour lancer docker compose il suffit d'exécuter

```bash
docker compose up
```

La commande doit être lancé dans le même répertoire que notre fichier `compose.yaml`
On peut y ajouter l'option `-d` si on veut le lancer en arrière place

### Lister les compose en route

Pour lister les compose en fonctionnement on utilise la commande

```bash
docker compose ps
```

### Arrêter les service

Pour arrêter les services on utilise la commande

```bash
docker compose stop
```