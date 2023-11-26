Un trie aussi appelé **prefix trie** est une structure en forme d'[[Tree|arbre]] qui sert a représenter et stocker des [[String|chaine de caractère]] de manière plus efficace qu'un tableau.

En effet dans un trie chaque nœud va représenter un caractère de la chaine ainsi en parcourant le trie on va pouvoir recréer les chaine de caractère stocker dans la structure.

De plus l'appel aussi **prefix trie** car à partir d'un nœud, d'un caractère on peut voir toutes les chaines de caractère qui en découle

![[trie.png]]

Dans cette exemple on voit que `ba` est un préfix du mot `bateau` et de `baton`

Ainsi un trie est une structure utilisé pour rechercher des mots et pour proposer de l'auto-complétion

## Implémentation

### Création

Le plus important dans un trie et d'indiquer si un nœud est correspond à une fin de mot ou pas. Il faut donc penser à ajouter un indicateur sur le nœud de fin

```ts
class TrieNode {
	value : string | null // on va utiliser la valeur null pour savoir si on est sur la racine
	children: Record<string, TrieNode>
	endOfWord: boolean

	/**
		@param {string} c - la caractère que l'on veut stocker
	*/
	constructor(c: string){
		this.value = c ? c : null;
		this.end = false;
		this.children = {};
	}
}

class Trie {
	root: TrieNode;

	constructor(){
		this.root = new TrieNode()
	}
}
```

## Insertion

Pour insérer un nouveau mot dans un trie on va parcourir toute les lettre de la [[String]] que l'on souhaite insérer et parcourir le trie en passant de lettre en lettre. Si la lettre n'existe pas alors on l'ajoute 

```ts
function insert(s: string, trie: Trie | null): Trie {
	let root = trie;
	if(!trie){
		root = new Trie();
	}

	let node = root.root;
	for(let i = 0; i < s.length; i++){
		if(node.children[s[i]] === undefined){
			node.children[s[i]] = new TrieNode(s[i]);
		}

		node = node.children[s[i]]
	}

	// Une fois qu'on à fini d'inserer le mot on defini que le dernier noeud que l'on à inserer est une fin de mot

	node.endOfWord = true;

	return root
}
```

[[Complexité et notation asymptotique|complexité]] : $O(n)$ où n $n$ est la taille de la chaine à insérer

### Recherche

Pour rechercher une chaine on a juste à parcourir les nœuds et vérifier que le dernier nœud correspondant au dernier caractère de la chaine est bien une fin de mot

```ts
function search(s: string, trie: Trie | null): boolean {
	if(!trie) return false;

	let node = trie.root;
	for(let i = 0; i < s.length; i++){
		if(node.children[s[i]] === undefined){
			return false;
		}else(node.children[s[i]]){
			if(i === s.length-1 && !node.endOfWord){
				return false
			}

			node = node.children[s[i]]
		}
	}

	return true
}
```

[[Complexité et notation asymptotique|complexité]] : $O(n)$ où n $n$ est la taille de la chaine à insérer

