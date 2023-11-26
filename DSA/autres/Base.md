Il existe plusieurs base numérique pour représenter les nombres

- base binaire : 0,1
- base décimale : 0,1...,9
- base hexadécimal : 0,1,...,F
- base octal : 0,1,...7
- etc...

En faite il existe autant de base que l'on souhaite et il arrive que l'on doit travailler avec ces différentes base il est donc important de savoir comment on passe d'une base à l'autre

## Changement de base

Il existe de cas différent lors d'un changement de base

1. Aller vers une base plus grande (ex: binaire vers decimal)
2. Aller vers une base plus petite (ex: décimal vers binaire)

### Aller vers une base plus grande

Aller vers une base plus grande ce fait très simplement. Pour cela il suffit de prendre chaque chiffre dans la base de départ de la droite vers la gauche et de le multiplier par la puissance de sa base élevé en fonction de sa position en commençant à 0

Ce qui nous donne la formule suivante

$$
\sum_{0}^{n-1} = a*(b^i)
$$

**Exemple** : On souhaite convertir le nombre `10` en binaire vers son nombre correspondant en sa version décimal.

On applique la formule qui nous donne

$$
10 = 1*(2^1)+0*(2^0) = 2+0 = 2
$$
### Aller vers une base plus petite

Pour aller vers une base plus grande on devait multiplier alors que pour aller vers une base plus petite on doit faire la division euclidienne par la base souhaite. Une fois cela fait On remonte les opérations dans le sens inverse 

![[changement de base.png]]

