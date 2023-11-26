## Utilisation

L'algorithme BFS est un algorithme très utilisé pour trouver le chemin le plus rapide entre deux sommets ou deux nœud. En effet durant sont déroulement on va construire un tableau de parent pour chaque nœud. On va donc pouvoir remonter de parent en parent
Mais ce qui en fait sa spécialité c'est que les sommets sont découvert du plus proche sommet par rapport au point de départ jusqu'aux plus loins
Ainsi on sait que pour aller de racine au sommet voulu on aura le chemin le plus court

## Principe

Bread First search (**BFS**) est un algorithme qui permet de visiter toutes les sommets d'un [[Graph]] ou les nœuds d'un [[Tree]] niveau par niveau

Celui-ci va se baser sur une [[Queue]]. En effet on va choisir un sommet de départ que l'on va mettre dans une queue dans le cas d'un arbre ce sera la racine de l'arbre.

On va traiter le premier sommet de la queue et venir ajouter tous les sommets que l'on peut accéder depuis le sommet actuelle dans la queue. 

Une fois que l'on à fait cela on va passer au prochain sommet dans la queue et ainsi de suite

## Implémentation

### Implémentation dans un arbre

Ici on implémente BFS avec un [[Array]] en tant que [[Queue]] et on imagine que notre arbre est est [[Binary tree]]

```ts
function bfs(root: Node | null) {
	if(!root) return;

	let temp = root;
	const queue: Node[] = [];

	const parent: Record<number, number[]>;
	queue.push(temp);

	while(queue.length){
		let node = queue.shift();

		// On traite le noeud comme on le souhaite ici en l'affichant
		console.log(node);

		if(node.left){
			queue.push(node.left);
			parent[node.left.val] = parent[node.left.val] ? [...parent[node.left.val], node.val] : [node.val];
		}

		if(node.right){
			queue.push(node.right);
			parent[node.right.val] = parent[node.right.val] ? [...parent[node.right.val], node.val] : [node.val];
		}
	}
}
```
[[Complexité et notation asymptotique|Complexité]] : $O(n)$ où $n$ est le nombre de nœud

### Implémentation dans un graph

L'implémentation dans un graph est quelque peu différente. En effet un graph peut boucler sur lui même tel que les [[Cyclic graph]] ou alors on peut avoir une arête qui boucle sur le même sommet dans le cas d'un [[Non-simple graph]]
De plus notre fonction va devoir prendre en paramètre un noeud de départ

On va donc devoir avoir un moyen pour sauvegarder quels sommet ont été visité. Pour l'implémentation on va utiliser type script et on va se baser sur une [[Map]] pour se souvenir de ce qui a déjà été visiter

**Important** : L'exemple donné ne marche pour un [[Undirect graph]] 

```ts
function bfs(g: Graph | null, start: number) {
	if(!g) return;

	const visited: Record<number, boolean> = {};
	const queue: Edgenode[] = []

	let edgenode = g.edgenode[start];

	// On va utiliser la variable pour stocker les parents de chaque noeud
	const parent: Record<number, number[]> = [];
	queue.push(start);
	if(!g.edgenode[start]) return;

	while(queue.length){
		v = queue.shift();
		visited[v] = true;

		// On recupère la liste de sommets que l'on peut acceder depuis `v`
		p = g.edgenode[v].nodes;
		while(p !== null){
			if(!visited[p.val]){
				queue.push(p);
				visited[p.val] = true;
				parent[p.val] = parent[p.val] = [...parent[p.val], v] : [v]
			}

			p = p.next;
		}
	}
	
}
```
[[Complexité et notation asymptotique|Complexité]] : $O(V+E)$ où $V$ est le nombre de sommet et $E$ le nombre d'arête
