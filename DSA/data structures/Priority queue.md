Une queue de priorité (**priority queue**) est une [[Queue]] qui offre énormément de flexibilité. En effet contrairement à une queue normal ici les éléments vont être traité par en fonction de l'ordre dans lequel ils sont arrivé mais en fonction de leur priorité.

On pourrai comparer cela a une liste de tache. En effet dans une liste de tache on effectue les taches en fonction de leur importance et non en fonction dans l'ordre dans lequel on les a rentré.

Un priority queue doit implémenter les 3 opérations suivante :

- Insert($Q, x$) : on insert un élément $x$ dans notre queue $Q$
- Minimum($Q$)/Maximum($Q$) : On renvoi notre item qui a la plus petite ou plus grande priorité
- DeleteMin($Q$)/deleteMax($Q$) : On supprime l'élément avec la plus grande priorité ou inversement

Un priority queue peut être implémenter avec des [[Array]], [[Linked List]]. Une bonne structure pour l'implémenter est d'utiliser un [[Heap]]