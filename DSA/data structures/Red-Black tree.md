Les red-black tree sont des [[Tree]] qui viennent fixer le problème que peuvent avoir les [[Binary search tree]]. 

En effet un arbre binaire de recherche peut avoir se retrouver avec une hauteur $h$ qui est égale à :

$$h = n$$
Cela peut arriver si par exemple tous ses nœuds se retrouvent à droite ou à gauche. Le Red-Black tree viens corriger cela en maintenant une hauteur 

$$h = log(n)$$
Pour obtenir ce résultat chaque nœud va en plus de de sauvegarder sa valeur va sauvegarder une autre variable : sa couleur (rouge ou noir)

De plus un arbre Red-Black doit obéir au propriétés suivantes :

- Chaque nœud est soit rouge ou noir
- La racine est noir
- Chaque feuille (nœud null) est noir
- Si un nœud est rouge alors ses deux enfants sont noir
- Pour chaque nœud le chemin pour aller à ses descendant contient le même nombre de nœud noir 
![[red-balck tree.png]]
## Rotation

La concept de rotation est fondamental dans un Red-Black tree. En effet lorsque l'on va venir modifier notre structure que ce soit en insérant ou en supprimant un nœud notre arbre va devoir continuer à obéir au propriété. 

Pour continuer à respecter ces propriétés on va venir modifier notre arbre après un insertion ou une suppression avec une **rotation**. 

On distingue deux rotations possibles:

- Rotation vers la gauche 
- Rotation vers la droite

Dans une rotation vers la gauche sur un nœud $x$ on suppose que son nœud droit $y$ n'est pas $null$ et dans une rotation vers la droite on suppose que notre nœud à gauche n'est pas $null$ 

![[rotation.png]]

De plus dans la rotation maintiens maintient l'ordre des sous arbres. Ainsi les nœud dans le sous-arbre $\alpha$ précèdent toujours les nœud dans le sous-arbre $\\beta$ 

### Rotation vers la gauche

```ts
function rotateLeft(tree: RBTree, x: Tree){
	const y = x.right;
	x.right = y.left;

	if(y.left !== null) {
		y.left.parent = x;
	}
	y.parent = x.parent;

	if(x.parent === null) {
		tree.root = y;
	}else if(x == x.parent.left){
		x.parent.left = y;
	}else{
		x.parent.right = y;
	}
	y.left = x;
	x.parent = y;
}
```


### Rotation vers la droite

```ts
function rotateRight(tree: RBTree, x: Tree){
	const y = x.left;
	x.left = y.right

	if(y.right !== null){
		y.right.parent = x;
	}

	y.parent = x.parent
	if(x.parent === null){
		tree.root = y;
	}else if(x === x.parent.right){
		x.parent.right = y;
	}else{
		x.parent.left = y;
	}

	y.right = x;
	x.parent = y;
}
```

## Implémentation 

### Insertion

```ts
class RBNode<T> {
	val : T | null
	left: RBNode<T> | null
	right: RBNode<T> | null
	parent : RBNode<T> | null;
	color: "red" | "black"

	constructor(val: T){
		this.val = val;
		this.color = "red"
		this.left = null;
		this.right = null;
		this.parent = null;
	}
}

class RBTree<T> {
	root: RBNode<T> | null;

	constructor(){
		this.root = null;
	}
}
```

```ts
function insert(tree: RBNode<T> | null, val: T): RBNode<T> {
	if(!tree){
		const node = new RBNode<T>(val);
		node.color = "black";
		return node;
	}

	const node = new RBNode<T>(val)
	let temp = tree;
	let prev = null;
	while(temp !== null){
		prev = temp;
		if(node.val < temp.val){
			temp = temp.left;
		}else{
			temp = temp.right
		}
	}

	node.parent = prev;
	if(prev === null){
		return node;
	}else if(node.val < prev.val){
		prev.left = node;
	}else{
		prev.right = node;
	}

	return InsertFix(tree, node)
}

function InsertFix(tree: RBNode<T>, node: RBNode<T>): RBNode<T> {
	while(node.parent.color === "red"){
		if(node.parent === node.parent.parent.left){
			let y = node.parent.parent.right;
			if(y.color === "red"){
				node.parent.color = "black"
				y.color = "black"
				node.parent.parent.color == "red";
				node = node.parent.parent
			}else if(node === node.parent.right){
				node = node.parent;
				rotateLeft(tree, node)
				node.parent.color = "black"
				node.parent.color = "red"
				rotateRight(tree, node.parent.parent)
			}
		}else{
			let y = node.parent.parent.left;
			if(y.color === "red"){
				node.parent.color = "black"
				y.color = "black"
				node.parent.parent.color = "red"
				node = node.parent.parent
			}else if(node === node.parent.left){
				node = node.parent;
				rotateRight(tree, node)
				node.parent.color = "black"
				node.parent.color = "red"
				rotateLeft(tree, node.parent.parent)
			}
		}
	}

	tree.root.color = "black"
}
```
[[Complexité et notation asymptotique|Complexié]] : $O(logn)$

La première partie de l'insertion se fait tout simplement comme une insertion dans un [[Binary search tree]] la différence viens ensuite.

En effet à la fin de notre insertion on va devoir fixer les problème suite à notre nœud. En effet le nouveaux nœud que l'on insert est rouge cela va donc briser les règles de notre Red-Black tree.
On va donc faire appelle à une autre fonction `insertFix` pour rééquilibrer l'arbre.

![[insert_rb_tree.png]]