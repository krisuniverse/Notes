# Atelier du 07/08/19

# Partie 1 :  Ajouter une "liste" dans le DOM

## Etape 1 - Formulaire d'ajout

### Plan d'attaque

1. Le formulaire d'ajout d'une liste se trouve dans la fenêtre "modal"
intercepter la soumission de ce formulaire

Pour cela, récupérer l'élément (le formulaire) et lui placer un écouteur d'événement de type submit (clicq sur le bouton submit ou sur la touche entrée)
```js
$('#addListModal form').submit( app.handleAddListFormSubmit );
```

2. Désactiver le fonctionnement par défaut

Dans le handler(methode passé en paramètre de submit), bloquer le rechargement de la page 
```js
event.preventDefault();
```

3. Récupérer la valeur dans l'input du formulaire
    - Solution 1 : utiliser l'id du modal
        ```js
        $("#addListModal .input").val();
        ```

    - Solution 2: via event.target (la cible de l'événement, donc le formulaire)
        ```js
        $(event.target).find('.input').val();
        ```

    - Solution 3 : récupérer l'input via son nom __(la mieux)__
        ```js
        $(event.target).find('.input[name="list-name"]').val();
        ```

4. appeler la méthode app.generateListElement (à créer à l'étape suivante) en donnant la valeur récupérée (de l'input) en paramètre
```js
app.generateListElement(listName);
```

### Résultat
```js
    handleAddListFormSubmit: function (event) {

        event.preventDefault();
        //console.log(event);
        var listName = $(event.target).find('.input[name="list-name"]').val();
        app.generateListElement(listName);

    },
```

**remarque**
- Notez que l’événement submit se déclenche uniquement sur l’élement form, et pas sur les éléments button ou input submit. (Les formulaires sont soumis, pas les boutons.) (source: mdn)
- par défaut, le navigateur appelle le eventlistener avec un événement en paramètre
    - le premier paramètre du handler correspondra toujours à l'événement
    - on peut don cle nommer comme on veut (e, evt, event, carotte)
- html identifie


## Étape 2 : Créer l'élément "liste"

## Plan d'attaque
1. Créer une méthode generateListElement dans app prenant en paramètre listName

cette méthode s'occupe de créer l'élément
```js
var app = {

    // init: function () {},
    // handleAddListFormSubmit: function (event) {},

    generateListElement: function (listName) {
        // instructions à venir
    },
}
```

2. Créer une template de la liste avec `<template>`
```html
<template>
    <!-- Coller la structure HTML d'une liste -->
</template>
```

3. Utiliser les méthodes `.contents()` et `.clone()` pour récupérer le contenu du template et le cloner dans une variable

Ici on veut cloner le contenu de la template, il faut donc faire la méthode `.contents()` avant la méthode `.clone()`

```js
    generateListElement: function (listName) {

        var newList = $('#emptyListTemplate').contents().clone();

    },
```

4. Appliquer les modifications nécessaires (ajout du nom de la liste)
```js
    generateListElement: function (listName) {

        var newList = $('#emptyListTemplate').contents().clone();

        // on modifie le h2 (nom de la liste)
        newList.find('h2').text(listName);
    },
```

5. Retourner l'élément "liste" (le clone mis à jour avec le nom de la liste)
```js
    generateListElement: function (listName) {

        var newList = $('#emptyListTemplate').contents().clone();
        newList.find('h2').text(listName);

        return newList;
    },
```
:warning: attention, cette méthode n'ajoute pas l'élément dans le DOM

## Résultat

```js
var app = {
    // init: function () {},
    // handleAddListFormSubmit: function (event) {},

    generateListElement: function (listName) {

        var newList = $('#emptyListTemplate').contents().clone();
        newList.find('h2').text(listName);

        return newList;
    },
}
```


## Etape 3 : Ajouter l'élément "liste" dans le DOM
```js
var app = {
    // init: function () {},
    handleAddListFormSubmit: function (event) {
        event.preventDefault();

        var listName = $(event.target).find('.input[name="list-name"]').val();

        // on génère une nouvelle liste grace à la méthode prévue pour
        var newListElement = app.generateListElement(listName);

    }
}
```

## Etape 4 : Fermer la fenêtre Modal
```js
var app = {
    // init: function () {},
    handleAddListFormSubmit: function (event) {
            // on génère une nouvelle liste grace à la méthode prévue pour
            var newListElement = app.generateListElement(listName);

            // et on insère cette nouvelle liste dans la div #jeTriche
            $('#jeTriche').append( newListElement );

            // on ferme la modal, en lui enlevant la class "is-active"
            $('#addListModal').removeClass('is-active');
    }
}
```

Autre option pour fermer le modal
```js
$(evt.target).parents('.modal').removeClass('is-active');
```

# Cleange du code

## Bonus de GuiGui la Diva : tester la saisie
```js
    handleAddListFormSubmit: function (event) {
        event.preventDefault();

        var listName = $(event.target).find('.input[name="list-name"]').val();

// tester s'il il a bien une saisie 
        if (listName) { //  test équivalent : if (listname != null && listName.length > 0)
            // on génère une nouvelle liste grace à la méthode prévue pour
            var newListElement = app.generateListElement(listName);

            // et on insère cette nouvelle liste dans la div #jeTriche
            $('#jeTriche').append( newListElement );

            // on ferme la modal, en lui enlevant la class "is-active"
            $('#addListModal').removeClass('is-active');
        }
}
```
## Insérer la liste avant le bouton

```js
            var columnContainingTheButton = $('#addListButton').parent();
            newListElement.insertBefore( columnContainingTheButton );
```


# Partie 2 : Ajouter toutes les listes au chargement du DOM

## Etape 1 : Supprimer les listes existantes au chargement du DOM
1. cibler l'élément contenant toutes les listes
2. vider cet élément
```js
$('#jeTriche').empty();
```

##Etape 2 : Récupérer toutes les listes en AJAX

1. Copier le dossier data

2. Faire la requête AJAX pour récupérer les données contenues dans lists.json
```js
    getListsFromAjax: function () {
        // on fait un appel AJAX vers notre source de données
        $.ajax({
            method: 'GET',
            url: 'data/lists.json',
            dataType: 'json',
            data: null
        }).done( function (response) {

        }).fail( function(error) {
            console.error(error);
            alert('Impossible de charger les listes');
        });
    },
```

3. Stocker la réponse dans une propriété (accécible partout dans l'objet app par la suite)
La propriété n'est crée que si la requête aboutit

```js
  getListsFromAjax: function () {
    // on fait un appel AJAX vers notre source de données
    $.ajax({
        // propriétés
    }).done( function (response) {

      app.lists = response;

    }).fail( 
        // fonction
    });
},

```
##Etape 3 : Parcourir la liste de "list"
```js
  getListsFromAjax: function () {
    // on fait un appel AJAX vers notre source de données
    $.ajax({
        method: 'GET',
        url: 'data/lists.json',
        dataType: 'json',
        data: null
    }).done( function (response) {

      app.lists = response;

    }).fail( function(error) {
        console.error(error);
        alert('Impossible de charger les listes');
    });
},

```

2. Créer une méthode pour ajouter la liste au dom 
elle contient les lignes
```js
  addNewListInDOM: function(newlist) {
    var columnContainingTheButton = $('#addListButton').parent();
    newlist.insertBefore( columnContainingTheButton );
  },

```

Appeler cette méthode dans handleAddListFormSubmit

```js
  handleAddListFormSubmit: function (event) {

      event.preventDefault();

      // Récupérer la saisie de l'utilisateur (titre)
      var listName = $(event.target).find('.input[name="list-name"]').val();

      // Tester s'il y a bien du texte de saisie
      if (listName) { //  équivalent de : if (listname != null && listName.length > 0)
          var newListElement = app.generateListElement(listName);

          // Insérer la nouvelle liste dans la div #jeTriche juste avant le bouton d'ajout
          app.addNewListInDOM(newListElement);

          // Fermer la modal
          $('#addListModal').removeClass('is-active');
      }
  },
```

Et dans le for présent dan sle done de la requête ajax

```js
      for (var list of app.lists) {
        var newListElement = app.generateListElement(list.name);
        app.addNewListInDOM(newListElement);
        }
```
## résulat 
```js
  getListsFromAjax: function () {
    // on fait un appel AJAX vers notre source de données
    $.ajax({
        method: 'GET',
        url: 'data/lists.json',
        dataType: 'json',
        data: null
    }).done( function (response) {

      app.lists = response;

      for (var list of app.lists) {
        var newListElement = app.generateListElement(list.name);
        app.addNewListInDOM(newListElement);
        }

    }).fail( function(error) {
        console.error(error);
        alert('Impossible de charger les listes');
    });
},
```
Ajouter un id à chaque liste
```js
```

## refaire fonction le double-clic qui permet de modifier le titre d'une liste
```js
```


# Bonus

## Le template

créer un template pour la card

## Générer la carte
```js
```


```js
```

```js
```

```js
```