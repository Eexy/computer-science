Un arbre binaire de recherche est un [[Binary tree]] ou l'enfant de gauche de chaque nœud va être plus petit que son parent et où chaque enfant de droite va être plus grand que son parent

L'avantage d'utiliser un arbre binaire de recherche c'est que l'on va pouvoir retrouver un nœud avec une complexité de $O(log_{2}n)$ car celui-ci supporte naturellement la [[Binary search|recherche binaire]]


## Implémentations

### Création d'un arbre binaire de recherche

```ts
function insert<T>(tree: Node<T> | null, val: T): Node<T> {
    if(!tree) return new Node<T>(val)

    if(tree.val < val){
        tree.left = insert<T>(tree.left, val);
    }else{
        tree.right = insert<T>(tree.right, val);
    }

    return tree;
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(h)$

### Recherche

```ts
function search<T>(tree: Node<T> | null, val: T): Node<T> | null {
    if(!tree) return null;

    if(tree.val < val){
        return search<T>(tree.left, val);
    }else{
        return search<T>(tree.right, val);
    }

    return tree;
}

```

[[Complexité et notation asymptotique|Complexité]] : $O(h)$

### Trouver le plus grand élément

```ts
function biggest<T>(tree: Node<T> | null): Node<T> | null {
    if(!tree) return null;

    if(tree.right) return biggest<T>(tree.right);

    return tree;
}

```

[[Complexité et notation asymptotique|Complexité]] : $O(h)$

### Trouver le plus petit élément

```ts
function lowest<T>(tree: Node<T> | null): Node<T> | null {
    if(!tree) return null;

    if(tree.left) return lowest<T>(tree.left);

    return tree;
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(h)$

### Trouver le prédécesseur

Trouver le prédécesseur reviens a chercher l'élément le plus a droite dans le sous arbre gauche

```ts
function predecessor(tree: Node<T> | null): Node<T> | null {
    if(!tree) return null;

    if(tree.left){
        return biggest<T>(tree.left);
    }

    return tree;
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(h)$

### Trouver le successeur

Le successeur dans un arbre binaire est le nœud le plus petit dans le sous-arbre droit

```ts
function successor(tree: Node<T> | null): Node<T> | null {
    if(!tree) return null;
    
    if(tree.right){
        return lowest<T>(tree.right);
    }

    return tree;
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(h)$

### Supprimer un élément

Pour supprimer un élément dans un arbre binaire il faut prendre en compte les 2 cas suivant :

- 1er cas: le nœud que l'on veut supprimer à 1 seul enfant au plus
- 2nd cas: Le noeud que l'on veut supprimer a deux enfant

```ts
function delete<T>(tree: Node<T> | null, val: T): Node<T> | null {
    if(!tree) return null;

    // On parcours l'arbre jusqu'a trouver la valeur que l'on doit supprimer
    if(val < tree.val){
        root.left = delete<T>(tree.left, val);
        return root;
    } else if(val > tree.val){
        root.right = delete<T>(tree.right, val);
        return root;
    }


    if(tree.left == null && tree.right === null){
        return null;
    }else if(tree.left === null){
        return tree.right;
    }else if(tree.right === null){
        return tree.left;
    }

    const temp = sucessor<T>(tree.right);
    tree.val = temp.val;
    tree.right = delete<T>(tree.right);

    return tree;
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(h)$