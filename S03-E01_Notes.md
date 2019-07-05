# Introduction

## Ouvrir la console
Inspecteur > Console

## Trucs utiles
document.//instruction

Écrire sur son document 
```javascript
document.write("<h1>Entrainement</h1>");
```
isNAN()
```javascript
```

permet de déterminer s'il s'agiit d'un `number`
## Debugguer mon code
[Infos supplémentaires](https://developer.mozilla.org/fr/docs/Web/API/Console)

```javascript
console.log("maVariable");
```

équivalent de `var_dump()` en php

Copnvention de langage
- camelCase
- constante en majuscule

#Les variables

## Déclarer une variable

```javascript
let maVariable; // maVariable stocke la valeur undefined

let maVariable = 10; 

let a = 10, b = 5, c = 2;
```
**Remarque**
Le point-virgule n'est pas obligatoir en Javascript, il est utilisé pour rendre le code plus lisible


# La concaténation

```javascript
var nom = "world";
var message = "Hello " + nom;

message += "!"; // la variable message contien désormais "Hello world!"
```

# Types de variables

## Vérifier le type de ma variable
```javascript
typeof maVariable ;
```

## Number (int et float)
```javascript
var age = 18;
var salaireHoraire = 10.53;
```
## Boolean
```javascript
var aSonPermis = true;
var voitureDisponible = false;
```

## String
```javascript
var maChaineDoubleQuotes = "Chaine de caractères entre double quotes \"\" ";
```

## Array
```javascript
```

# les opérateurs arithmétiques
+, -, *, /, 
```javascript
1 + 1;
10 / 5 
1 * 2 
666 - 42 
10 % 4 // retourne 2
25 * (4 + 10)
```

# Les conditions

## Condition `if`

### if
L'instruction est exécutée si la condition est `true`
```javascript
if (/*condition*/) {
    // instruction
}
```
### if...else
```javascript
if (/*condition*/) {
  // instructions si condition vérifiée
}
else {
  // instructions si condition non vérifiée
}
```

# Les tableaux

`monTableau.length` : renvoie la taille du tableau (similaire à count() en php)

# Les objets

```javascript
let fruits = {
  superbon : "cerise",
  sucre : "banane",
  acide : "kiwi"
  //
};
```

# Fiches recap
[Conditions](https://github.com/O-clock-Alumni/fiches-recap/blob/master/js/conditions.md)

[Syntaxe](https://github.com/O-clock-Alumni/fiches-recap/blob/master/js/syntaxe.md)

[]
```javascript
```
```javascript
```


```html
```
```css
```
```javascript
```

git init

git add READ.md

git status