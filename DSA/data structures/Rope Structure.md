Cette structure est un moyen de représenter les [[String]] autre que part un [[Array]]. En effet l'une des opérations que l'on fait souvent sur des strings est de venir ajouter un élément ou encore de venir concaténer deux chaines de caractère pour en former une nouvelle or si on fait cela avec un tableau on se retrouve avec une [[Complexité et notation asymptotique|complexité]] de $O(n)$

Ainsi la représentation par corde (**rope structure**) va venir améliorer les performances de cela.
Cette structure se base un [[Binary tree]] ou chaque nœud va contenir une string et ainsi l'arbre pourra représenter de longue chaine de charactère.
De plus chaque nœud va aussi contenir le poids de son sous arbre gauche avec le poids d'une feuille correspondant à la taille de chaine de charactère qu'il contient

Cette structure est souvent utiliser pour manipuler de grosse quantité de texte comme par exemple dans un éditeur car par exemple il est facile de revenir en arrière (CTRL+Z) étant donné qu'on à juste a venir supprimé le denier nœud créé

![[Vector_Rope_example.svg]]

**Implémentation** : [Wikipedia implémentation](https://en.wikipedia.org/wiki/Rope_(data_structure))

lémentation](https://en.wikipedia.org/wiki/Rope_(data_structure))

