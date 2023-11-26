Count sort est un algorithme principalement utilisé pour trié les nombres

## Principe

On créer un deuxième tableau qui à autant de place plus une que le plus grand nombre du tableau que l'on souhaite trié. Par exemple si le plus grand nombre de notre tableau est 4 alors on aura 4 places
Une fois cela fait on va venir compter le nombre d'occurrence de chaque nombre et les placer dans leur place correspondant au nombre. Ainsi le nombre d'occurrence de `1` seront à l'index `1`. 
On se retrouves donc avec un tableau d'occurrence. Maintenant que l'on a cela on faire une somme cumulative des occurrences puis déplacer tous les nombre d'une case vers la gauche avec la première case qui va contenir 0.
En faisant cela ce que l'on fait c'est qu'on va indiquer la place qu'aura notre nombre dans le tableau une fois trié.
Il nous reste plus qu'a placé les nombres pour les avoir trié. Dans le cas ou un élément apparait plusieurs fois on va incrémenter la position finale par 1 à chaque fois qu'on le croise pour avoir sa nouvelle position

**Exemple** : On souhaite trié le tableau suivant
```
[1,0,3,1,3,1]
```

On remarque que la plus grande valeur du tableau est `3`. On va donc créer un deuxième tableau qui va compter le nombre d'occurrence de chaque élément de taille 4

```
occurence = [0,0,0,0]
```

On compte le nombre d'occurrence de chaque éléments en les plaçant à la place correspondant au nombre que l'on compte (tous les occurrence pour `1` vont aller dans `occurence[1]`)

```
occurence = [1,3,0,2]
```

On fait la somme cumulative des occurrence

```
occurence = [1,4,4,6]
```

On déplace tous les éléments vers gauche pour obtenir la positions des éléments dans le tableau trié

```
occurrence = [0, 1, 4, 4]
```

Maintenant on reboucle sur notre tableau original et on regarde sa place grâce au tableau d'occurrence. De plus dès qu'on le croise on incrémente le nombre dans le tableau d'occurrence comme ça si on croise encore une fois notre nombre on aura sa position qui sera juste a coté de sa précédente occurrence. A la fin on a donc le résultat : 

```
nums = [0, 1,1,1,3,3]
occurence = [1, 4, 6]
```

## Implémentation

```ts
function countSort(nums: number[]): number[] {
	const max = Math.max(...nums)
	const occurrence = new Array(max+1).fill(0)

	// On compte le nombre d'occurrence
	for(let i = 0; i < nums.length; i++){
		++occurrence[nums[i]];
	}

	// On fait la somme cumulative des occurence
	for(let i = 1; i < occurrence.length; i++){
		occurence[i] += occurrence[i-1]
	}

	// On place les éléments dans notre tableau trié en decrezmentant la valeur contenu dans notre tableau d'occurrence pour obtenir la nouvelle place pour la prochaine occurrence
	const ans = new Array(nums.length).fill(0)
	let i = nums.length-1
	while(i >= 0){
		ans[occurrence[nums[i]]-1] = nums[i];
		occurrence[nums[i]] -= 1;
		--i; 
	}

	return ans

}
```

[[Complexité et notation asymptotique|Complexité]] : $O(n+k)$ avec $n$ qui correspond au nombre d'élément dans notre tableau de base et $k$ le nombre d'élément dans notre tableau d'occurrence