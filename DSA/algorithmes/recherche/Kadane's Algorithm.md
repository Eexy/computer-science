## Principe

Cet algorithme permet de trouver le sous-ensemble qui à la plus grande somme en mathématique. Ainsi il permet de trouver dans un [[Array]] la séquence qui à la plus grande somme

Son fonctionnement est le suivant :

- On boucle sur les élément du tableau
	- On maintient une variable qui va sauvegarder la somme actuelle
	- On maintient une autre variable qui va sauvegarder la plus grande somme trouver dans le tableau
- On renvoie la meilleur somme

## Implémentation

```ts
function kadane(nums: number[]): number {
	let bestSum = 0;
	let currentSum = 0;
	for(let i = 0; i < nums.length; i++){
		currentSum = Math.max(0, currentSum + nums[i]);
		bestSum = Math.max(bestSum, currentSum);
	}
	return bestSum
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(n)$