L'architecture Hexagonal est une architecture qui permet d'organiser une applications en plusieurs parties différentes pour faciliter l'évolution et la maintenance. 

On distingues deux parties différentes

## Les différentes parties

### Le core

Le core est l'élément centrale de l'application c'est lui qui contient toute la logique. Tout va se construire autour de lui

#### Les ports

Les ports vont servir sont principalement des interfaces qui vont définir comment communiquer avec le [[#Le core|core]]

### Les services
Ce sont les services qui vont contenir tout la logique de notre application

#### Les domains

Les domaines contiennent les structures que notre core va utiliser pour sa logique et qui vont être partagé par toute l'application

### Les adapters

Les adapteurs sont les composant qui vont permettre de communique avec le [[#Le core|core]]. Par exemple c'est grâce au adapters que l'on va pouvoir communiquer avec la base de données, c'est dans les adapters que l'on utilise les librairies externes ou les services dont on a besoin.

De plus ce sont les adapteurs qui vont implémenter les [[#Les ports|ports]]

#### Les repository

Les repositories sont comme leur nom indique correspondent au repo. C'est ici que l'on va interagir avec la ou les bases de données

#### Les handlers

Les handlers correspondent au point d'entrée pour notre application depuis l'extérieur. Cela veut dire que c'est ici que l'on va envoyé les données de l'extérieur vers notre core.

Dans le cas d'un API cela correspondrai à nos contrôleurs

exemple : 
- https://www.golinuxcloud.com/hexagonal-architectural-golang/
- https://medium.com/@matiasvarela/hexagonal-architecture-in-go-cfd4e436faa3

## Avantages

- Séparations strictes des composants : Chaque composant est agnostique des autres cela veut dire qu'il n'a pas besoin de savoir en interne comment il marche car les adaptateurs doivent implémenter les différentes interfaces
- Focus : On peut se préoccuper sur ce qui est important, la logique
- Augmentation de la productivité : une fois les ports fini chaque équipe peut travailler sur ça partie
- Amélioration des tests : chaque composant peut être testé de manière isolé
- Facilite le changement d'infrastructure : étant donné qu'on a pas besoin de savoir en interne par exemple comment le repository fonctionne on peut faciliter le changement de base de donnée

## Désavantages

- Architecture lourde pour les petits projets : l'architecture fonctionne parfaitement sur des gros projets bien défini si on est sur des petits projets ou des projets qui doivent avancer vite vaut mieux ne pas la prendre en compte
- Problème de performance : toute l'architecture se base sur des appelles à des fonctions cela peut rapidement devenir couteux si on en abuse

Lien : 
- https://www.golinuxcloud.com/hexagonal-architectural-golang/
- https://medium.com/@matiasvarela/hexagonal-architecture-in-go-cfd4e436faa3
- https://www.youtube.com/watch?v=th4AgBcrEHA&list=PLGl1Jc8ErU1w27y8-7Gdcloy1tHO7NriL


