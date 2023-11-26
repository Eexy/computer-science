Une fonction de hashage (hash function) est une fonction qui va venir associer une clé unique à une valeur qu'on lui aura passé en entré. 

C'est une fonction très utile pour principalement deux raisons

1. Vu que la clé est unique le seul moyen de générer la même clé est d'utiliser la même entrée. Cela peut par exemple dans le cas ou l'on veut détecter la copie. En effet si on veut vérifier qu'un texte a été copié on envoi nos deux texte dans la fonction. Si ils produisent la même clé alors ce sont des copies
2. Etant donné que le clé est unique on peut récupéré la donnée de départ si elle a été stocker juste en passant la clé. C'est la base de fonctionnement d'une [[Hash table]]

## Propriétés

Une bonne fonction de hachage possède les deux propriétés suivantes :

1. Elle n'est pas trop couteuse en ressource que ce soit en temps et en mémoire
2. Elle va repartir uniformément les clés pour éviter les collisions

## Fonctionnement

Une fonction de hashage va prendre notre entrée de départ et va venir lui mapper une clé qui va être généralement un gros entier pour venir limiter le risque de collision

**exemple** : On cherche a hasher une [[String|chaine de caractère]] pour l'insérer dans une [[Hash table]]

Dans cette exemple on va supposer que notre [[Hash table]] ne peut stocker que 50 éléments. Une fonction de hashage viable serait de faire la somme de tous les caractère qui la compose avec leur code [[ASCII]] puis d'utiliser un modulo 50 pour lui définir une place

```ts
function hash(s: string, m: number): number {
    let sum = 0;
    for(let i = 0; i <= s.length; i++){
        sum += Math.pow(128, i)*s.charCodeAt(i)
    }

    return Math.floor(sum % m);
}
```

Ici on va venir prendre le code [[ASCII]] des caractère et effectuer un [[Base#Changement de base|changement de base]] pour les avoir en base 128. On fait cela car dans la table [[ASCII]] il y a 128 caractère. En faisant cela on s'assure d'avoir un gros entier et ainsi de limiter les cas de collisions