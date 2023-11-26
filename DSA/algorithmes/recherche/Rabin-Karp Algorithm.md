L'algorithme Rabin-Karp est un algorithme pour chercher un pattern dans un ensemble plus grand. Il est principalement utilisé pour chercher un pattern dans une [[String]]

## Principe

Cet algorithme se base sur deux technique

- [[Window Sliding Methode]]
- [[Hash function]]

Pour chercher le pattern de manière plus efficace qu'une recherche naïve on va venir hacher notre pattern. Une fois que l'on à fait cela on va se déplacer dans notre ensemble par portion qui seront de la taille de notre pattern.

On va venir hasher chaque portion de l'ensemble si l'une de nos portion possède le même hash que celui de notre pattern alors on à trouver notre pattern dans l'ensemble

### Implémentation

```ts
function search(s: string, pattern: string) {
	const patternLength = pattern.length;
	const stringLength = s.length;

	// `d` correspond au nombre de caractère possible dans l'alphabet que l'on souhaite traité
	const d = 256

	// `q` est un nombre premier que l'on va utiliser en tant que modulo pour etre sur que notre hash ne depasse pas les limite de la mémoire
	const q = 13;

	for(let i = 0; i < patternLength - 1; i++){
		h = (h*d)%q;
	}

	// On calcul le hash de notre pattern et le hash de la premiere portion par la même occasion
	const hashPattern = 0;
	let hashPortion = 0;
	for(let i = 0; i < patternLength; i++){
		hashPattern = (d*hashPattern+s.charCodeAt(i)) % q;
		hashPortion = (d*hashPortion+s.charCodeAt(i)) % q;
	}

	for(let i = 0; i <= stringLength - patternLength; i++){
		if(hashPortion === hashPattern){
			// On peut avoir deux hash identique avec des lettre differente on s'assure donc que toute les lettres sont correct
			for(let j = 0; j < patternLength; j++){
				if(!s[i+j] != pattern[j]) break;
			}

			return i;
		}

		// On calcul la nouvelle valeur de notre hash pour notre nouvelle portion en utilisant la même approche que la Window Sliding Method
		if(i < N-M){
			hashPortion = (d*(hashPortion - s.charCodeAt(i)*h)+ s.charCodeAt([i+patternLength])) %q;

			if(hashPortion < 0){
				hashPortion = (hashPortion+q)
			}
		}
	}

	return -1
}
```

[[Complexité et notation asymptotique|Complexité]] : $O(nm)$ où $n$ est la taille de notre ensemble et $m$ la taille de notre pattern