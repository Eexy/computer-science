## Principe

Le but de ce trie est de trier les nœud d'un [[Directed graph]] pour chaque arête $uv$ d'un sommet $u$ à un sommet $v$, $u$ apparait avant $v$ une fois trié

Pour faire ce trie on va utilise un algorithme appelait **algorithme de Kahn**.

Dans cette algorithme on va passer sur chaque nœud et compter le nombre d'arêtes entrante. Une fois cela fait on va placer dans une [[Queue]] chaque nœud n'ayant pas d'arête entrante. 
En faisant cela on s'assure que tous les nœud ayant été mis dans la queue n'ont pas de nœud qui vient avant eux.
On va donc s'occuper des éléments de la queue un par un. Etant donnée que les éléments de base n'ont pas d'arête entrante on peut directement les placer dans notre tableau trié
De plus on va venir baisser retirer une arête entrante à tous les nœud accessible depuis le nœud actuelle. Si ce nombre devient égale a 0 alors on peut placer le nœud dans la queue
## Implémentation

```ts
/*
 g = {
	 1: [2,...]
	 2: [3,....]
 }

*/

function sort(g: Record<number, number[]>): number[] {
	const indegree = Record<number, number> = {}
	for(const [key, value] of Object.entries(g)){
		if(indegree[Number(key)] === undefined){
			indegree[Number(key)] = 0;
		}

		for(let i = 0; i < value.length; i++){
			let node = value[i];

			if(indegree[node] === undefined){
				indegree[node] = 1
			}else{
				++indegree[node]
			}
		}
	}

	const queue = [];

	for(const [key, val] of Object.entries(g)){
		if(!indegree[Number(key)]){
			queue.push(Number(key))
		}
	}

	const sorted = [];
	while(queue.length){
		const node = queue.shift();
		sorted.push(node)
		for(const neighbor of g[node]){
			--indegree[neighbor];

			if(!indegree[neighbor]){
				queue.push(neighbor)
			}
		}
	}
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(V+E)$