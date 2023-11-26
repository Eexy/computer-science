
## Principe  

On cherche le plus petit élément du [[Array]]. Un fois qu'on l'a on inverse l'élément au début et notre plus petit élément. On répète cette action jusqu'à avoir le tableau trié

## Implémentation

```TS
function selectionSort(nums: number[]): number[] {
    for(let i = 0; i < nums.length; i++){
        let kMin = i;
        for(let j = i; j < nums.length; j++){
            if(nums[j] <= nums[kMin]){
                min =  nums[j]
                kMin = j;
            }
        }

        let temp = nums[i];
        nums[i] = min;
        nums[kMin] = temp;
    }

    return nums;
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(n²)$
