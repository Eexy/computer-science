## Principe

Cet algorithme est un algorithme de tri pour trier un [[Array]] en trois parties.

Le principe derrière cet algorithme et que l'on travaille sur un tableau qui possède seulement trois valeurs différente.
On va venir créer un pointeur **low**, **mid** et **high**. 

- Le pointer low va etre initialisé à 0 et va représenter la fin de la première partie
- Le pointeur mid va servir à traverser le tableau
- Le pointeur high va être initialisé avec la dernière position du tableau et va servir à représenter le début de la dernière partie

On va donc boucler sur notre tableau et a chaque fois qu'on l'on trouve un valeur une valeur qui va doit être mis dans la première partie on va faire un swap entre la veleur contenu à mid et a low.
On fera le même swap si on tombe sur une valeur qui doit être placé dans la dernière partie et on continuera notre chemin si on est sur un élément qui appartient au milieu

## Implémentation

Implémentation en imaginant que le tableau est le suivant `[120120]`

```ts
// On suppose une fonction swap qui va venir echanger les élément de place
function dutch(nums: number){
	let low = 0;
	let mid = 0;
	let high = nums.length - 1;

	wihle(mid < end){
		if(nums[mid] === 0){
			swap(nums[mid], nums[low]);
			++mid;
			++low;
		}else if(nums[mid] === 1){
			++mid
		}else{
			swap(nums[mid], nums[high])
			--high;
		}
	}
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(n)$



