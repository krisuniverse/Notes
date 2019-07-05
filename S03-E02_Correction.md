
#Rappels

`Math.floor`
> math est un module et floor est une fonction

## Le DOM

- API
- interface entre le html et javascript


## Cibler un objet
document.getElementById('')
document.getElementByClassName('')
document.querySelector('')

## Module

#Correction

```javascript
var app = {
  init: function () {
    console.log('app.init');

    
  }
};
document.addEventListener('DOMContentLoaded', app.init);
```
Une fois que la page est chargée (événement: DOMContentLoaded), tu déclanches app.init (app point la méthode init)

Pour intéragir avec un élément de sa page, il faut qu'il soit chargé. Donc pour éviter les erreurs on fait le code ci-dessus

## Étape 1 et 2

```javascript
let app = {
  init: function () {
    console.log('app.init');

    let lareponsedelafonction = app.askQuestion(questions[0]);
    console.log(lareponsedelafonction);
    
  },
  // création de la fonction askQuestion
  askQuestion: function(questionToAsk) {
    let reponse = window.prompt(questionToAsk);
    return reponse;
  },

};
```
## Étape 3

Mettre `checkResponse()` à la suite des autres modules
```javascript
let app = {
      init: function () {
    console.log('app.init');

    let response = app.askQuestion(questions[0]);
    console.log(response);

    let isCorrect = app.checkResponse(0, response);

    if (isCorrect) {
      
    } else {

    }

    
  },
//...
  checkResponse : function(questionId, userResponse) {

    // Récupérer la réponse attendue pour la question posée
    let rightresponse = responses[questionId];

    // Comparer la réponse atendue avec la réponse effectuée
    if (userResponse == rightresponse) {
      //retourner vroi si la réponse est correcte
      return true;
    } else {
      return false;    
    }

  }
}
```

En gros, ce qui sera retourné par nos fonctions sera récupéré dans des variable, qu'on placera dans init 

##Étape 4 - Modification du DOM
```javascript
    // afficher dans la console "exact" ou "mauvaise réponse"
    if (isCorrect) {
      //console.log('exact');
      // On clible l'élément <ul> listant les réponses correctes
      let ulResponseElement = document.querySelector('#right .responses');

      // On ajoute das son innerHTML le nouveau <li>
      ulResponseElement.innerHTML += '<li>' + questions[0] + '</li>'; 

    } else {
      //console.log('mauvaise réponse');
      // On clible l'élément <ul> listant les réponses correctes
      let ulResponseElement = document.querySelector('#wrong .responses');

      // On ajoute das son innerHTML le nouveau <li>
      ulResponseElement.innerHTML += '<li>' + questions[0] + '</li>'; 
    }
```

##Étape 5
```javascript
 playQuiz : function() {
    //On commence par vider les réponses actuelles
    document.querySelector('#right .responses').innerHTML = '';
    document.querySelector('#wrong .responses').innerHTML = '';

    //Cette méthode boucle sur le tableau de question
    for (let currentQuestionId in questions) {

      // au chargement du DOM, appeler cette méthode avec la première question du fichier `js/questions.js`
      let response = app.askQuestion(questions[currentQuestionId]);
      console.log(response);

      // appeler cette métjode 'checkResponse' après avoir récupérer la réponse de l'internaute pour la première question
      let isCorrect = app.checkResponse(currentQuestionId, response);

      // afficher dans la console "exact" ou "mauvaise réponse"
      if (isCorrect) {
        //console.log('exact');
        // On clible l'élément <ul> listant les réponses correctes
        let ulResponseElement = document.querySelector('#right .responses');

        // On ajoute das son innerHTML le nouveau <li>
        ulResponseElement.innerHTML += '<li>' + questions[currentQuestionId] + '</li>'; 

      } else {
        //console.log('mauvaise réponse');
        // On clible l'élément <ul> listant les réponses correctes
        let ulResponseElement = document.querySelector('#wrong .responses');

        // On ajoute das son innerHTML le nouveau <li>
        ulResponseElement.innerHTML += '<li>' + questions[currentQuestionId] + '</li>'; 
      }

    }

  },
```
**remarque**
Si je veux cibler plusieurs éléments de la me class il faut utiliser `querySelectorAll`, pour récupére r les éléments il faut systématiquement utilisé une boucle

# Bonus

```javascript
let app = {
  rightAnswers: 0,
  wrongAnswers: 0,
  //..
  playQuiz : function() {
    if (isCorrect) {
        //...

        //On incrémente le compteur
        app.rightAnswers += 1;

        // On ajoute das son innerHTML le nouveau <li>
        ulResponseElement.innerHTML += '<li>' + questions[currentQuestionId] + '</li>'; 

    } else {
        //...

        //On incrémente le compteur
        app.wrongAnswers += 1;

        // On ajoute das son innerHTML le nouveau <li>
        ulResponseElement.innerHTML += '<li>' + questions[currentQuestionId] + '</li>'; 
    }
  }
    document.querySelector('#right h2').textContent += ' (' + app.rightAnswers + ')';
    document.querySelector('#wrong h2').textContent += ' (' + app.wrongAnswers + ')';
  //...
}
```

```javascript

```

```javascript
```

```javascript
```
```javascript
```
