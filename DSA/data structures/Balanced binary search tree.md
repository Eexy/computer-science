Un arbre binaire de recherche équilibré (Balanced binary search tree) est un [[Binary search tree|binaire de recherche]] dont la taille est exactement

$$h = log(n)$$
Cela implique donc que la différence de hauteur des sous arbres est d'au plus 1

![[balanced binary tree.png]]

En étant équilibré la [[Complexité et notation asymptotique|complexité]] des opérations de base est diminué ce qui nous donne :

| Operations  | Complexité |
| ----------- | ---------- |
| Insertion   | $O(logn)$  |
| Suppression | $O(logn)$  |
| Recherche   | $O(logn)$  |


## Implémentation

Voici comment créer un arbre équilibré à partir d'une liste de nombre déjà trié

```ts
/**
class TreeNode{
	constructor(val: number, left?: number, right?: number){
		this.val = val;
		this.left = left ? new TreeNode(left) : null;
		this.right = right ? new TreeNode(right) : null
	}
}
*/
function createBalanceBinaryTree(nums: number[]): TreeNode | null{
	if(!nums.length) return null

	let mid = Math.floor(nums.length/2);

	const root = new TreeNode(nums[mid]);
	root.left = createBalanceBinaryTree(nums.slice(0, mid));
	root.right = createBalanceBinaryTree(nums.slice(mid+1));

	return root;
}
```