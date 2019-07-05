
#Document

## Méthodes

`Récupérer 
```javascript
let test = document.geElementById(result);
```

À la base 
```html
		<table>
				<thead>
					<tr>
						<td>Message</td>
						<td>nbTry</td>
						<td>nbToFind</td>
					</tr>
			</thead>
			<tbody id="result">
		
			</tbody>
		</table>

		<script src="../js/jeu.js"></script>
```

Grâce à la fonction afficheResultat(data)
J'affiche de manière dynamique le message, le nombre d'essais et le nombre qui était à trouver


# DOM
Le Document Object Model ou DOM (pour modèle objet de document) est une interface de programmation pour les documents HTML, XML et SVG. 

Il fournit une représentation structurée du document sous forme d'un arbre et définit la façon dont la structure peut être manipulée par les programmes, en termes de style et de contenu. 


DOM représente le document html, avec tous ses éléments y compris ses id et ses class.

## Sélection un élément dans HTML

Cibler par l'id
```javascript
let monID = document.getElementById("masection");
console.log(monID);
```

Cibler par la class
```javascript
let mesClasses = document.getElementsByClassName('avion');
console.log(mesClasses);
```
Cibler par le nom de la balise
```javascript
let maBalise = document.getElementsByTagName("p");
console.log(maBalise);
```

Cibler tout type d'un élément 
```javascript
let p = document.querySelector('p');
console.log(p);

let p = document.querySelector('#masection');
console.log(p);

let p = document.querySelector('#masection, p'); // récupérer l'id="masection" et les p
console.log(p);

let p = document.querySelector('.avion');
console.log(p);

let lesP = document.querySelectorAll('p');
console.log(lesP);
```

## La manipulation 

Manipuler 1 élément
```javascript
monID.innerHTML = 'Test'; // change masection en Test car on a été récuperer ma section dan sle document html pou rle mettre dans monID

// monID correspond à un objet
//innerHTMl correspond à une propriété de mon objet
```

```javascript
  monID.innerHTML = 'Test';
  monID.className = "avion";
  monID.style.color = 'red';

```
```javascript

let monID = {
    innerHTML : "Section",
    className : "avion";
}

// équivalent de
monID.innerHTML = 'Test';
monID.className = "avion";

```
```javascript
// boucler sur une liste d'éléments 
  for (i = 0; i < lesP.length; i++) {
      console.log(lesP[i]);
  }

// exemple
  for (i = 0; i < lesP.length; i++) {
    lesP[i].style.color = 'red';
  }

```

# Les modules

Un module est un constructeur d'objets