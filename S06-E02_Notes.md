# Traduire le code en jQuery

## Lexique


## Résultat
```js
var app = {
  init: function() {
    console.log('init');

    // ajout de la getion de l'vent click sur le bouton d'ajout de liste
    $('#addListButton').click(app.displayAddListModal);

    // Récupration de l'élément Modal pour ajouter une liste
    var addListModalElement = $('#addListModal');

    // Cibler tous les boutons de fermeture du modal
    var closingButtons = addListModalElement.find('.close');

    // Pour chaque bouton
    closingButtons.each(function(index, currentButtonElement) {

      $(currentButtonElement).click(function() {
        addListModalElement.removeClass('is-active');
      });

    });

    $('.column h2').dblclick(app.displayChangeListNameForm);
  },

  displayAddListModal: function(evt) {
    // Récupration de l'élément Modal + ajout de la classe active
    $('#addListModal').addClass('is-active');
  },
}
```

## étape 2
l'événement double click `dblclick`

pour 
le sélecteur o n prend les h2 qui sont dans des colonnes 


## étape 3

1. Ajouter une div.column
```js
```
2. Ajouter un boutton dans la div.column avec les bones classes et id
```js

```
3. Dans ce bouton, mettre un span
```js
``` 
4.  Ajouter le bouton au dom
```js
```

```js
```

**remarque**
- espace insécable `&nbsp;`