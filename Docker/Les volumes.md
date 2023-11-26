Les volumes sont un moyen de rendre les données d'un container persistantes. En effet les container ne sauvegardent pas leurs données ainsi à chaque fois que l'on éteint ou redémarre un container tous les données qui ont été créées sont supprimer.
Pour éviter ceci on va utiliser un volume. Un volume va permettre de monter un dossier/fichier de l'hôte dans le container. Ainsi si le container écrit ou lit à cette endroit il accèdera/modifiera le dossier/fichier qui est situé sur l'hôte et non dans le container
Ce dossier/fichier étant sauvegarder sur l'hôte sera toujours présent même après l'extinction/redémarrage de notre container

[Volume doc](https://docs.docker.com/storage/volumes/)

## Créer un volume

Un volume est créer à partir du cli en utilisant la commande suivante

```bash
docker create volume volume-name
```

Une fois que l'on à créer notre volume on peut venir l'inspecter avec la commande

```bash
docker volume inspect volume-name
```

## Lier un volume à un container

La liaison entre le volume et le container se fait au moment du lancement de ce dernier en ajoutant l'option `--mount` et en precisant les informations suivantes :

1. Le type de mount : dans notre cas cela sera un `volume`
2. Le nom du volume à utiliser
3. L'endroit dans le container ou l'on doit le monter (endroit du container que l'on veut sauvegarder)

**exemple** : Liaison d'un container à un volume pour enregistrer les fichier de sqlite

```bash
docker run --dp 3000:3000 --mount type=volume,source=volume-name,target=/etc/todos image-name
```

