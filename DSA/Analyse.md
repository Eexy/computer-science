Pour analyser un algorithme et trouver sa [[Complexité et notation asymptotique|complexité]] il faut trouver son nombre d'opérations dans le pire cas.

On rappelle que les opérations suivantes sont des opérations simples.

- \-
- \+
- appel a une fonction
- comparaison (if)
- =

Ces opérations comptent comme 1 unité de temps.

De plus on rappel qu'on oublie les constantes en les réduisant a 1. Ainsi $0(2n) = O(n)$

## Analyse d'un algorithme simple

**Example:**  Voici l'algorithme qui permet de calculer la somme des $n$ entier

```C
int sum(int n){
    return (n*(n+1))/2
}
```

Ici on a une seule opération simple : l'expression mathématique. On a donc $O(1)$

## Analyse des boucles

Pour analyser les boucles il suffit simplement de compter le nombre total d'opération que la boucle va effectuer

**exemple**: Voila l'algorithme de trie : Selection sort

```c
void selection_sort(int s[], int n)
{
    int i,j; /* counters */
    int min; /* index of minimum */
    for (i=0; i<n; i++) {
        min=i;
        for (j=i+1; j<n; j++){
            if (s[j] < s[min]) min=j;
                swap(&s[i],&s[min]);
        }
    }
}
```

On remarque que la boucle extérieur va de $0$ a $n-1$ elle va donc s'effectuer n fois. La boucle intérieur quand a elle va s'exécuter $n-i-1$ fois.

Donc le nombre exact de fois ou la comparaison est effectuer est de :

$S(n) = \sum_{i=0}^{n-1} \sum_{j=i+1}^{n-1}1 = \sum_{i=0}^{n-1}n-i-1$

Cette somme ajoute les entier de manière décroissante en démarrant avec n-1.

$S(n) = (n-1)+(n-2)+...+2+1$

On peut donc utiliser la formule de la somme des n entier ce qui nous donne

$\frac{(n-1)(n-1+1)}{2} = \frac{n^2-n}{2}$

En simplifiant en utilisant le fait qu'on oublie toujours les facteurs a 1 et en utilisant la formule d'addition dans la notation Big O on obtient

$f(n) = O(n^2)$

Un autre maniere plus simple pour obtenir le resultat est de chercher dans le pire des cas combiens de fois notre comparaison va etre effectué.
On sait que notre boucle externe va toujours s'effectuer $n$ fois quoiqu'il arrive. Ce qui est important de savoir c'est combien de fois notre boucle interne va s'effectuer.

Dans le pire des cas la boucle va aller de 1 a n-1 inclus. Elle va donc s'effectuer n-1 fois.

Une fois que l'on a cela il nous suffit de mettre ça dans la notation Big O en respectant les rêgles comme l'oublie des constant et de suivre les regles de l'addition et de la multiplication. Ce qui nous donne $O(n*n-1) = O(n^2-1) = O(n^2)$

**example: Une boucle jusqu'a la moitié** : Imaginons que nous avons une boucle qui ne s'occupe que de la moitité des entrées

```c
void half(int n){
    for(int i = 0; i < n/2; i++){
        printf(i);
    }
}
```

Ici la boucle va de $O$ a $(n/2)$. On pourrait donc dire qu'on a $O(n/2)$. Or on sait que l'on doit réduit les facteurs et les constante a 1 ce qui nous donne $0(n/2) = O(\frac{1}{2}n) = O(n)$

### Propriété de la somme

Voici quelques propriétés de la somme qui vont être utile pour analyser une boucle

- $\sum_{n=s}^{t}C*f(n) = C*\sum_{n=s}^{t}f(n)$
- $\sum_{n=s}^{t}f(n)+\sum_{n=s}^{t}f(n) = C*\sum_{n=s}^{t}(g(n)+f(n))$
- $\sum_{n=s}^{t}f(n) = \sum_{n=s}^{j}f(n)+\sum_{j+1}^{t}f(n)$
- $\sum_{i=k0}^{k1}\sum_{j=l0}^{l1}a_ij = \sum_{j=l0}^{l1}\sum_{i=k0}^{k1}a_ij$

## Relation de dominance

On peut se retrouver avec un algorithme qui est $O(n!log(n))$. Dans ce cas présent on voit bien $n!$ va croitre plus rapidement que $log(n)$ car $n! >> log(n)$. Si on se retrouve dans un cas pareil alors on dire que $n!$ domine $log(n)$. On peut alors juste garder le terme qui croit le plus rapidement. On a donc $O(n!log(n)) = O(n!)

## Logarithme

**Logarithme** est simplement l'inverse de la fonction exponentiel. Ainsi dire $b^x = y$ est équivalent a dire que $x = log_b y$.

**exemple** : Si on cherche $x$ qui correspond au nombre de fois que l'on doit multiplier $2$ par lui même pour arriver a $16$ alors cela reviens a résoudre l'équation

$$2^x = 16 => x = log_2 16$$

**fact** : Logarithme est l'anagramme d'algorithme

**exemple: Une boucle exponentielle** Etudions une boucle qui croit par une multiplication de facteur par lui même

```c
void exp(int n, int c){
    for(int i = 0; i < n; i = i*c){
        print(i);
    }
}
```

En regardant cette boucle on observe que la condition d'arrêt s'active quand $c^i >= n$. On doit donc trouver $i$ en fonction de $n$. D'après la formule haut dessus on obtient

$$c^i = n => i = log_c n$$

La boucle va donc être exécuté $log_c n$. On a donc une complexité $O(logn)$.

**exemple :** Dans la recherche binaire on cherche un élément dans un tableau déjà trié, on ne sait pas juste à quel emplacement il se trouve.
Pour le trouver on va donc prendre l'élément du milieu. Si c'est le bon élément on renvoie la position sinon on a deux cas.

- Si l'élément recherché est inferieur a celui du milieu on ne garde que la partie gauche du tableau et on continue jusqu'à trouver l'élément ou ne rien trouver
- Si l'élément recherché est supérieur à l'élément du milieu on ne garde que la partie droite et on continue ainsi de suite

Voici l'algorithme en C

```c
int binarySearch(int array[], int n, int x) {
    int low = 0;
    int high = n;

  // Repeat until the pointers low and high meet each other
    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (array[mid] == x)
            return mid;

        if (array[mid] < x)
            low = mid + 1;

        else
            high = mid - 1;
    }

    return -1;
}
```

Ainsi a chaque fois on divise par deux jusqu'a arriver a 1 ou dans la l'autre sens la limite du tableau.

Pour trouver la complexité de l'algorithme on cherche cela reviens a chercher combien de fois on va multiplier 2 par lui même avant d'arriver au milieu du tableau en partant de 1

$$2^x = n/2 => x = log_2(n/2) = log_2(n) - log_2(2) => log_2(n) - 1$$

On simplifie en utilisant les règle sur l'addition et les constante dans la notation big O. Ce qui nous donne

$$O(logn)$$

**important**: Dans la notation Big O ($0(n)$) on ne s'intéresse pas a la base du log

### Propriété du logarithme

#### Ecriture du logarithme

Voici les différentes écriture du logarithme que l'on peut retrouver en fonction de leur base

- base b = $2$ => $lgx$
- base b = $e$ => $lnx$
- base b = $10$ => $logx$

#### Quelque propriétés mathématique

- Addition : $log(a)+log(b)$ = $log(a*b)$
- Soustraction : $log(a)-log(b)$ = $log(a/b)$
- Simplification : $log_a(a) = 1
- changement de base : $log_a b*log_c a = log_c b$
- Puissance : $log_b (x^p) = p*log_b x$

### Logarithme et arbre

#### Arbre binaire

![Inserer image arbre binaire]

Si on a un arbre binaire qui est est un arbre ou a chaque niveau le nombre d'enfant (de feuille) est doublé alors on peut trouver la hauteur de l'arbre juste en ayant le nombre de feuille
En effet on a :

$$n = 2^h => h = log_2 n$$

#### Arbre général

Maintenant essayons de généraliser cette définition. Soit un arbre qui à $d$ feuille où $d=2$ dans le cas d'un arbre binaire alors a chaque niveau il va avoir

$$n = d^h$$

Par conséquent on a :

$$h = log_d n$$

## Récursion

Pour trouver la complexité d'un algorithme récursif on utilise un arbre de récurrence

**exemple**: Imaginons qu'on essaye de trouver la complexité d'un algorithme qui affiche les nombre de n jusqu'à 1

```c
void print(int n) {
    print(n)

    if(n > 1){
        return print(n-1);
    }
}
```

Pour trouver sa complexité on va dessiner un arbre de récursion. Pour cela on va choisir un cas simple a représenter. Par exemple $n=3$

![[basic_tree.png]]

On dessine cette arbre en voyant que chaque appel va faire un sous appel

Pour trouver sa complexité il faut juste trouver le nombre total d'appel dans notre arbre.

Pour cela a coté de chaque niveau on met le nombre total d'appel sur le niveau actuel ce qui nous donne ceci.

![[basic_tree_with_call.png]]

On voit qu'on a 1 seul appel par niveau. On a donc juste a trouver le nombre de niveau total que l'on va avoir. On sait que l'on va de $n$ a $1$. On va donc avoir n niveau avec a chaque niveau 1 appel. Au total on aura donc n appels. Ce qui nous donne une complexité de $O(n)

**exemple: suite de fibonacci** Imaginons que nous devions trouver la complexité de l'algorithme suivant qui permet de calculer la suite de fibonnaci

```c
int fibonacci(int n)
{
  if (n == 0 || n == 1)
    return n;
  else
    return (fibonacci(n-1) + fibonacci(n-2));
}
```

Si on dessine l'arbre de récurrence avec $n=4$ par exemple on obtient ceci

![[fib.png]]

On ajoute les nombre d'appel par niveau

![[fib_with_call.png]]

On remarque les appels se multiplies par deux a chaque niveau en demarrant à partir d'en haut. Ainsi en remarquant ce pattern on en deduis que notre complexité est de

$$O(2^n)$$