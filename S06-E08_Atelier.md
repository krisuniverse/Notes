# Fonctionnalité 1 : Ajouter une liste

## Plan d'attaque
1. Créer la route côté BACK
2. Créer la méthode associée
3. Faire la requête AJAX côté FRONT

## Côté Back
1. Créer la route dans `Application.php`
2. Créer la méthode d'ajout de liste `addList()`
```php

    public function addList()
    {
        // si listName existe, je "trime" la valeur reçue (suppression des espaces en début et fin)
        $listname = isset( $_POST['listName'] ) ?  trim($_POST['listName']) : null ;
        
        // Vérifier qu'on réçoit bien une valeur 
        if ($listname != null && strlen($listname) > 0 ) {

            $newList = new ListModel();
            $newList->setName($listname);
            $newList->insert();

            // Signaler au client (personne qui fait l'appel) que l'insertion a eu lieu
            $this->showJSON(
                array(
                    'success' => true,
                    'error' => ''
                )
            );

        } else {
            // Signaler au client que l'insertion n'a pas eu lieu
            $this->showJSON(
                array(
                'success' => false,
                'error' => 'Missing listName parameter.'
                )
            );
    
        }
        
    }
```

## Côté Front
1. 

Faire l'appel AJAX (ajout de la lsite en BDD) :
- avant la génération de liste `generateListElement()` et l'ajout de la liste dans le DOM `addNewListInDOM()`côté Front
- après la vérifcation du nom saisie 

Dans cette requête AJAX :
- vérifier si l'ajout a eu lieu grâce à `success`, propriété de l'objet renvoyé par le Back via showJSON dans ListController

```js
    handleAddListFormSubmit: function (event) {
        event.preventDefault();
        console.log(event);

        var listName = $(event.target).find('.input[name="list-name"]').val();

        // Vérifier si le nom fourni est vide
        if (listName) { //  test équivalent : if (listname != null && listName.length > 0)
        
            // Appel AJAX
            $.ajax({
                method: 'POST',
                url: 'http://api.okanban.local/lists/add',
                dataType: 'json',
                data: {listName}

            }).done( function (response) {
                console.log(response);

                if (response.success) {
                    // Générer la liste puis l'ajouter au DOM
                    var newListElement = app.generateListElement(listName);
                    app.addNewListInDOM(newListElement);
                } else {
                    alert(response.error);
                }

            }).fail( function (error) {
                console.error(error);
                alert("Impossible d'ajouter la liste !");
            });

            // fermer la modal
            $('#addListModal').removeClass('is-active');
        } else {
            alert('Veuillez saisir un nom de liste')
        }
    },
```

# Fonctionnalité 2 : Supprimer une carte

## Côté Back
1. Créer la route dans `Application.php`

```php
$this->router->map('GET|POST', '/cards/[i:cardId]/delete', 'Okanban\Controllers\CardController#deleteCard', 'delete_card');
```

2. Créer la méthode d'ajout de liste `deleteCard()`
```php
```

## Côté Front
1. Dans index.html, ajouter la classe `deleteButton` dans la `<a>` 
```html
    <template id="emptyCardTemplate">
            <div class="box">
                    <div class="columns">
                        <div class="column card-text">
                            
                        </div>
                        <div class="column is-narrow">
                            <a href="#">
                                <span class="icon is-small has-text-primary">
                                    <i class="fas fa-pencil-alt"></i>
                                </span>
                            </a>
                            <!-- Juste en dessous -->
                            <a href="#" class="deleteButton">
                                <span class="icon is-small has-text-danger">
                                    <i class="fas fa-trash-alt"></i>
                                </span>
                            </a>
                        </div>
                    </div>
               
```
2. Ajouter un id comprenant  l'id de la carte
```js
    generateCardElement: function (cardText, cardId) {
        // copier le contenu de la template et le cloner
        var newCard = $('#emptyCardTemplate').contents().clone();
        
        // modifier le text de la carte
        newCard.find('.card-text').text(cardText);

        // ajouter un id à la carte
        newCard.attr('id', 'card_'+cardId);
        // mettre un écouteur dévénement au bouton supprimer
        newCard.find('.deleteButton').click(app.handleCardDelete);

        return newCard;
    },
```
```js
```

```php
```
**remarques**
- `GET|POST` permet de tester sa route (dump et compagnie fonctionnent à nouveau)
```php
$this->router->map('GET|POST', '/cards/[i:cardId]/delete', 'Okanban\Controllers\CardController#deleteCard', 'delete_card');
```
- AltoDispatcher permet de récupérer les param passé en id de la route en paramètre de la méthode appelée
```php
maMethode($idPasséEnParam)
```

AltoDisptacher utilise array_values et l'opérateur de décomposition pour nous permettre de récupérer le param de la route via la méthode (liée à la route) 
array_values
opérateur de décomposition `...`
retourne les éléments d'un tableau sous forme d'argument

```php
$monTableau = array('1', '2', '3');
print_r ($montableau);
print_r(...$monTableau);
```
# Fonctionnalité 3 : Modifier le titre d'une liste

## Côté Back
1. Créer la route dans `Application.php`
```php
$this->router->map('POST', '/lists/[i:listId]/update', 'Okanban\Controllers\ListController#updateList', 'update_list');
```
2. Créer la méthode d'ajout de liste `updateList()`
```php
```
## Côté Front


# 
```
.closest(".column[id^='list_']");
```

# organiser son code

