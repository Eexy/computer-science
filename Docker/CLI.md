Le cli de docker va permettre de pouvoir interagir avec les images, les container, les réseaux etc...

[Docker CLI ref](https://docs.docker.com/engine/reference/commandline/cli/)

## Container

### Créer et lancer un nouveau container

```bash
docker run [OPTIONS] IMAGE_TO_USE [COMMAND] [ARG...]
```

### Lancer un container

```bash
docker start [container_id]
```

### Redémarrer un container

```bash
docker restart [container_id]
```

### Renommer un container

```bash
docker rename [container_id] [new_name]
```

### Lister les containers

Cette commande permet de lister tous les containers avec leur ID. C'est grâce à ses ID que l'on va pouvoir interagir avec les container

```bash
docker ps
```

### Arrêter un container

```bash
docker stop [container_id]
```

### Afficher les logs d'un container

```bash
docker logs [container_id]
```

## Images

### Help

Pour voir les commandes disponibles afin de gérer les images

```bash
docker image help
```

### Créer une image (A partir d'un docker file)

```bash
docker build -t image_name path_to_dockerfile
```
### Supprimer les images

Cette commande permet de supprimer une ou plusieurs images en même temps

```bash
docker image rm image_name...
```

### Lister les images

Il existe deux moyen de lister les images

```bash
docker images
```

```bash
docker image ps
```
### Inspecter une image

```bash
docker image inspect image_to_inspect
```

### Récupérer une image depuis le hub

```bash
docker pull NAME[:AG|@DIGEST]
```

## Volumes

### Lister les volumes

```
docker volume ps
```

### Inspecter les volumes

```bash
docker volume inspect volume-name
```

### Supprimer un volume

```
docker volume rm volume-name [volumes...]
```
