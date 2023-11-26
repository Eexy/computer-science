## Principe

L'algorithme se base sur un pivot. On peut choisir ce pivot aléatoirement. On va ensuite créer deux pile. Dans la première pile tous les éléments qui sont avant notre pivot (plus petit) et une autre pile contenant tout les élément après notre pivot (dans l'ordre croissant ou l'ordre voulu)
Grace à cela on sait on connait la place de notre pivot dans notre futur tableau trié. On a juste a répéter ce process dans les deux pile

## Implémentation

```ts

function partition(nums: number[], l: number, h: number): number {
    // On choisi notre pivot. Ici se sera le derniere élément
    int p = nums[h];

    // Indice du premier element plus grand que notre pivot.
    // Dans le tableau tout les element qui ont un index inferieur a firsthigh sont inferieur a notre pivot
    // Tous les élément qui ont un indice superieur sont superieur a notre pivot
    // On l'initialise avec la position la plus petit
    let firsthigh = l

    for(let i = l; i< h; i++){
        // Si l'élément qu'on check est inferieur a notre pivot
        if(s[i] < s[p]){
            // on echange de place avec firsthigh car cela veut dire qu'il ne pointait pas vers le premier élément plus grand que notre pivot et ensuite on increment sa position
            swap(s[i], s[firsthigh]);
            ++firsthight;
        }
    }

    // A la fin on inverse le pivot de place avec notre premier élémént plus grand que le pivot pour avoir notre pivot au centre
    swap(s[p], s[firsthigh])

    // Maintenant firsthigh correspont à la place de notre pivot on peut donc renvoyer sa position
    return firsthigh
}

function quicksort(numbs: number[], l: number, h: number): number[]{
    let p = 0;

    if((h-l) > 0){
        p = partition(nums, l, h);
        quicksort(nums, l, p-1);
        quicksort(nums, p+1, h)
    }

}
```

[[Complexité et notation asymptotique|Complexité]] : $O(nlogn)$

En moyenne la complexité de quicksort est de $O(nlogn)$ mais elle dépend fortement du choix du pivot. En effet si le pivot que l'on choisit est toujours le premier élément du tableau une fois trié alors elle peut aller jusqu'à $O(n²)$. 
Un technique pour éviter cela est de choisir un pivot de manière aléatoire