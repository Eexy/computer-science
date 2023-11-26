Le backtracking est une manière de généré les solutions d'un problème en essayant de calculer toutes les solutions tout en les calculant une seule fois pour ainsi éviter les répétitions et optimisé les ressources nécessaire.

Pour cela on va diviser le problème en sous-problème. On va essayer de résoudre ces sous-problèmes et les enregistré dans un ensemble contenant les solutions de tous ces problème ainsi chacun de ses sous-problème va venir étendre notre ensemble de solutions

L'un des moyens de voir le backtracking est le [[Depth First Search]]. En effet on va d'abord parcourir tous les sous-problème avant de traiter notre problème original.

**Exemple** : On essaie de construire tous les ensemble d'un ensemble de taille $n$

Imaginons que notre ensemble est de taille $n = 3$.
Faire cela reviens à tous simplement calculer le nombre de sous-ensemble de taille $n = 1$, $n=2$ et $n = 3$

Ainsi on doit donc calculer toute les possibilités possibles on est donc sur un problème de backtracking

## Pruning

Le **Pruning** est le concept qui consiste à résoudre le nombre de sous-problème à résoudre. Celui-ci se base sur le fait que si on à trouvé  une solutions $B$ qui est meilleurs que $A$ alors cela ne sert à rien de continuer à calculer $A$

**Exemple** : On essaie de calculer toutes les positions que prendre un simple pion au echec.

On sait qu'un pion ne peut avancer que tout droit donc cela ne sert à rien de prendre en compte les cases sur les coté ou derrière. 

Ainsi on viens de résoudre le nombre de sous-problème à résoudre

## Heuristic

Le backtracking nous donne une méthode pour trouver la solutions optimale parmi un tas de solutions. Or calculé toutes les solutions sur une large instance d'un problème est sûr d'échouer pour causes de manques de ressource que ce soit du temps ou de la mémoire.

On va donc voir des méthodes alternatives pour résoudre ces problème. 

- [[Random Sampling]]
- [[Local Search]]