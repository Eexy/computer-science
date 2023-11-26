Ce pattern va permettre de définir différentes stratégies, algorithme en fonction de la situation et surtout de les rendres interchangeable

**exemple** : On à application de map qui va permettre de calculer le meilleur itinéraire pour aller d'un point A à un point B. Au début notre application n'est capable d'effectuer cette opération que pour les trajet à pied.
Par la suite on cherche à permettre à l'utilisateur de définir s'il souhaite effectuer le trajet à pied ou en voiture. On pourrait alors tout simplement ajouter une méthode en qui va venir faire ce calcul. Cependant si on augmente le nombre de moyen de transport disponible on va vite se retrouver avec code compliqué à maintenir.
Or ce que l'on pourrait faire c'est de passer l'algorithme à utiliser, la strategy pour calculer l'itinéraire en fonction du choix de l'utilisateur.

```typescript
class Map {
// implementation de la class

	calculatePath(strategy, start, end){
		return strategy(start, end)
	}
}

// Utiliser pour calculer le trajet en voiture
function calculateCarPath(start, end) {

}

// Utiliser pour calculer le trajet à pied
function calculateWalkPath(start, end){

}

// .. autre methode de transport

function main(){
	const map = new Map()
	const start = a;
	const end = b;
	const method = method

	if(method === "car"){
		return map.calculatePath(calculateCarPath, start, end)
	}
	// Faire le reste avec les authe moyen de transports
}
```