## Principe

L'algorithme va suivre le même principe que le [[Selection sort]]. On va chercher notre élément le plus petit, le placer dans le tableau et ainsi de suite la seule différence c'est que pour accélérer le processus on va se basé sur une [[Heap]]

Voici les étapes de l'algorithme

- On insere tous les éléments dans la heap
- On retire le minimum a chaque fois jusqu'à temps qu'on a vidé la heap
- On a notre tableau trié

## Implémentation

```typescript
function heapSort(nums: number[]): number [] {
    let temp: number[] = []

    const heap = makeHeap(nums);

    let val = 0;
    while(val = heap.min() !== undefined){
        temp.push(val);
    }

    return temp
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(nlogn)$

