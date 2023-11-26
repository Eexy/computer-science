## Principe

Merge sort se base sur le fait de trié un [[Array]] en le séparant en deux. En le séparant en deux puis de trié le coté gauche et le coté droit. Une fois cela fait on réunie les deux moitié.
On répète cette opération récursivement jusqu'à arriver a des tableau de taille 1 car un tableau de taille 1 est forcément trié

## Implémentation

```ts
function merge(left: number[], right: number[]) number[] {
    const sorted: number[] = [];

    while(left.length && right.length){
        if(left[0] < right[0]){
            sorted.push(left.shift())
        }else{
            sorted.push(right.shift())
        }
    }

    return [...sorted, ...left, ...right]
}

function mergeSort(nums: number[]): number[] {
    if(nums.length <= 1) return nums;

    const mid = Math.floor(nums.length/2);

    const left = mergeSort(nums.slice(0, mid));
    const right = mergeSort(nums.slice(mid));

    return merge(left, right)
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(nlogn)$