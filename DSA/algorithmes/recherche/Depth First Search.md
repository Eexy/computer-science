## Utilisation

Depth First search (**DFS**) est un algorithme très utilisé pour repérer les cycle dans un graph. En effet contrairement a [[Bread First Search]]. Ici sa spécialité c'est que l'on va parcourir tout un chemin avant de continuer notre exécution ainsi si un chemin boucle sur lui même on à va vite le savoir
La principale utilisation de cette algorithme est pour évaluer les [[Decision Tree|arbre de décision]]. En effet lorsque l'on utilise un arbre de décision la réponse se trouve en bas de l'arbre il nous faut donc un moyen d'y arriver le plus rapidement possible.

## Principe

Depth First Search (**DFS**) est comme [[Bread First Search]] un algorithme pour parcourir tous les sommets d'un [[Graph]] ou d'un [[Tree]].

La différence avec BFS c'est son exécution. En effet la ou BFS utilise une queue pour parcourir la structure DFS lui utilise une [[Stack]]

En utilisant une [[Stack]] on va d'abord explorer tout un chemin avant de passer au suivant. Ainsi par exemple dans un [[Binary tree]] on va explorer d'abord l'un des sous arbre et seulement quand on aura fini de l'Explorer on passera au suivant.

## Arbre DFS

Lorsque l'on applique l'algorithme DFS que ce soit dans un arbre ou dans un graph celui-ci va générer un arbre qui va permettre de représenter dans quel ordre les nœuds on été découvert. Cela va donc indiqué sont déroulement on appelle cela l'arbre DFS

**Exemple** : Voici les arbre DFS du graph ci-dessous en fonction des point de départs

![[dfs-tree.png]]

Dans cette arbre on considère qu'un nœud B est un enfant d'un nœud A seulement si durant le déroulement de l'algorithme celui ne peut être atteint que par A et que A est son parent direct. 

## Implémentation

L'implémentation peut se faire de manière itérative comme avec [[Bread First Search]] on remplace juste la [[Queue]] par une [[Stack]] ou alors peut aussi l'implémenter de manière récursive.

### Implémentation dans un arbre

#### Implémentation recursive

Ici on va implémenter une [[Stack]] avec un [[Array]]

```ts
function dfs(root: Node | null){
	if(!root) return;

	console.log(root);
	
	if(root.left) {
		dfs(root.left);
	}

	if(root.right){
		dfs(root.right);
	}
}
```
[[Complexité et notation asymptotique|Complexité]] : $O(n)$ où $n$ correspond au nombre de nœud dans l'arbre

#### Implémentation itérative

```ts
function dfs(root: Node | null){
	if(!root) return;

	const stack: Node[] = [root];
	
	while(stack.length){
		const node = stack.pop()
		console.info(node);

		if(node.left){
			stack.push(node.left);
		}

		if(node.right){
			stack.oush(node.right);
		}
	}
}
```
[[Complexité et notation asymptotique|Complexité]] : $O(n)$ ou $n$ est le nombre de nœud

### Implémentation dans un graph

#### Implémentation récursive

**Important** : L'exemple donné fonctionne seulement pour un [[Undirect graph]] 

```ts
function dfs(g: Graph | null, start: number) {
	if(!g) return;

	const visited: Record<number, boolean> = {};

	return recursiveDfs(g, start, visited);
}

function recursiveDfs(g: Graph, start: number, visited: Record<number, boolean>){
	if(!g.edgenode[start]) return;

	visited[start] = start;

	// On parcours la piles de sommet adjacent
	const p = g.edgenode[start].nodes;
	while(p != null){
		if(!visited[p.val]){
			recursiveDfs(g, p.val, visited);
		}

		p = p.next;
	}
}
```
[[Complexité et notation asymptotique|Complexité]] : $O(V+E)$ ou $V$ est le nombre de sommet et $E$ le nombre d'arête

#### Implémentation itérative

**Important** : L'exemple donné fonctionne seulement pour un [[Undirect graph]] 

```ts
function dfs(g: Graph | null, start: number) {
	if(!g) return;

	if(!g.edgnode[start]) return;

	const visited: Record<number, boolean> = {};
	visited[start] = true;

	const stack: number[] = [start];
	while(stack.length){
		let v = stack.pop()
		let p = g.edgenode[v].nodes();

		while(p !== null){
			if(!visited[p.val]){
				visited[p.val] = true;
				stack.push(p.val)
			}

			p = p.next;
			
		}
	}
}
```
[[Complexité et notation asymptotique|Complexité]] : $O(V+E)$ ou $V$ est le nombre de sommet et $E$ le nombre d'arête