## Principe

On va boucler sur les éléments du [[Array]]. Si on voit que l'élément est plus petit que l'élément avant lui alors on va déplacer notre élément vers la gauche jusqu'à temps qu'il soit devant un élément plus grand que lui et que lui même soit après un élément plus petit que lui

## Implémentation

```ts
function insertionSort(nums: number[]): number[] {
    for(let i = 1; i < nums.length; i++){
        let key = nums[i];
        let j = i-1;

        while(j >= 0 && nums[j] > key){
            nums[j+1] = nums[j];
            --j
        }

        nums[j+1] = key
    }
    
    return nums
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(n²)$

