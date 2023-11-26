Les listes chainés (Linked list) sont une structures qui contrairement au [[Array]] non continu. Cela veut dire que les éléments contenu ne se suivent pas dans la mémoire. 
Ainsi cela permet d'avoir une structure de taille variable on peut donc stocker autant d'éléments que l'on souhaite

![[linked_list.png]]

## Principe

Le fonctionnement d'une linked list est le suivant : Chaque élément va avoir deux propriétés :

 - La valeur qu'ils contiennent
 - Un pointer vers le prochain élément.

C'est grâce à ce pointer que l'on va se déplacer/ajouter/supprimer des éléments. 

## Avantages

- Pas de taille prédéfini on peut insérer autant d'éléments que l'on souhaite
- Les opérations d'insertions et de suppressions se font beaucoup plus facilement et sont plus efficace que dans un [[Array]]


## Désavantages

- Etant donner que les éléments ne se suivent pas dans la mémoire on ne peut pas profiter de la mise en cache faite par le système
- On ne peut pas récupérer un élément grâce à son index. On doit à chaque fois parcourir toute la liste jusqu'à temps qu'on est sur le bonne élément

## Implémentation

### Création

```ts
class List<T>{
    data: T;
    next: null | T;

    constructor(val: T){
        this.data = val;
        this.next = null;
    }
}

function insert(x: number, root: List<number>): List<number> {
	if(!root) return new List<number>(x);

	let temp = root;

	while(temp.next !== null){
		temp = temp.next
	}

	temp.next = new List<number>(x)

	return root;
}
```
[[Complexité et notation asymptotique|complexité]] : $O(n)$

### Recherche

```ts
function recursiveSearch<T>(l: List<T> | null, val: T): List<T> | null {
    if(l === null) return null;

    if(l.data === val) return l;

    return recursiveSearch(l.next, val)
}
```
[[Complexité et notation asymptotique|complexité]] : $O(n)$

### Suppression

Dans ce cas si on doit prévoir les 3 cas suivant :

1. L'élément est au début de la liste
2. L'élément est au milieu
3. L'élément est à la fin

```ts
function delete<T>(list: List<T>|null, val: T) List<T> | null {
    if(!list) return null;

    let curr = l;
    let prev = null;
    while(temp){
        if(curr.data === val){
            if(prev){
                prev.next = curr.next;
            }
        }

        prev = curr;
        curr = curr.next;
    }

    return l;
}
```

## Algorithmes

Etant donné que dans une liste chainé on ne peut pas accéder au éléments juste avec son index on ne peut pas appliquer autant d'algorithme que dans un tableau

### Algorithmes de tri

- [[Merge sort]]

## structures

- [[Stack]]
- [[Queue]]
- [[Doubly Linked List]]