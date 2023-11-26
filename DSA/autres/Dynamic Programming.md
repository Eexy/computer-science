## Principe

Le principe derrière Dynamic programming est la sauvegarde des résultat précédent.
En effet le [[Backtracking]] nous permet de calculer toute les solutions possible d'un problème nous assurant de toujours avoir la meilleure or recalculer des résultats précèdent nous fait perdre du temps. Avec le dynamic programming on va venir sauvegarder les résultats et les sauvegarder comme cela si on a besoin on a juste a directement les récupérer.
C'est une solutions qui marche très bien avec la récursion.

Pour faire un algorithme qui utilise cela on doit juste identifier les sous-problème d'un algorithme qui vont venir être recalculé en permanence et les sauvegarder dans un [[Array]] par exemple. Ainsi on aura juste besoin de regarder dans le tableau

## Fibonacci

Calculer la suite de Fibonacci est un excellent problème où on peut appliquer le dynamic programming.
En effet si on viens a calculer la suite de Fibonacci avec un algorithme récursive on aurai l'algorithme suivant

```ts
function fib(n: number){
	if (n <= 1) return 1;

	return fib(n-1)+fib(n-2)
}
```

En dessinant l'arbre de récursion au aurai le résultat suivant : 

![[computer science/DSA/illustrations/autre/fib.png]]

Avec cet algorithme on aurai une [[Complexité et notation asymptotique|Complexité]] de $O(2^n)$

Or on voit bien qu'en calculant $fib(2)$ dans l'arbre de gauche on est obligé de calculer $fib(1)$ il n'y à donc pas d'intérêt de venir le recalculer à droite. On pourrait donc sauvegarder le résultat précèdent 

```ts
function dynamic(n: number, res: Record<number, number>){
	if(n <= 1) return 1;

	if(res[n]) return res[n]

	res[n] = fib(n-1)+fib(n-2)

	return res[n]
}
```

Ici on va venir sauvegarder le résultat pour chaque $n$ dans une [[Map]] ainsi on aura juste à passer la clé et récupérer le résultat au lieu de venir le recalculer

Cette approche nous fait passer d'une complexité de $O(2^n)$ à $O(n)$

