Les performances des algorithmes peuvent être étudier indépendamment de la machine ou du langage choisis.

On suppose un modèle d'ordinateur qui possède les propriétés suivantes :

- chaque opérations simple (+,-,=,if, appel a une fonction) équivaut a une étape, 1 unité de temps
- les boucles et les sous routines ne sont pas des opérations simples. Leur nombre d'étape dépend du nombre d'opérations simples quelles vont effectuer. **(sort) n'est pas une opération simple**
- A chaque fois qu'on lit dans la mémoire cela équivaut a une 1 étape.

On mesure ainsi le temps d'exécution d'un algorithme en comptant le nombre d'opération au total qu'il va effectuer

## Complexité

On mesure le temps d'exécution en parlant de complexité d'un algorithme. Il existe 3 cas de complexité

**Pire cas complexité (worst-case complexity)** : Le pire cas de complexité d'un algorithme est la fonction défini par le nombre maximum d'opérations qu'un algorithme va devoir effectuer pour résoudre un problème. Cela reviens a dire que c'est dans ce cas que notre algorithme va être le plus long.
Lorsqu'on analyse un algorithme c'est ce cas l'a que nous étudions et qu'on utilise pour définir le temps d'exécution

**Meilleur cas (best-case complexity)** : Le meilleur cas est tout simplement l'inverse du pire cas. C'est la fonction défini par le nombre minimum d'opérations que notre algorithme va effectuer pour résoudre le problème. C'est donc dans ce cas la que notre algorithme va s'effectuer le plus rapidement

**Le cas moyen de complexité (average-case complexity)** : Le cas moyen est la fonction défini par le nombre moyen d'opérations que notre algorithme va devoir effectuer pour résoudre notre problème.

**/!\\ chacune de c'est complexités définisses une fonction : Le temps en fonction de la taille de l'entrée**

## Big O notation

Il arrive que des moments il est difficile d'analyser une fonction très compliqués. Il est plus simple de parler de la fonction en fonction sa limite supérieur (upper bound) et de sa limite inferieur (lower bound)
On utilise alors la **notation Big O** pour simplifier notre analyse en ignorant les détails qui ne vont pas impacter notre comparaison d'algorithme

La notation big O ignore la différence entre les diffèrent facteur ainsi pour Big O on a

$$
  f(n) = 2n <=> g(n) = n
$$

Cela fait du sens car si on implémente exactement le même algorithme dans deux langage diffèrent. On peut se retrouver avec un écart d'exécution. Par exemple peut-être que notre algorithme ira deux fois plus vite en C qu'en Java. Or cela nous indique rien sur l'algorithme en lui même vu que c'est le même dans les deux cas donc on n'a pas besoin de le prendre en compte tout simplement car on parle de manière général

De plus elle ne s'intéresse qu'au terme qui croit le plus dans la fonction. Si on trouve ce terme alors on a trouvé notre pire cas

### Définition de la notation Big O\*\*

- $f(n)=O(g(n))$ veut dire que $c*g(n)$ est une limite supérieur de $f(n)$. Ainsi il existe une constante $c$ tel que $f(n)$ est toujours $<= c*g(n)$ pour un nombre $n$ assez large
- $f(n)=\Omega(g(n))$ veut dire que $c*g(n)$ est une limite inferieur de $f(n)$. Ainsi il existe une constante $c$ tel que $f(n)$ est toujours $=> c*g(n)$ pour un nombre $n$ assez large
- $f(n)=\Theta(g(n))$ veut dire que $c1*g(n)$ est une limite supérieur de $f(n)$ et que $c2*g(n)$ est une limite inferieur de $f(n)$. Ainsi il existe des constantes $c1, c2$ tel que $f(n)<= c1*g(n)$ et $f(n) >= c2*g(n)$ pour un nombre $n$ assez large

Chacune de ces définitions assumes qu'il existe une constant $n_0$ tel quelles sont valides. Cela est dû au fait que l'on ne s'intéresse pas au petites valeur de $n$ car ce n'est pas important si notre algorithme arrive a trié plus rapidement un tableau de 6 valeurs qu'un autre

### Relation de dominance

Voici la relation de dominance dans la notation big O

$c < log(n) < n < nlog(n)n < n^2 < 2^n < n!$

Cela veut dire qu'un algorithme qui est O(log(n)) s'exécutera plus vite qu'un algorithme qui est O(n!) plus la taille de l'entrée va grandir.

Cette relation s'obtient en utilisant les limites. En effet supposons que l'on ai deux fonctions $f(n)$ et $g(n)$

On pourrait alors utiliser les limite pour savoir qui domine qui

Si on a :

$$lim\frac{f(n)}{g(n)} = \infty$$

Alors on peut dire que **$f(n)$ domine $g(n)$** et donc on peut en conclure que l'on obtient les résultats suivants

$$g(n) = O(f(n)) \\ f(n) = \Theta(g(n)) $$

Si notre limite tendait vers $0$ alors on aurai l'inverse

### Travailler avec la notation big O

#### Additionner les fonctions

La somme de deux fonction en notation Big O est la suivante

$O(f(n))+O(g(n)) => O(max(f(n),g(n)))$
$\Omega(f(n))+\Omega(g(n)) => \Omega(max(f(n),g(n)))$
$\Theta(f(n))+\Theta(g(n)) => \Theta(max(f(n),g(n)))$

Ainsi si on a un algorithme qui est défini par la fonction $n^3+n^2+n+1 => O(n^3)$. Cela reviens a extraire le terme qui grandit le plus vite

#### Multiplier les fonctions

Dans le cas ou on se retrouve avec une multiplication par une constante. On ignore cette dernière ce qui nous donne

$O(c*f(n)) => O(f(n))$
$\Omega(c*f(n)) => \Omega(f(n))$
$\Theta(c*f(n)) => \Theta(f(n))$

**/!\ Cela ne marche seulement si c > 0**

Dans le cas on on se retrouve dans un produit ou les deux fonctions croissent en même temps alors on garde les deux. Ce qui nous donne :

$O(f(n))*O(g(n)) => O(f(n)*g(n))$
$\Omega(f(n))*\Omega(g(n)) => \Omega(f(n)*(n))$
$\Theta(f(n))*\Theta(g(n)) => \Theta(f(n)*g(n))$

**Note** : Dans le monde pro, lorsque l'on passe des entretien ou que l'on réponds a des challenges comme sur leetcode on décide de ne garder que la fonction qui croit le plus vite