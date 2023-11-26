Une image dans docker est le modèle qui va être utilisé pour créer notre container. L'image va contenir tout les instructions nécessaire au bon fonctionnement comme par exemples :

- Les ports à utiliser
- Le code à utiliser
- Les commandes à exécuter
- etc...

Une fois l'image construite on va pouvoir la lancer dans notre container

## Dockerfile

Le `Dockerfile` est le fichier qui va contenir les instructions pour pour la construction de notre images

### Instructions

[Dockerfile référence](https://docs.docker.com/engine/reference/builder/)
#### FROM

L'instruction `FROM` va permettre de définir une image que l'on va utiliser pour créer notre propre image.
En effet dans docker on peut créer une image à partir d'une autre afin de gagner du temps. Ainsi par exemple on peut créer une image qui va servir à lancer une application Nodejs en partant de l'image communautaire afin de gagner du temps. De plus en faisant cela on s'assure que tout ce qui est nécessaire à Nodejs est correctement installé

```dockerfile
FROM node:18-alpine
```

#### WORKDIR

L'instruction `WORKDIR` va permettre de définir le dossier de travail de notre image. C'est dans ce dossier que toute les autre instructions seront exécuté

**exemple** : On défini le dossier `/app` comme dossier de travail

```dockerfile
WORKDIR /app
```

#### COPY

L'instruction `COPY` va permettre de copier un répertoire/ficher de l'hôte dans les container. Il est important de prendre en compte que cette copie est effectué au moment de la création de l'image est pas au moment du lancement du container. De plus chaque copîe est effectuer à partir du dossier de travail

**exemple** : On copie le répertoire actuel dans notre image
```dockerfile
COPY . .
```

#### RUN

L'instruction `RUN` va permettre l'exécution de commande lors de la création de notre image et seulement pendant la création de l'image.
On va pouvoir exécuter chainer plusieurs commande en les séparant avec l'operateur `&&\`

**exemple** : Installation des packages nécessaire à notre application nodejs

```dockerfile
RUN npm install
```

#### CMD

L'instruction `CMD` va aussi nous permettre d'exécuter une commande mais cette fois-ci au lancement de notre container contrairement à l'instruction `RUN`.
De plus contrairement à cette dernière il ne peut avoir qu'une seule instruction `CMD`

**exemple** : Lancement de notre application une fois le container lancé

```dockerfile
CMD ["npm", "start"]
```

Comme les autres instructions celle-ci est exécutée dans notre dossier de travail

#### EXPOSE

L'instruction `EXPOSE` va permettre de venir exposer des ports de notre container afin de pouvoir s'y connecter

**exemple** : On expose le port $3000$
```dockerfile
EXPOSE 3000
```

Si on souhaite exposer plus de ports alors on à juste à enchainer les instructions `EXPOSE`

#### ENV

L'instruction `ENV` va permettre de passer des variables d'environnements. Comme la commande `EXPOSE` on peut avoir autant de variables d'environnent que l'on souhaite

**exemple** : On défini l'environnement pour notre application nodejs

```dockerfile
ENV NODE_ENV=production
```

## Multi-stage image

Il est possible de séparer la création de notre image en plusieurs étapes que l'on va appeler des `stages`. Cela peut-être très utiles dans plusieurs situations

- On veut lancer les tests avant de créer l'image final
- On souhaite garder garder une fonctionnalité spécifique par exemple dans le cas d'une application avec typescript notre première étape serai de compiler le code ts en code js et de ne garder que le code js pour la fin
- On souhaite garder notre dockerfile facile à lire et à maintenir

Pour utiliser les stages il nous suffit de de définir un nom à nos images intermerdiare avec l'instruction `AS <name>` et d'y faire référence avec l'instruction `--from=<name>`

**exemple** : On souhaite lancer les tests avant de construire notre image de prod

```dockerfile
FROM node:18-alpine AS base
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "test"]

FROM base
WORKDIR /app
COPY --from=base . .
CMD ["npm", "start"]
EXPOSE 3000
```

