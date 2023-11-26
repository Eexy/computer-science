## Principe

Une recherche linéaire est la recherche de base pour trouver un élément dans un tableau. Il suffit simplement de parcourir le tableau jusqu'à la fin et regarder si on ne trouve pas notre élément

## Implémentation

```ts
function linearSearch(nums: number[], x: number): number {
	for(let i = 0; i < nums.length; i++){
		if(nums[i] === x) return i;
	}
	
	return -1;
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(n)$