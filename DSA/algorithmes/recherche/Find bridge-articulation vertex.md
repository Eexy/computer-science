## Principe

Le moyen le plus simple pour trouver un [[Graph#Vocabulaire#Bridge / Articulated vertex|pont]] dans un [[Graph]] est de tout simplement boucler sur tous les nœuds du graph, enlever chaque nœud un par un et voir si il est encore possible de traverser tous les graph. En effet si on se retrouve avec une partie du graph qu'on ne peut plus accéder alors cela veut dire qu'on à séparer notre graph en plusieurs sous graphe distinct et donc que le nœud qu'on à enlevé était un pont.

Pour réaliser cela on va utiliser l'algorithme [[Depth First Search]] et l'[[Depth First Search#Arbre DFS|arbre DFS]] qu'il génère pour chaque nœud.

En effet en déroulant DFS on remarque que si notre racine de l'arbre possède plus d'un seul enfant alors c'est que notre racine est un pont. On rappelle que durant DFS un nœud B est un enfant d'un nœud A seulement si le nœud A est le parent direct de B et que B ne peut être accéder que par A

Si on reprend notre exemple suivant :

![[dfs-tree.png]]

On voit que le nœud $2$ est un pont. En effet on voit que si on applique DFS en commençant à 2 alors celui-ci possède deux enfants or vu qu'on est obligé de passer par le nœud $2$ pour rejoindre $3$ en venant de $1$ est inversement alors notre nœud $2$ est bien un pont du graphe

Au contraire si on supprime $1$ du graph on voit bien que celui-ci n'est pas un pont car si on applique DFS en partant de $1$ alors on voit que peut toujours atteindre $2$ en partant de $3$ est inversement

Maintenant qu'on a géré cela on va devoir prendre un deuxième cas en compte : le cas où on à une arête qui retourne en arrière.

**Exemple** : 

![[graph-back-edge.png]]



On voit bien qu'ici si on supprime le nœud $2$ on peut quand même continuer atteindre le nœud $1$ depuis le nœud $3$. Cela est dû au fait qu'on à une arête qui pointe en arrière depuis 3 est surtout qui pointe sur un nœud qui est un **ancêtre** de $2$. 

On va donc devoir prendre en compte dans notre algorithme ce genre d'arête. Pour cela on va utiliser deux nouvelles valeurs à chaque nœud. 

La première valeur va tout simplement correspondre à l'ordre dans lequel chaque nœud à été découvert (On va l'appelé **discovery time**). Ici on peut commencer à compter à partir de 0 ou de 1. 
Par exemple dans le graphe juste au-dessus le nœud $1$ à été découvert en premier on va donc lui attribué la valeur $1$ et ainsi de suite.
Forcément ici $1$ est notre point de départ c'est pour cela qu'il a la valeur $1$ dans l'ordre de découverte mais si changeait de nœud comme point de départ cela changerai forcément l'ordre mais cela n'est pas le plus important. Cette valeur deviens importante en l'utilisant de pair avec la prochaine valeur

Le plus important est la second valeur que l'on va attribué à chaque nœud. Cette valeur correspond tout simplement au nœud le plus ancien dans l'ordre de découverte qui peut être atteint en utilisant **seulement une arête qui retourne en arrière**
C'est à dire une arrête qui pointe sur un nœud qui à été découvert avant.
Cette valeur est appelé la **low-link value** est elle peut prendre en valeur soit l'ancêtre qui a été découvert avant et qui est accessible seulement avec une seule arête qui pointe vers l'arrière soit la valeur du nœud actuelle dans le cas où on ne peut pas atteindre de nœud plus ancien.

Cette valeur va donc nous servir justement à détecté les arrête vers l'arrière est donc détecté si l'un de nos descendant peut accéder à des nœuds qui se trouve avant. Ainsi s'il n'existe pas de chemin entre nos descendant et nos ancêtre cela veut dire qu'on est sur un nœud qui fait le lien entre entre les deux coté donc un pont.
De plus cette valeur doit être la plus petite possible car si un de nos descendant peut accéder à l'un de nos ancêtre alors cela veut dire que nous aussi

## Implémentation

```ts
/**
class Graph {
	const edgenode: Record<number, {val: number, nodes: number[]}
}
*/

function findBridge(g: Graph, start: number): number[] {
	const visited = new Array(g.nvertices).fill(false);
	const discoveryTime = new Array(g.nvertices).fill(0);
	const lowLink = new Array(g.nvertices).fill(0);
	const parent = new Array(g.nvertices).fill(-1);
	const bridges = [];
	let order = 0;

	function helper(start: {val: number, nodes: number[]}){
		// Compte le nombre d'enfant du noeud dans l'arbre dfs
		let children children = 0;
		
		// On lui assigne l'ordre dans lequel il est decouvert
		// De base on dit que le noeud le plus ancien qu'il peut atteindre c'est lui même 
		discoveryTime[start.val] = lowLink[start.val] = order++;

		// On parcours tous les noeud adjacent de notre noeud de déparft et on applique DFS
		for(let i of start.nodes){
			// V represente notre noeud adjacent
			const v = i;

			if(!visited[v]){
				children++;
				parent[v] = start.val
				helper(g.edgenode[v])

				// On va venir checker ici si l'un des noeud adjacent peut acceder à nos ancetre. Si c'est le cas alors nous aussi on peut y acceder et donc on à une plus petit low-link value
				low[start.val] = Math.min(low[start.val], low[v]);

				// on va venir etudier les deux cas pour verifier que si notre noeud actuelle n'est pas un pont

				// 1. On check si notre noeud actuelle à plus de 1 enfant dans l'arbre DFS
				if(parent[start.val] === -1 && children > 1){
					birdges.push(start.val);
				}

				// 2. On regarde que tous nos enfant ne peuvent pas acceder à nos ancetre
				if(parent[start.val] !== -1 && low[v] >= disc[start.val]){
					bridges.push(start.val);	
				}
			}else if (v != parent[start.val]){
				// On met a jour la lowlink value de start pour les prochain appelle car en effet on peut accèder à un noeud qui a été decouvert avant et qui à déjà été visité donc cela veut dire qu'on a trouver notre arrete qui pointe en arrière
				low[start.val] =  Math.min(low[start.val], disc[v])
			}
		}		
		
	}

}

// il faut penser à faire une boucle sur tous les noeud du graph et appeler la fonction avec chaque noeud en point de départ 
```

[[Complexité et notation asymptotique|complexité]] : $O(V(V+E)$ où $V$ est le nombre de sommet et $E$ le nombre d'arête

