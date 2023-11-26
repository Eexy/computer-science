## Principe

On parcours notre tableau et on compare chaque élément avec son voisin de droite. Si l'élément à droite est plus petit alors on inverse leurs position. On répète cela jusqu'à temps que notre tableau soit trié

## Implémentation

```ts
function bubbleSort(nums: number[]): number[] {
    let isSorted = true;
    for(let i = 0; i < nums.length; i++){
        for(let j = 0; j < n-i-1; ++j){
            if(nums[j] > nums[j+1]){
                const temp = nums[j];
                nums[j] = nums[j+1];
                nums[j+1] = temp;
                isSorted = false;
            }
        }

        if(isSorted) break;
    }

    return nums;
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(n²)$