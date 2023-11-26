Un arbre est une structure non continu et qui s'étend vers le bas. Dans un arbre chaque élément est appelé un **nœud** (ou feuille). Chacun de ses nœuds possède des enfants qui sont eux même des nœud et ainsi de suite.
Enfin le nœud qui est au départ de l'arbre est appelé la **racine**

**Exemple**
![[tree.png]]




La **hauteur** de l'arbre va dépendre du nombre de nœud qu'il possède et combien d'enfant chaque nœud peut avoir.

Par exemple on va parlé d'un [[Binary tree]] si chaque nœud peut posséder au plus d'enfant ainsi pour calculer la taille d'un arbre qui possède $n$ nœud on peut appliquer la formule suivante

$$
h = log_{k}(n)
$$
où la $k$ va correspondre au nœud de nœud maximum que peut avoir un arbre. Dans le cas d'un [[Binary tree]] on aurai

$$h = log_{2}(n)$$
