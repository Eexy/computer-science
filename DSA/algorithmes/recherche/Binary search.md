## Principe

La recherche binaire (binary search) est une recherche qui s'effectue sur un tableau **trié**. Son fonctionnement est le suivant

Imaginons que l'on souhaite récupéré la position du nombre `1` dans le tableau suivant

```
nums = [1,2,3,4,5,6,7,8,9,10]
```

On commence par regarder l'élément au milieu du tableau ici on va supposer que notre tableau commence à l'indice 1 pour faciliter la compréhension. L'élément au milieu est donc le chiffre 5. On remarque que notre élément est plus grand que ce que l'on recherche donc l'élément que l'on cherche est forcement à sa gauche.

On va alors prendre le milieu du sous tableau `[1...5]`. Ici on a 3. On à le même soucis que précédemment. On reprendre donc le milieu du sous tableau `[1..3]`.

On fait cela jusqu'à tomber sur la valeur que l'on recherche. Si on arrive au début du tableau sans l'avoir trouvé alors l'élément n'est pas dans le tableau

## Implémentation

```ts
function binarySearch(nums: number[] | x: number) number {
	let start = 0;
	let end = nums.length-1;

	while(start <= end) {
		let mid = Math.floor(start+end/2)

		if(arr[mid] === x) return mid

		if(arr[mid] > x){
			end = mid-1;
		}else if(arr[mid] < x){
			start = mid-1;
		}
	}

	// On renvoi -1 si l'élément n'a pas été trouvé
	return -1;
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(logn)$