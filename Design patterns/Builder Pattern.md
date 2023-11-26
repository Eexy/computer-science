Ce pattern est un pattern de création qui va permettre de créer des objet complex étape par étape. Il va principalement servir pour permettre la création de différentes représentation tout en gardant le même code de construction et eviter le code à rallonge et telescoper lors de la création d'objet

**exemple** : On souhaite construire une maison.
- On créer les murs
- On ajoute le toit
- On pose les fenêtre 
- On met la porte

Ce que l'on viens de décrire c'est notre code de construction de l'objet maison. Or si maintenant on veut faire évoluer notre maison pour ajouter un garage, une piscine, un jardin ?
Ce que l'on pourrait faire ça serait de créer différente classe pour tous les créer sauf qu'ici on se retrouve encore avec un problème : que fait-on si on veut une maison avec une piscine et un jardin ?
En effet si on représente chaque type de maison par une classe alors on est bloqué et on ne peut pas faire évoluer.
Ce que l'on pourrait faire c'est de rester sur notre classe maison de base et lui passé les paramètre que l'on souhaite

En faisant cela on va se retrouver avec un classe difficile à instancier car on aura énormément de champs à définir même si on souhaite créer une maison basique.

C'est à ce moment la que le pattern va être utile. En effet dans notre classe maison on va venir définir toutes les propriété qu'elle supporte: toit, mur, jardin, piscine etc...

Ensuite dans notre code de construction de notre objet on ne va garder que les étapes de la constructions communes a tout les types de maison. Ici on parle des murs, l'ajout du toit, les fenêtre et la porte

Enfin on va venir implémenter des méthodes ou des fonctions qui vont venir modifier notre objet afin de lui ajouter les propriété voulu

```typescript
class House {
	walls: number
	roof: bool
	winws: number
	door: bool
	pool: boolean
	garage: boolean

	constructor(roof, windows, door, walls){
		this.roof = roof;
		this.windows = windows
		this.door = door
		this.walls = walls
		this.garage = false;
		this.pool = false
	}

	addGarage(){
		this.garage = true;
		return this
	}
// do samething with pool etc...

}
```

