# les attributs data

## Créer un attribut data
Les attributs data sont des attributs de données. Ils permettent d'échanger des données propriétaires entre le HTML et le DOM, qu'on poura manipuler dans le script

```html
<div data-*="ce que je veux"></div>
<!--Le * remplace le nom choisi -->

<div data-champomy="c'est la vie"></div>
```
nav[i].dataset.kiwi
Si je cible l'élément par la class il faut faire 


```html
 <nav id="select-model" class="select-model" data-banne="bannane" data-kiwi="info_associée"></nav>
```

## Cibler un attribut data
```js
var app = {
  init: function() {
  
    let nav = document.getElementByClassName('select-model');

    // i correspond à l'indice de l'élément comportant la class 
    console.log(nav[i].dataset.kiwi);
  }
};
```

```html
 <nav id="select-model" class="select-model" data-banne="bannane" data-kiwi="info_associée"></nav>
```

# setInterval

Appelle une fonction de manière répétée, avec un certain délai fixé entre chaque appel

```html
<script>
    let hauteur = 0;
	function f() {
		hauteur +=5;

		let div = document.getElementById('div');

		div.setAttribute("style","height:" + hauteur + "px");

		console.log(hauteur);

		if(hauteur == 500) clearInterval(timer); // on s'arrete quand la hauteur fera 500px. on aurait pu mettre un bouton qui déclenche le clearInterval.

		}

        let timer = window.setInterval("f()",100); // permet de rappeler une fonction plusieurs fois.
</script>
```
`clearInterval();` arrête l'exécution d'un traitement timer précédemment défini avec setInterval().

Ici , les {} après le if sont optionnelles

On déclare la fonction f() mais on la déclende unqiuement quand on l'appelle 
```js
 let timer = window.setInterval("f()",100);
```

# setTimeout()

Appeler une fonction 1 seul fois au bout d'un temps déterminé. 
C'est un compte à rebours

```js
setTimeout(function(){ alert("Hello"); }, 3000);
```

**Exemple(avec écouteur d'événement)**
```js
let monBouton = document.getElementById('test')

monBouton.addEventListener('click', function { setTimeout() {alert("test");}, 3000) })
```


# lexo

## Objectifs
- Conception un système d’interprétation de matrice simple en JS
- Gestion de différents type de blocs en CSS
- Positionnement des blocs en CSS
- Génération des éléments de navigation en JS

## Pistes techniques
- Encapsulation dans un module
- Boucles imbriquées
- Passage de données en dataset

## Brief
Conception d'une ardoise numérique de représentation en faux pixels, configurable pour afficher un dessin arbitraire :

L'ardoise et les modèles de dessin doivent être séparés (nous voulons pouvoir ajouter de nouveaux modèles sans risquer de « casser » l'ardoise)
Les modèles de dessin doivent être exprimés sous forme de code (dans un fichier JS)
La taille de pixels est configurable
Les types de pixels doivent être stylisables (nous voulons pouvoir changer les couleurs à loisir)
Il est possible de naviguer entre les différents dessins qui seront affichés dans l'ardoise

1. Récupérer les éléments utiles
```js
generateButtons: function() {

    let nav = document.querySelector('#select-model');

}

```
2. Créer les boutons 
- créer les boutons
- ajouter une class
- inscrire la class sur style.css
- créer un data-model
- ajout des boutons à la nav
- appeler la fonction dans init pour l'appeler au chargement de la page

```js
var app = {
  init: function() {

    // on génère la navigation en rapport avec les modeles existants
    app.generateButtons();

  },
  generateButtons: function() {

    let nav = document.querySelector('#select-model');

    // pour chaque model trouvé on créer un bouton
    for (let model in map.models) {
      // création du bouton
      let btn = document.createElement('button');

      // ajout d'une classe
      btn.className = 'select-model-button';

      // ajout d'un dataset "model" pour passer l'info lors du click l'équivalent de data-model ="squid"
      btn.dataset.model = btn.textContent = model;

      // ajout du bouton à la nav
      nav.appendChild(btn);


      // ajout d'un écouteur de click ; au clic on exécute handleLoadModel
      btn.addEventListener('click', app.handleLoadModel);

    }


  }
};

document.addEventListener('DOMContentLoaded', app.init);

```

3. Charger le modèle lors du clic (fonction)

- récupérel le nom du model
- récupérer le modèle à fafficher (currentModel)
- cibler la div #invader et la récupérer dans une variable container
- insérer du vide dans la div 
- attribuer un elargeur à la div en fonction du modèle à afficher

- générer le canva vide avec une boucle for, line coreespond à chaque ligne du tableau au niveau de la clé (ex:squid), etc
- Parcourir les lignes du tableau models[model]
  - pour chaque rang consituant le model 
      - stocker le type de bloc (x, -, etc)
      - créet une div pour chacun des caractères
      - ajouter une class à chacune des div pour 

-

```js
var app = {
  //init : function() {},

  //generateButtons : function() {},

  handleLoadModel: function(evt){

    let modelName = evt.target.dataset.model;

  // stockage du nom du modèle demandé, pour utilisation ultérieure
    let currentModel = map.models[modelName];

    //préparation de l'ardoise
    let container = document.getElementById('invader');
    container.innerHTML = '';
    container.style.width = currentModel[0].length * 20 + 'px';

    // génération de l'ardoise vide
    for (let line = 0; line < currentModel.length; line++) {
      
      for (let column = 0; column < currentModel[line].length; column++) {
        
        // stockage du type de bloc
        let block = currentModel[line][column];

        // création d'un élément DOM pour le pixel
        let square = document.createElement('div');

        // ajout d'une classe .square et d'une classe pour le type de block (nommage BEM)
        square.className = 'square ' + 'square--' + map.types[block];

        // ajout du pixel dans l'ardoise
        container.appendChild(square);

      }

    }

  }

};
```





```js
```

```html
```

```html
```

```html
```