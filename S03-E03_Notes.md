# Révisons fonction

```javascript
function maFonction() {
    //instruction
    return "Hello";
}
```

## Renvoyer le code d'une fonction
```javascript
console.log(maFonction);
```

##Executer une fonction
```javascript
console.log(maFonction());
```
Une fonction peut avoir des métadonnées (générées par Javascript lors de la création de la fonction).

Lorsqu'on déclare une fonction on a des propriéts dessus. Ici `name` nous permet d'obtenir le nom de la fonction
```javascript
console.log(maFonction.name)
```


# Le

**remarques**
- Module vs Objet
Le module est un objet qui contient un enseble de propriét et/ou de méthode sur la même thématique 

- Propriété vs Méthode
Une propriété devient une méthode si on lui associe une fonctio anonyme (`function()`)

> "C'est ce que tu mets en face qui définit ce qu'il est"

```javascript

var monModule = {
    maMethode: function() { // ceci est une méthode
        //instruction
    },
    maPropriete: 25;
}
```


```javascript
emprunter //c'est un objet qui retourne la fonction (cf console.log(emprunter))

emprunter()// ma fonction est une valeur

// utiliser en paramètre d'une autre fonction
emprunter(monModule.maMethode);


```
une fonction appelée avec une parenthèse est une  valeur (même utilisation qu'ne varaible) alors qu'ne fonction sans parenthèse c'est un objet (on peut donc appelr ses propriétés)

```javascript

var form = document.getElementById('#form-input')

form.addEventLIstener('submit', function(evt) {
    evt.preventDefault(); // empêcher le reload
    console.log(evt.target.querySelectorAll('.signup-form-input')) // target correspond à la cible de l'evénement, donc le form
})
```

inspecter > console > cocher preserve log (pour conserver ce qui a été tapé dans la console)
```javascript
```
```javascript
```

prenom-nom.vpnuser.oclock.io/