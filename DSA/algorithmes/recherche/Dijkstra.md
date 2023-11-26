## Principe

L'algorithme dijskta est un algorithme utilisé pour trouver le chemin le plus court entre deux sommets d'un [[Weighted graph]].

Pour cela il part dû principe que si on est essaye de relier deux point $A$ et $B$ et que le chemin passe par un point $C$ alors il faut qu'on cherche le chemin le plus court entre $A$ et $C$ et ainsi de suite

illustration : https://www.programiz.com/dsa/dijkstra-algorithm

Pour résoudre les sous-problème a chaque itération on va parcourir tous les sommets adjacent et ajouter celui qui à la plus petite distance entre notre point de départ et le sommet actuelle

## Implémentation

```ts
function dijkstra(g: Graph: start: number) {
	const intree: Record<number, boolean> = {};
	// On stock la distance la plus petite entre notre point de départ et notre point actuelle
	const distance: Record<number, nbumber> = {};
	let current = start;
	let next = 0;
	let weight = 0;
	// taille du chemin le plus court depuis le départ
	let dist = 0; 

	for(const key of Object.keys(g.edgenodes)){
		intree[Number(key)] = false;
		distance[Number(key)] = Infinity;
	}

	distance[start] = 0;

	while(!intree[current]){
		intree[current] = true;
		let p = g.edgenodes[current].nodes;
		while(p !== null){
			next = p.val;
			weight = p.weight;

			// On met a jour la distance qui sépare notre point par rapport au d'épart
			if(distance[next] > distance[current]+weight){
				distance[next] = distance[current]+weight;
			}

			p = p.next;
		}

		current = 1;
		dist = Infinity;
		for(let i = 1; i <= g.nvertices; i++){
			if(!intree[i] && dist > distance[i]){
				dist = distance[i];
				current = i;
			}
		}
	}
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(n²)$

