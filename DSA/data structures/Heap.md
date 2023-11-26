La **heap** est une DS qui est simple et qui est efficace pour supporter les opérations d'une [[Priority queue]] que sont l'insertion et l'extraction du minimum ou du maximum

Une heap est une structure en forme d'arbre ou chaque nœud va être plus petit/ ou plus grand (en fonction de l'implémentation que l'on veut lui donner) que ses enfant. Mais attention une heap n'est que partiellement trié.
La force de la heap c'est que vu qu'elle est partielle trié elle est facile a maintenir et surtout que l'on peut trouver le plus petit élément rapidement (le trie [[Heap sort]] se base dessus).

# Implémentation

On pourrait implémenter une heap avec un arbre binaire par exemple mais en faisant cela on utiliserait de la mémoire en plus pour stocker les pointers vers les enfants de chaque nœud.
Pour résoudre ce problème on peut implémenter un heap grâce à un tableau. La particularité de ce tableau c'est que l'on va utiliser les indices pour se repérer dans notre arbre.

**exemple**: Représentation de la heap en arbre et en tableau

![[heap-implementations.png]]

Dans ce tableau les enfants à gauche seront ceux qui ont un indice qui peut s'écrire sous la forme $2^l + 1$ tandis que les enfants de droite sont ceux de la forme $2^l + 1$ avec $l$
Enfin le parent est à la position $floor(l/2)$

On à donc les fonctions suivante

```typescript
function parent(n: number): number {
    return Math.floor(n-1/2)
}

function leftChild(n: number): number {
    return Math.pow(2, n)+1
}

function rightChild(n: number): number {
    return Math.pow(2,n)+1
}
```

En représentant la heap avec un tableau il y a une chose importante a prendre en compte : **Les trou**. 
En effet il se peut qu'il existe des parents qui n'ont qu'un seul enfant. Or pour correctement les représenter on va devoir laisser des trous à certains endroit ce qui va prendre de la place.
Une technique pour obtenir le moins de vide possible est de commencer a remplir de gauche a droite avec les éléments les plus bas dans l'arbre et ainsi avoir le tableau le plus compacte

En faisant cela la taille de notre heap est de : $h = logn$

On a donc l'implémentation suivante :

```ts
Class Heap {
    vals: number[];

    constructor(){
        this.vals = [];
    }

    getParentIndex(i: number): number{
        return Math.floor(i-1/2);
    }

    getParent(i: number): number{
        return this.vals[this.getParentIndex(i)];
    }

    getLeftChildIndex(i: number): number {
        return 2*n+1
    }

    getLeftChild(i: number): number {
        if(this.getLeftChildIndex(i) > this.vals.length-1) return undefined

        return this.vals[getLeftChildIndex(i)]
    }

    getRightChildIndex(i: number): number {
        return 2*n+1
    }

    getRightChild(i: number): number {
        if(this.getRightChildIndex(i) > this.vals.length-1) return undefined

        return this.vals[this.getRightChildIndex(i)]
    }

    add(val: number): Heap {
        // On insere notre nouveau élément à la fin du tableau
        this.values.push(val)

        // On va deplacer notre élément dans la heap jusqu'a temps de lui donner la bonne place.
        // On va le faire remonter dans le tableau (bubble up)
        let newElementIndex = this.vals.length-1;
        return this.bubbleUp(newElementIndex)
    }

    bubbleUp(index: number): Heap {
        // Si notre élément est déjà au debut de notre tableau alors on peut renvoyer la heap
        if(index === 0) return this
        
        // Si le parent de notre élément lui ai déjà inferieur alors on est déjà à la bonne place
        if(this.vals[getParentIndex(index)] < this.vals[index]) return this;

        // Sinon on echange les deux élément de place et on continu le process dans le cas ou notre futur nouveau parent soit aussi plsu grand que l'élément que l'on viens d'inserer
        this.swap(this.getParentIndex(index), index);
        return this.bubbleUp(this.getParentIndex(index));
    }

    /* Swap la position de j avec celle de i  */
    swap(i: number, j: number): void {
        let temp = this.vals[j]
        this.vals[j] = this.vals[i];
        this.vals[i] = temp;
    }

    min(): number | undefined{
        // On intialise avec une variable temporaire car il se peut que la heap soit vide
        let min = undefined


        // Dans le cas ou notre heap n'est pas vide alors vu qu'on est dans une min-heap l'élément au debut est forcement le plus petit
        if(this.vals.length){
            min = this.vals.shift();

            // On retire l'élément à la fin et on le met au debut
            const end = this.vals.pop();
            this.vals.unshift(end);

            // Maintenant il va faloir verifier que l'élément que l'on viens d'inserer au debut rempli bien la condition qu'il est plus petit que ses enfant
            // Sinon on va devoir le faire descendre (bubble down)
            this.bubbleDown(0);
        }

        return min
    }

    bubbleDown(p: number): Heap {
        // On regarde si l'élément de gauche est plus petit si c'est le cas on echancge de place
        // On fait de meme avec l'élément de droite
        if(this.getLeftChild(p) < this.vals[p] && this.getLeftChild(p) < this.getRightChild(p)){
            this.swap(this.getLeftChildIndex(p), p)
            return this.bubbleDown(this.getLeftChildIndex(p))
        }else if(this.getRightChild(p) < this.vals[p]){
            this.swap(this.getRightChildIndex(p), p)
            return this.bubbleDown(this.getRightChildIndex(p))
        }

        return this;

    }
}
```