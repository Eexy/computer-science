Les graphes (**graph**) sont une structure très utilisé en informatique car ils permettent de représenter des relations comme par exemple le réseau autoroutier, le réseau d'amis sur les réseau social, les réseau électriques etc...

## Les graphes

Un graphe G est défini par le couple $G = (V, E)$  avec : 

- Un ensemble de sommet (**vertice**) : $V$
- Un ensemble d'arêtes (**edge**) qui relient les sommet  : E

Tous les graphes sont représenter par ce couple mais il existe diffèrent type de graphe

- [[Undirect graph]]
- [[Directed graph]]
- [[Weighted graph]]
- [[Unweighted graph]]
- [[Simple graph]]
- [[Non-simple graph]]
- [[Sparse graph]]
- [[Dense graph]]
- [[Cyclic graph]]
- [[Acyclic graph]]

## Vocabulaire

### Degree

Le degré (**degree**) d'un sommet $A$ correspond au nombre de sommet que l'on peut atteindre depuis ce sommet.

Dans un [[Undirect graph]] on calcul simplement le degré d'un sommet simplement en comptant le nombre d'arête qui le relit tandis que dans un [[Directed graph]] le degré d'un sommet correspond à la somme du nombre d'arête qui sort moins la somme d'arête qui rentre

Dans un graph le sommet avec le plus haut degré défini le degré du graph

### Cycle 

Dans un graphe un cycle est lorsque dans une suite d'arête de le sommet de la première arête et le sommet d'arriver de la dernière arête sont les même 

### Bridge / Articulated vertex

Un pont (**bridge**) ou aussi appelé point d'articulation (**articulated vertex**) est un sommet du graph qui quand est supprimé sépare le graphe en plusieurs sous graph non relié.

algorithme : [[Find bridge-articulation vertex]]

### Spanning tree

Un spanning tree d'un graph $G = (V,E)$ correspond au sous-ensemble $E$ qui relie tout les sommet de $G$ en formant un arbre

## Représenter un graph

Il existe deux manière de représenter un graph

- [[#Adjancy Matrix|les matrice d'agencement]]
- [[#Adjancy List|les liste d'agencement]]

### Adjancy Matrix

Les matrice d'agencement (**adjancy matrix**) sont des matrices $M$ de taille $(n*n)$ où $n$ correspond au nombre de sommet dans le graphe.
Pour chaque élément de $(i,j) \in M$ contient une valeurs numérique allant de $0$ jusqu'au nombre nombre d'arête reliant le point $a$ au point $b$.

**exemple** On essaie de construire la matrix d'agencement du graph suivant

![[graph.png]]

On regarde quelles sont les arête existantes :

- 1 arête allant de $a$ vers $b$ ou inversement
- 1 arête allant de $a$ vers $c$ ou inversement
- 1 arête allant de $b$ vers c ou inversement

On obtient donc :

|     | a   | b   | c   |
| --- | --- | --- | --- |
| a   | 0   | 1   | 1   |
| b   | 1   | 0   | 1   |
| c   | 1   | 1   | 0   |

**exemple** On essaie maintenant de construire une matrice d'agencement mais dans un graph dirigé

![[directed graph example.png]]

On a :

- 1 arête allant de $a$ vers $b$
- 1 arête allant de $a$ vers $c$
- 1 arête allant de $c$ vers $b$

Ce qui nous donne

|     | a   | b   | c   |
| --- | --- | --- | --- |
| a   | 0   | 1   | 1   |
| b   | 0   | 0   | 0   |
| c   | 0   | 1   | 0   |

### Adjancy List

Une autre manière de représenter un graph est d'utiliser un tableau de [[Linked List]]

Dans ce tableau chaque index va représenter un sommet. On va donc associer une [[Linked List]] ou chacun des éléments va correspondre à un sommet que l'on peut atteindre depuis le sommet sur lequel on est

**exemple** : On reprend notre premier exemple et on essaie de cette fois ci utiliser une liste agencement

![[graph.png]]

On à la liste suivante

![[adjancy list.png]]

### Quelle représentation choisir

Voici qu'elle représentation utilisé en fonction de ce que l'on cherche à faire

| Comparaison                                                       | Winner  |
| ----------------------------------------------------------------- | ------- |
| Tester si l'arête (x,y) existe                                    | Matrice |
| Trouver le degrée d'un graph                                      | Liste   |
| Représentation qui utilise le moins de mémoire sur un petit graph | Liste   |
| Représentation qui utilise le moins de mémoire sur un grand graph | Matrice |
| Inserer/supprimer une arête                                       | Matrice |
| Moyen le plus rapide pour traverser un graph                      | Liste   |

De manière général les [[#Adjancy List|liste d'agencement]] sont a préconisé

## Implémentation

On va implémenter un graph en utilisant une [[#Adjancy List]]

### Création

```ts 
class Edgenode{
	val: number; // défini la valeur du sommet
	weight: number; // défini le poid de l'arête
	next: Edgenode | null; // défini le sommet suivant

	constructor(val: number, weight: number = 0){
		this.val = val;
		this.weight = weight;
	}
}

class Graph {
	edgenode: Record<number, {nodes: Edgenode | null, degree: number}>;
	degree: number;
	nvertices: number;
	nedges: number;
	directed: boolean;

	constructor(directed: boolean = false){
		this.edgenode = {};
		this.nvertices = 0;
		this.degree = 0;
		this.nedges = 0;
		this.directed = directed;
	}
}
```

### Insertion

```ts
function insert(g: Graph, vertice: number, val: number): Graph {
	const edgenode = new Edgenode(val);

	// On ajoute le nouveau neoud sur la liste des point adjacent du sommet `vertice`
	edgenode.next = null;
	if(g.edgenode[vertice]){
		if(g.edgenode[vertice].nodes){
			edgenode.next = g.edgenode[vertice].nodes;
		}
	}

	g.edgenode[vertice].nodes = edgenode;

	// On augmente le degree du point
	g.edgenode[vertice].degree =  g.edgenode[vertice].degree ? ++g.edgenode[vertice].degree : 1;

	// On incremente le nombre d'arête dans le graph
	++g.nedges

	// On incremente le nombre sommet dans le graph
	++g.nvertices

	// On regarde si le graph est dirigé. Si il n'est pas dirigé alors il faut aussi qu'on insere l'arrete inverse

	if(!g.directed){
		insert(g, val, vertice)
	}

	return g;
}
```

[[Complexité et notation asymptotique|complexité]] : $O(1)$

## Algorithmes

### Recherche

- [[Bread First Search]]
- [[Depth First Search]]
- [[Find bridge-articulation vertex]]

### Spanning tree

- [[Prim's Algorithm]]
- [[Kruskal Algorithm]]