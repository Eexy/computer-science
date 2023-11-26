## Principe

Le but est de cette technique est de réduire le nombre de boucle imbriqué et ainsi réduire la [[Complexité et notation asymptotique|complexité]]

**exemple** : Imaginons qu'on à le tableau suivant

```
nums = [1,2,3,4,5]
```

On souhaite calculer la somme des éléments 2 par 2. Ce que l'on pourrait faire serai de boucler sur chaque élément et de faire la somme des 2 éléments. Cela nous donnerai un code comme ceci :

```ts
function sum(nums: number[]) {
	for(let i = 0; i < nums.length; i++){
		let sum = 0;
		for(let j = 0; j < 2; j++){
			if(nums[i+j] < nums.length){
				sum += nums[i+j];
			}
		}
		console.log(sum);
	}
}
```

En faisant cela on remarque qu'on a une [[Complexité et notation asymptotique|complexité]] qui est égale a $O(n²)$

Cela est dû au faite que pour chaque élément on à une sous boucle or il y a un moyen de réduire la [[Complexité et notation asymptotique|complexité]] à $O(n)$ en utilisant la technique **Window Sliding Method**. 

Une analogie à utiliser cette technique serait la suivante. Imaginons que l'on souhaite graissé la chaine d'un vélo. On a deux moyens

- On graisse les éléments 1 par 1
- On graisse les éléments 2 par 2

Dans le premier cas à chaque fois qu'on a graisser notre maillon on doit aller regraisser notre chiffons puis graisser le maillons suivant et ainsi de suite tandis que dans le deuxième cas on va aller graisser les maillons portions par portions en laissant glisser le chiffons. On aura ainsi moins d'étapes a faire car on devra seulement regraisser le chiffon tous les deux maillons 

Cette technique fonctionne de la même façons. On va glisser de portions en portions ce qui sera beaucoup plus rapide et réduira la [[Complexité et notation asymptotique|complexité]] à $O(n)$. On aura alors un algorithme linéaire

## Implémentation

```ts
function sum(nums: number[]) {
	let sum = 0;

	// on créer comence par calculer la somme de notre premiere portion
	for(let i = 0; i < 2 && i < nums.length; i++){
		sum += nums[i]
	}

	// On va maintenant se déplacer de portions en portions en partant de la fin de la portion precedante et en éliminant ce qui se passe avant

	for(let i = 2; i < nums.length; i++){
		console.log(sum)
		sum -= nums[i-2];
		sum += nums[i];
	}
}
```

[[Complexité et notation asymptotique|complexité]] : $O(n)$