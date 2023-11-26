Une pile (**stack**) est une structure qui implémente le fonctionnement **LIFO** (Last In First Out). Cela veut dire que le dernier élément inséré dans la pile sera le premier élément a sortir.

On peut imaginer cela comme une pile d'assiette. C'est à dire que dans une pile d'assiette on prend toujours celle qui est au-dessus donc la dernière inséré.

Une Pile peut être implémenter avec un [[Array]] mais est plus généralement représenter avec une [[Linked List]].
Celle-ci ne possède que deux opérations

- Push : on insert un élément sur la pile
- Pop : on retire le dernier élément inséré

## Implémentation

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

function push<T>(val: T, stack: ListNode<T> | null): ListNode<T> {
	const node = new ListNode<T>(val);
	node.next = stack;
	return node;
}
```

[[Complexité et notation asymptotique|complexité]] : $O(1)$


### suppression

```ts
function pop<T>(stack: ListNode<T> | null): ListNode<T> | null {
	if(!stack) return null;

	const node = stack;
	stack = stack.next;
	return node;
}
```

[[Complexité et notation asymptotique|complexité]] : $O(1)$