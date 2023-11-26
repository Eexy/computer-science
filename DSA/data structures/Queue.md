Une queue (**queue**) est une structure qui fait l'inverse d'une [[Stack]]. En effet celle-ci applique le fonctionnement **FIFO** (First In First Out). Ainsi cela veut dire que le premier élément inséré est le premier élément à sortir

![[queue.png]]

On peut imaginer cela comme une file d'attente ou le premier arrivé sera le premier servi

Comme pour une [[Stack]] la queue peut être implémenter avec soit un [[Array]] soit avec un [[Linked List]]. De plus elle implémente les deux même méthode que sont :

- Enqueue : on insert un élément à la fin de la queue
- Dequeue : on retire le premier élément


## Implémentation

L'implémentation de la queue est un peu plus complexe que celle de la [[Stack]] car ici on doit toujours garder un pointer sur le premier élément inséré

### création

```ts
class ListNode<T> {
	val: T;
	next: ListNode<T> | null;

	constuctor(val: T){
		this.val = val;
		this.next = null;
	}
}

class Queue<T> {
	back: ListNode<T> | null;
	front: ListNode<T> | null;

	constructor(){
		this.back = null;
		this.front = null;
	}
}

function enqueue<T>(val: T, queue: Queue<T> | null): Queue<T> {
	const node = new ListNode<T>(val);
	
	if(!queue){
		const root = new Queue<T>();
		this.front = node;
		this.back = node;
	}

	// Si le pointer sur la fin de la queue ne pointe sur rien alors c'est que la queue est vide
	if(!queue.back){
		queue.front = node;
		queue.back = node;
		return queue;
	}

	node.next = this.back;
	this.back = node;
	
	return queue;
}
```

[[Complexité et notation asymptotique|complexité]] : $O(1)$


### suppression

```ts
function dequeue<T>(queue: Queue<T> | null): ListNode<T> | null {
	if(!queue) return null;

	// On regarde si la queue est vide
	if(!queue.front) return null;

	const node = queue.front;
	queue.front = queue.front.next;

	// Si notre nouvelle element au debut est null alors c'est que la queue est vide
	if(!queue.front){
		queue.back = null;
	}

	return node;
}
```

[[Complexité et notation asymptotique|complexité]] : $O(1)$