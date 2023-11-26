Une liste doublement chainé (**Doubly linked list**) est une [[Linked List]] où chaque élément a un pointer vers le suivant et un pointer vers le précèdent

![[doubly linked list.png]]

Grâce à cela on peut revenir en arrière plus facilement mais aussi cela facilite la suppression

## Implémentation

## Création

```ts
class List<T>{
	val: T;
	next: Node<T> | null;
	prev: Node<T> | null;

	constructor(val: T){
		this.val = val;
		this.next = null;
		this.prev = null;
	}
}

function insert<T>(x: T, root: List<T>): List<T> {
	if(!root) return List<T>(x);

	let temp = root;
	while(temp.next){
		temp = temp.next;
	}

	const newNode = new List<T>(x);
	newNode.prev = temp;
	temp.next = newNode;

	return root;
}
```
[[Complexité et notation asymptotique|complexité]]: $O(n)$

### Suppression

```ts
function delete(x: number, root: List<number>): List<number> | null {
	if(!root) return null;

	let curr = root;
	let del = null;
	while(!del && !curr){
		if(curr.data === x){
			del = curr;
		}

		curr = curr.next;
	}

	curr.prev.next = curr.next;

	if(curr.next){
		curr.next.prev = curr.prev;
	}

	return del;
}
```

[[Complexité et notation asymptotique|complexité]]: $O(n)$