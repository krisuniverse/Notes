# Factorisation de la requête ajax

## Définition de la méthode makeAjaxRequest
La méthode makeAjaxRequest prend 2 paramètres :
  - l'url
  - le traitement à effectuer lorsque la requête aboutit
    - le traitement est contenu dans une fonction qu'on appelle callback
```js
var app = {
    // init
    // makeAjaxHTMLRequest
    // makeAjaxJSONRequest
    // make SWAPIRequest
    // getPeopleDetailsFromSwapi
    // getPlanetDetailsFromSwapi

  makeAjaxRequest: function (url, doneCallback) {
    $.ajax({
      method: 'GET',
      url, // équivaut à url: url
      dataType: 'json',
      data: null
    })
    .done( doneCallback )
    .fail( function (error) {
      console.error(error);
      alert('erreur durant la requete AJAX vers SWAPI');
    })
  }
}
```
**remarque**
- Callback
  > Un callback est ce qu’on peut traduire par « fonction de retour ». C’est une fonction comme une autre sauf qu’elle est placée en paramètre d’une autre fonction pour être exécutée à un moment précis.
  > [Article sur les callback](https://maxlab.fr/javascript/javascript-methodes-avancees/)


## Appel de la méthode makeAjaxRequest

```js
var app = {
  // init:
  // makeAjaxHTMLRequest:
  // makeAjaxJSONRequest:
  // make SWAPIRequest:

// utilisation dans une méthode qui comporte un paramètre (id)
  getPeopleDetailsFromSWAPI: function (peopleId) {
    function monCallback(response) {

      console.log(response);
      // on veux injecter le nom du personnage dans la div dont l'id est "swapi"
      var monP = $('<p>').text( "Le personnage dont l'id est "+peopleId+" s'appelle "+response.name);

      $('#swapi').append(monP);

    };
    app.makeAjaxRequest(`https://swapi.co/api/people/${peopleId}/`, monCallback);
    
  },

// utilisation dans une méthode qui ne prend pas de paramètre (sans id)
  getPlanetDetailsFromSWAPI: function () {
    function monCallback(response) {
      //console.log(response);
      var monP = $('<p>').text( "La planète dont l'id est 10 s'appelle "+response.name);

      $('#swapi').append(monP);
    };

    app.makeAjaxRequest('https://swapi.co/api/planets/10/', monCallback);
  },

    //makeAjaxRequest: function (url, doneCallback) {}
}
```

# Factorisation de l'extrème

## Étapes

### Étape 0 : Définir le traitement de la réponse (détails du film) à la requête
```js
function filmCallback(film) {
    // instruction à venir
}
```

### Étape 1 : Lancer une requête Ajax en lui passant l'url (du film) et le callback qu'on vient de définir
```js
app.makeAjaxRequest(`https://swapi.co/api/films/${filmId}/`, filmCallback );
```

### Étape 2 : Afficher la liste des planètes
> La réponse à la requête nous renvoie un objet qui a plusieurs propriétés, dont la propriété title 

- Afficher le titre du film dans une balise titre
  ```js
  var title = $('<h3>').text("Les planetes du film "+film.title);
  title.appendTo($('#swapi'));
  ```
- Créer un élément `<ul>` pour y ajouter nos résultats futurs planètes
  ```js
  var monUl = $('<ul>');
  ```

- Définir le traitement du résultat de la requête qui récupère les détails d'une planète donnée (ici afficher le nom de la planète)
  ```js
  function planetCallback (planet) {
    // pour chaque planète listé dans le tableau planet.name, on va ajouter le nom de la planète, dans un <li> (ce <li> sera dans la balise <ul> définie précedemment)
    var newLi = $('<li>').text(planet.name);
    newLi.appendTo(monUl);
  }
  ```    

### Étape 3 : Récupérer les détails sur les planètes (puis les afficher)

La fonction qui gère le traitement (afficher le nom de chaque planète) est définie, il faut maintenant l'utiliser. C'est-à-dire la passer an argument de la méthode makeAjaxRequest :
```js
for (var planet_url of film.planets) {
    app.makeAjaxRequest(planet_url, planetCallback );
}
```
> Pour chaque planète listée dans le tableau `film.planets`, on va appeler la fonction `planetCallback` (i.e mettre le nom de la planète, dans un `<li>` (ce `<li>` sera dans la balise `<ul>` définie précedemment)

### Étape 4 : Ajouter cette liste (qui contient du coup tous les `<li>`) dans le DOM
```js
monUl.appendTo( $('#swapi'));
```

## Code final
```js
var app = {
    // init
    // makeAjaxHTMLRequest
    // makeAjaxJSONRequest
    // make SWAPIRequest
    // getPeopleDetailsFromSwapi
    // getPlanetDetailsFromSwapi

    getPlanetsFromFilm: function(filmId) {

      function filmCallback(film) {

          // Définition de la fonction à executer par la méthode done
          // le callback est passé en argument de la méthode makeAjaxRequest
          var title = $('<h3>').text("Les planetes du film "+film.title);
          title.appendTo($('#swapi'));
    
          var monUl = $('<ul>');
          monUl.appendTo($('#swapi'));

          // 2 - faire une boucle sur les url des planets
          function planetCallback(planet) {
            $('<li>').text(planet.name).appendTo(monUl);
          }
    
          for (var planet_url of film.planets) {
            app.makeAjaxRequest(planet_url, planetCallback);
          }
      };

          app.makeAjaxRequest(`https://swapi.co/api/films/${filmId}/`, filmCallback);

      },

    //makeAjaxRequest: function (url, doneCallback) {}
}
```
