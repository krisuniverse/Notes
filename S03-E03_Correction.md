# Exo 4 - Les couleurs

**énoncé**
Tester si la value est une couleur => Il faut que ça commence par un # => Il faut que la longueur fasse 4 (#FFF) ou 7 (#FFFFFF)
Si ce n'est pas une couleur, écrire un message d'erreur.
Si c'est une couleur, on l'ajoute au `<ul>`.
On met le `<li>` dans la couleur de la couleur tapée
On supprime la valeur de l'input à la soumission

## Code de base
```javascript
let exo4 = {
    init: function() {
        // mon code
    },
    // mon code
}
```

## 

## Créer une méthode qui récupère la valeur de l'input
```javascript

    getValue: function() {
        // Je récupére l'input
        let input = document.getElementById('colors-input');

        //Je récupére la valeur de l'input
        return input.value.trim();

    }
```

## Créer un méthode  qui ajoute la couleur à la liste affichée

```javascript
    addColor: function(evt){

        // On arrête le comportement par défaut
        // pour éviter le rechargement de la page
        evt.preventDefault();

        // Je récupére l'input
        let value = exo4.getValue()

        //Test
        if (exo4.testColor(value)) {
            exo4.displayColor(value);
        } else {
            console.log('Ko');
        }


    },
```

## Créer un méthode qui vérifie que c'est une couleur
```javascript
    testColor: function(value) {

        let isColor = true;


        if (!value.indexOf('#') === 0 || (value.length != 4 && value.length != 7)) {
            return false;
        }

``` 

Mais on peut simplifier l'écriture :

On peut mettre les conditions dans des variables, qui renverront donc un bouléen.

On peut également retourner le résultat de la condition
```javascript 

    testColor: function(value) {

        // Est-ce que ça commence par un dièse ?
        let startWithHash = value.indexOf('#') === 0;

        // Est-ce que ça fait 4 ou 7 caractères ?
        let lengthOk = value.length === 4 || value.length === 7;

        return startWithHash && lengthOk;

    }
```

## Créer une fonction qui va colorer l'élément <li>
```javascript
    displayColor: function(color) {

        //Création du li
        let li = document.createElement('li');

        // Puis mettre la valaur de l'input dans ce <li>
        li.textContent = color;

        // Je rajoute de la couleur
        li.style.color = color;

        //Je récupère mon <ul>
        let ul = document.getElementById('colors-list');

        //Enfin on ajoute le li dans ul
        ul.appendChild(li);

    },
```

## Supprimer la valeur de l'input à la soumission


```javascript
    resetInput: function() {
        let input = document.getElementById('colors-input');
        input.value = '';
        input.focus();
    },
```

Appeler la méthode dans la méthode qui ajoute les couleurs `addColor`

```javascript
    exo4.resetInput();
```

## Afficher le message d'erreur
```javascript
    displayError : function(errorMessage){
        let error = document.getElementById('colors-error');
        error.textContent = errorMessage;
    },
```


##
```javascript
```