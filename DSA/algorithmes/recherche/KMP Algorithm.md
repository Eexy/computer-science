Cette algorithme permet de chercher un pattern dans un ensemble plus grand. Par exemple cela serait le fait de chercher un pattern dans une [[String|chaine de caractère]]

## Principe

Le principe derrière cet algorithme est le suivant :

Lorsque l'on cherche un pattern dans une chaine de caractère il se peut que seulement une partie des caractère vont matcher mais pas la fin. Au lieu de recommencer du départ à chaque et de vérifier des lettre qu'on à déjà vu on va directement reprendre de là ou on s'est arrêté 

**Exemple** : https://binary-baba.medium.com/string-matching-kmp-algorithm-27c182efa387

## Implémentation

La première étape de cette algorithme est de construire le tableau de préfix qui sont aussi des suffixe. C'est à dire que l'on doit dans notre pattern les parties du pattern qui correspondent à son début (son préfix)

```ts
function findLps(s: string): { len: number; prefix: number[] } { 
  const prefix: number[] = [0]; 
  let len = 0; 
  let i = 1; 
  while (i < s.length) { 
    if (s[i] === s[len]) { 
      prefix.push(len+1); 
      ++len; 
      ++i; 
    } else { 
      if (len === 0) { 
        prefix.push(0); 
        ++i; 
      } else { 
        len = prefix[len - 1]; 
      } 
    } 
  } 
  return { len, prefix }; 
}
```

[[Complexité et notation asymptotique|complexité]]: $O(n)$

La deuxième étape est tout simplement de chercher dans notre chaine original le pattern que l'on souhaite. Cela se fera beaucoup plus rapidement car on aura juste à checker si on est sur un prefix du pattern. Si ce n'est pas le cas on peut continuer d'avancer

```ts
function findPattern(s: string, pattern: string): number { 
  if (s.length < pattern.length) return -1; 
  if (s === pattern) return 0; 
  const { prefix } = findLps(pattern); 
  let i = 0; 
  let j = 0; 
  while (i < s.length) { 
    if (pattern[j] === s[i]) { 
      ++i; 
      ++j; 
    } 
    if (j == pattern.length) { 
      return i - j; 
    } else if (i < s.length && pattern[j] != s[i]) { 
      if (j == 0) {  
        ++i; 
      } else { 
        j = prefix[j - 1]; 
      } 
    } 
  } 
  return -1; 
}
```

[[Complexité et notation asymptotique|complexité]] : $O(n+m)$ où $n$ est la taille de notre chaine et $m$ la taille de notre pattern