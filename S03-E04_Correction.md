# Étape 1 : récupérer le form et poser un écouteur d'événement

## 1.Récupéréer la div errors, le form login-form et les champs .field-input
Ici on crée une méthode qui créer de spropriétés

```javascript
var app = {
  init: function() {
    
        //Ciblage des éléments du DOM
    app.errorsArea = document.getElementById('errors');
    app.loginForm = document.getElementById('login-form');
    app.fields = document.querySelectorAll('.field-input');

  }
};

document.addEventListener('DOMContentLoaded', app.init);
```


##  2. Écouter les champs
```javascript
var app = {
    init: function() {
      
      //Ciblage des éléments du DOM [...]
    
      // Ecouteur d'événement pour chaque champ
      for (let fieldIndex = 0; fieldIndex < app.fields.length; fieldIndex++)   {
        let field = app.fields[fieldIndex];
        field.addEventListener('blur', app.isInputValid);
      }

    },

    isInputValid: function(evt) {
      let field = evt.target;
    }

};
```


target permet de cibler l'élément sur lequel l'écouteur est posé

element.classList retourne une liste des attributs de classe de l'élément ciblé.
Pour ajouter une class, on procède de la manière suivante :

```javascript
    field.classList.add('valid');
```

Dans notre code, ça donne :
```javascript
var app = {
    //init
        //Ciblage des éléments du DOM
        //Écouteur d'événement pour chaque champ
    // isInputValid

    checkField : function(field) {

        field.className = 'field-input'; // on réinitialise la classe du champ pour s'assurer de pouvoir continuer à tester nos conditions

        if (field.value.length < 3) {
          app.errorsArea.innerHTML = 'Doit contenir au moins 3 caractères';
          field.classList.add('invalid'); // dans le css invalid a pour background-color: #ff3860 (rouge)

          return false;
        }

        field.classList.add('valid'); // dans le css invalid a pour background-color: #00d1b2 (vert)
        return true;

    }
}
```

## 3. Détecter les erreurs

1. On récupère les 2 éléments à vérifier
2. Puis on stock le résulat de la méthode checkField
3. On retourne le résultat du test de la condition


```javascript
var app = {
    //init
        //Ciblage des éléments du DOM
        //Écouteur d'événement pour chaque champ
    //errors : []
    //isInputValid
    //isFormValid
  hasErrors: function() {

    let usernameField = document.getElementById('field-username');
    let passwordField = document.getElementById('field-password');

    let usernameValid = app.checkField(usernameField);
    let passwordValid = app.checkField(passwordField);

    return usernameValid && passwordValid;

  },
  //isInoutValid
  //checkField
}
```

Après la création de hasError, on ajoute une valeur dans le tableau errors (réalisé en étape 3)

```javascript
var app = {
  checkField : function(field) {

    field.className = 'field-input';

    if (field.value.length < 3) { 
    // juste en dessous
      app.errors.push(field.placeholder + ' doit contenir au moins 3 caractèrs');
      field.classList.add('invalid');
      
      return false;
    }

    field.classList.add('valid');
    return true;

  },
}
```
push() permet de rajouter un élément à un tableau (ici errors)

4. On créer la méthode pour vérifier si le formulaire est valide `isFormValid` 
5. On crée la méthode que va effacer les erreurs
6. On crée une méthode qui va afficher les erreurs

```javascript
var app = {
    //init
        //Ciblage des éléments du DOM
        //Écouteur d'événement pour chaque champ

    errors: [], // on déclare une propriété qui contient un tableau vide
    //isInputValid
    isFormValid: function(evt) {

        if(app.hasErrors()) {
          evt.preventDefault();
        }

    },
    //hasErrors
    //checkField
    clearErrors: function() {
        app.errors = [];
        app.errorsArea.innerHTML = '';
    },

    showErrors: function() {
        for (let errorIndex = 0; errorIndex < app.errors.length; errorIndex++) {
        app.errorsArea.innerHTML += "<p class='error'>" + app.errors[errorIndex] + "</p>";
    } 
  }
```


code en entier (vérifier)

```javascript
var app = {
    init: function() {
      
          //Ciblage des éléments du DOM
      app.errorsArea = document.getElementById('errors');
      app.loginForm = document.getElementById('login-form');
      app.fields = document.querySelectorAll('.field-input');

        // Ecouteur d'événement pour chaque champ
        for (let fieldIndex = 0; fieldIndex < app.fields.length; fieldIndex++)   {
            let field = app.fields[fieldIndex];
            field.addEventListener('blur', app.isInputValid);
        }
  
    },
    errors: [], // on déclare une propriété qui contient un tableau vide
    isInputValid: function(evt) {
        let field = evt.target;
    },
    checkField : function(field) {

        field.className = 'field-input'; // on réinitialise la classe du champ pour s'assurer de pouvoir continuer à tester nos conditions
    
        if (field.value.length < 3) { 
          app.errors.push(field.placeholder + ' doit contenir au moins 3 caractèrs');
          field.classList.add('invalid'); // dans le css invalid a pour background-color: #ff3860 (rouge)
          
          return false;
        }
    
        field.classList.add('valid'); // dans le css invalid a pour background-color: #00d1b2 (vert)

        return true;
    
      },
    isFormValid: function(evt) {
        if(app.hasErrors()) {
            evt.preventDefault();
        }
    },
    hasErrors: function() {

        let usernameField = document.getElementById('field-username');
        let passwordField = document.getElementById('field-password');
    
        let usernameValid = app.checkField(usernameField);
        let passwordValid = app.checkField(passwordField);
    
        return usernameValid && passwordValid;
    
    },
    clearErrors: function() {
        app.errors = [];
        app.errorsArea.innerHTML = '';
    },
    showErrors: function() {
        for (let errorIndex = 0; errorIndex < app.errors.length; errorIndex++) {
        app.errorsArea.innerHTML += "<p class='error'>" + app.errors[errorIndex] + "</p>";
        } 
    }
};
document.addEventListener('DOMContentLoaded', app.init);
```
```javascript
```
```javascript
```