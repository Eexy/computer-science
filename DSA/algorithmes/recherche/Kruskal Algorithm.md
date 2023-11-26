## Principe

Cet algorithme est aussi un algorithme pour trouver le [[Weighted graph#Minimum spanning Tree|minimum spanning tree]] d'un [[Graph]] tout comme l'est [[Prim's Algorithm]].

La différence entre les deux vient du fait que cet algorithme fonctionne mieux avec les [[Sparse graph]] et que dans cet algorithme on ne commence pas avec un sommet en particulier

Le fonctionnement de celui-ci est le suivant :

On va considéré chaque sommet du graphe comme étant son propre composant dans l'arbre qui sera construit à la fin. 

On va ensuite prendre chaque arête en prenant toujours l'arête qui à le plus petit poids et ont va la considéré dans le résultat final seulement si elle relie des composants qui ne sont pas déjà relié

## Implémentation

```ts
function kruskal(g: Graph){
	const edges: Edges[] = createEdgeArray(g);
	// On va imaginer qu'on à implementer quicksort pour trié des arête
	const sortedEdges: Edges[] = quicksort(edges);

	// Creer un arbre pour chaque sommet relié si on relie deux composant alors on fusionne les deux
	const setEdges = new SetUnion();

	for(let i = 0; i < sortedEdges.length; i++){
		// Check si l'arête que l'on traite ne relie pas déjà des composant relié
		if(!isComponentAlreadyLinked(setEdges, sortedEdges[i])){
			setEdges.add(sortedEdges[i]);
		}
	}
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(logn)$

