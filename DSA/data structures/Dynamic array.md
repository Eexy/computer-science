Les tableaux dynamique (Dynamic array) viennent résoudre le principal soucis qu'on les [[Array|tableaux]] de base : **La taille fixe**
En effet on ne sait pas forcément à l'avance la taille du tableau que l'on va devoir créé. Il peut donc être intéressant d'avoir un tableau qui peut grandir autant que l'on souhaite

Son fonctionnement est le suivant :

A chaque fois que l'on ajoute un élément s'il y a plus de place on créé un nouveau tableau en interne qui a deux fois la taille du tableau précèdent. On copie tous les anciens élément et on ajoute le nouveau. Enfin on renvoi le nouveau tableau.

Notre tableau va donc grossir de façon logarithmique. Dans le cas où on multiplie sa taille par deux a chaque fois il va grossir $lgn$ fois.

On pourrait penser que le fait de devoir recopier chaque éléments a chaque fois qu'on doit créer un nouveau tableau pourrai ralentir le fonctionnement mais en fait en moyenne chaque élément va être recopié seulement deux fois. Cela s'explique de la façon suivante

**exemple** : Imaginons que l'on veuille insérer 4 éléments (1,2,3,4)

```ts
let ar = [];

// On insere notre premier élément

ar.push(1)
// ar = [1]

// On souhaite inserer notre deuxième element. On doit donc aggrandir la taille du tableau en la doublant et recopier notre premier élément. Un fois cela fait on peut donc inserer notre nouveau élément

ar.push(2)
// ar = [1, 2]

// Pour l'instant nous avons bouger qu'un seule élément. Il n'y a donc eu qu'un seule mouvement alors que nous 2 éléments

// Continuons en inserant notre élément '3'. On va devoir doubler la taille du tableau en l'a passant à 4. Ce qui nous donne apres insertion

ar.push(3)
//ar = [1,2,3]

// On a du redeplacer notre 1er éléments et notre second élément/ Au total on a donc eu M=2 mouvement

// On ouhaite inserer notre 4 éléments. Cette fois ci il y a assez de place. On peut donc l'inserer sans déplacer les autre

ar.push(4)
//ar = [1,2,3,4]

// M=2

```

On voit bien avec cette exemple que seule la première moitié des éléments vont devoir bougé a chaque fois que l'on double la taille du tableau alors que les éléments de la dernière moitié seront au pire bougé qu'une seule fois et ainsi de suite. 

Ainsi une moitié des élément va bouger qu'une seule fois (la dernière moitié), 1/4 des élément va bouger deux fois et ainsi de suite. Le nombre total de mouvement effectué va donc être

$$M = \sum_{i}^{lgn} = i*\frac{n}{2^i} = n\sum_{i}^{lgn} = \frac{i}{2^i} <= n\sum_{i}^{\infty} = \frac{i}{2^i} = 2n => O(n)$$