## Principe

L'algorithme de Prim est un algorithme pour trouver le [[Weighted graph#Minimum spanning Tree|minimum spanning tree]] d'un [[Weighted graph]].

Son fonctionnement est le suivant :
- On choisis un sommet de départ au hasard
- Tant qu'il y a des sommets qui ne sont pas dans l'arbre (des sommets non parcouru)
	- On sélectionne l'arête avec le plus petit poids entre un sommet qui ai déjà dans l'arbre et un sommet qui ne l'est pas encore
	- On ajoute l'arête et le sommet à notre arbre

## Implémentation

```ts
// On représente le graph avec une adjancy list
const graph = {
  'A': {'B': 4, 'C': 2},
  'B': {'A': 4, 'C': 1, 'D': 5},
  'C': {'A': 2, 'B': 1, 'D': 8, 'E': 10},
  'D': {'B': 5, 'C': 8, 'E': 2},
  'E': {'C': 10, 'D': 2}
};

// Cherche l'arête avec le plus petit cout
function findMinEdge(edges) {
  let minEdge = null;
  let minWeight = Infinity;
  for (const [v, weight] of Object.entries(edges)) {
    if (weight < minWeight) {
      minEdge = v;
      minWeight = weight;
    }
  }
  return [minEdge, minWeight];
}

function prim(graph) {
  // On usitilise un set pour stocker les sommets ajouter au treee
  const mst = new Set();

  // On selectionne le premier sommet comme point de départ
  const startVertex = Object.keys(graph)[0];
  mst.add(startVertex);

  // On initialise les arêtes à parcourir à partir de notre point de départ
  const edges = graph[startVertex];

  // On itère jusqu'a ce qu'on est tous les sommet
  while (mst.size < Object.keys(graph).length) {
    // On cherche l'arête la plus petite en partant de notre point de départ
    const [minEdge, minWeight] = findMinEdge(edges);

    // On ajoute le nouveau sommet à l'ensemble
    mst.add(minEdge);

    // On ajoute tous les sommet accessible depuis notre nouveau point à l'ensemble d'arete a traité
    for (const [v, weight] of Object.entries(graph[minEdge])) {
      if (!mst.has(v)) {
        edges[v] = weight;
      }
    }

    // On supprime l'arête qui vient d'etre ajouté
    delete edges[minEdge];
  }
```

[[Complexité et notation asymptotique|Complexité]] : $O(n²)$, $O(m+nlogn)$

**Amélioration** : Utilise une priority queue comme une [[Heap]] pour toujours avoir l'arête avec le plus petit poids et réduire la complexité a $O(m+nlogn)$