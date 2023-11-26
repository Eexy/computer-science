
## Principe

Au lieu de trié les éléments en les comparant l'un par rapport au autre ce trie place les éléments dans des bucket en regroupant les éléments qui partagent une même clé. 
Par exemple si on doit trié des string on peut les regroupé en fonction de leur première lettre. 
Une fois cela fait on va répéter cette opérations au sein des bucket eux même en créant des sous buckets etc...

Cet algorithme se base sur des entier ainsi si on veut l'utiliser il faut pouvoir convertir nos donnée en entier. De plus il existe deux manière de l'implémenter :
- Most significant digit (MSD) : Ici on démarre a gauche. Cette implémentation est la plus efficace et convient plus si on doit trié des strings ou des entier de même taille
- Lest significant digit (LSD) : Ici on démarre a droite donc avec le chiffre des unité et on remonte vers la gauche

**Exemple** Imaginons que l'on souhaite trié un tableau de chiffre. 

```
[170, 45, 75, 90, 802, 24, 2, 66]
```

On pourrait trié ce tableau en se disant que si on trie les éléments chiffre par chiffre alors on finira par obtenir la liste trié de nos entier.

- 1ere étape : On cherche le plus gros élément. Ici c'est `802`. Il y a 3 chiffres dedans donc on va itéré 3 fois
- 2eme étape : On regroupe et on trie les éléments dans des buckets en fonction de leur chiffre des unité. Cela nous donne le tableau suivant
```
[170, 90, 802, 2, 24, 45, 75, 66]
```
- 3eme étape : On refait la même opération avec le chiffre des dizaine. Ce qui nous donne
```
[802, 2, 24, 45, 66, 170, 75, 90]
```
- 4eme étape : On s'occupe du chiffre des centaines ce qui nous donne le tableau trié
```
[802, 2, 24, 45, 66, 170, 75, 90]
```

## Implémentation
 
Radix sort avec l'utilisation de [[Count sort|count sort]] pour trier les éléments entre eux

```ts
function radixSort(nums: number[]): number[] {
	// On recupère le plus grand nombre
	const max = Math.max(...nums)

	// On utilise count sort pour trié chaque chiffre. Vu que l'on veut trié en fonction de la place du chiffre (unité, dizaine, centaine...) on passe l'exposant qui va nous servir à extraire le chiffre et faire le bon nombre de passage
	for(let exp = 1; Math.floor(m/exp) > 10; exp *= 10*){
		countSort(arr, exp)
	}
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(d*(n+b))$ 

- $d$ : Correspond au nombre maximum de chiffre qu'on a dans le plus grand nombre de notre liste
- $n$ : Correspond à la taille de notre liste
- $b$ : Correspond à notre base de notre système (Ici 10 vu qu'on travaille avec des nombres en base 10)