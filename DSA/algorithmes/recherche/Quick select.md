
## Principe

L'algorithme quickselect permet de retrouver le k-nième élément dans l'ordre croissant ou décroissant d'un [[Array]].

Cette algorithme se base sur le même principe que [[Quick sort]]. En effet on va choisir un pivot et on va trier les éléments en fonctions du pivot. La différence avec quicksort c'est qu'ici au lieu de s'occuper des deux sous portions à chaque fois on s'occupe seulement de la portion ou notre élément est présent

## Implémentation

```ts
/**
	@param {number} left - indice de l'élément à gauche
	@param {number} right - indice de l'élément à droite 
	@param {number} pivot - position du pivot choisi

*/
function partition(nums: number[], left: number, right: number, pivot: number){
	const pivotVal = nums[pivot];
	// On place le pivot à la fin du tableau
	swap(nums, right, pivot);

	// Indice du premier élément plus grand que le pivot dans la liste une fois trié. Au debut on pointe sur le premier élément de la liste si elle n'est pas encore trié
	let FirstGreater = left;

	for(let i = left; i < right; i++){
		if(nums[i] < pivotVal){
			swap(nums, firstGreater, i);
			++firstGreater
		}
	}

	swap(nums, right, firstGreater);
	return firstGreater;
}

/**
	Retourne le k-nieme plus petit élément
*/
function quickselect(nums: number[], left: number, right: number, k: number){
	if(left === right) return nums[left];

	// Choix du pivot aléatoire
	let pivot = Math.floor(Math.random()*(right-left-1));

	pivot = partition(nums, left, right, pivot);

	if(k === pivot) return nums[k];

	if(k < pivot){
		return select(nums, left, pivot-1, k);
	}

	return select(nums, pivot+1, right, k)
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(n)$ en moyenne l'algorithme à une complexité linéaire mais comme quicksort cela dépend du pivot choisi. En effet si on se retrouve à chaque fois à prendre le premier élément ou le dernier élément de la liste une fois trié alors on aura une complexité $O(n²)$