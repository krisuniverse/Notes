# 1. Client vs Serveur

**Client**

- c'est le navigateur
- HTML : contenu
- CSS : présentation
- Javascript : Traitements


**Serveur**

Un serveur est un programme qui interprète ma requête http et me renvoie une réponse


**Comment ça marche ?**
1. le client demande la page au serveur
2. Le serveur réceptionne la requête puis génère la page HTML demandée
3.  Le serveur envoie la page HTML générée au client
4.  Du code javascript est généré est exécuté par le navigateur du client pour modifier la page HTML


# 2. Programmer et décomposer

**Qu'est ce qu'un programme ?**

Une suite d'instructions ayant pour but de réaliser une action


**Le principe**

- langage de programmation
- entrée(input ou requête)
- traitement
    - langage contient des restrictions (fonctions, variables, boucles, etc)
    - décomposer le besoin en plusieurs commandes simples et compréhensibles sous forme d'instructions
- sortie (output ou réponse


# 3. PHP

## 3.1 Intro
PHP signifie PHP : Hypertext Preprocessor

**Les avantages de PHP**

- langage le plus rapide en terme d'excution, à l'heure actuelle
- langage opensource
- langage souple et flexible

**Remarques**
Sur le terminal, la commande `php -a` permet de faire des test sans recharger sa page web


## 3.2 La syntaxe

### 3.2.1 La syntaxe générale

Toute instruction se termine par un point-virgule `;`

Le point `.` permet de concatener une chaîne de caractères avec un autre type de données

```php
$fruit = 'citron';
echo 'ceci est un ' . $fruit; // affiche ceci est un citron
```


**Les simple et double quotes**

La différence entre le `'simple quote'` et `"double quote"`,c'est que les `"double quotes"` peuvent afficher les variables
```php
echo 'ceci est un $fruit' ; // affiche ceci est un $fruit
echo "ceci est un $fruit"; // affiche ceci est un citron
```

**Remarques**
- Les double quote évitent d'avoir des problèmes sur des chaines de caractères lorsqu'il y a un mot avec une apostrophe.Car si on utilise une `'simple quote'`, PHP croit que l'instruction se termine. Ainsi, si on utilise `'simple quote'` on doit échapper l'apostrophe (le précéder d'un \ )

**Les types de données (primaires)**
- les chaînes de cracatères (string) : texte
- les entiers (integer) : les entiers
- les flottants (float) : les nombres à virgule
- les booléens (booleans) : true ou false, 1 ou 0

Il existre d'autres types que l'on abodera plus tard : tableau, fonction, objetcs, etc


### 3.2.2 La commande echo
Cette commande permet d'afficher à l'écran ce qui est appelé
```php
echo 'hello world';
echo $maVariable;
```

### 3.2.3 Les variables

**Les types de données primaires**
- les variables doivent suivre la syntaxe camelCase
- donner un nom explicit
- éviter les chiffres, les caractères accentueés et spéciaux
- écrire les noms en anglais


**Assigner une valeur à une variable**
- chaîne de caractères
    ```php
    $maVariable = 'hello world';
    ```
- entier
    ```php
    $leChiffre = 42;
    ```

- flottant
    ```php
    $chiffreVirgule = 78.99;
    ```

**Modulo**

Le modulo permet de déterminer le reste d'une opération 
```php
echo 20 % 2 // modulo 0
echo 20 % 3 // modulo 2 (20-18=2)

```


**Obtenir des informations sur une variable**

`var_dump` affiche les informations d'une variable, comme son type et sa valeur
```php
var_dump($chiffreVirgule); // affiche float(78.99)
```

`print_r` affiche les données mais sans en afficher la nature
```php
print_r($chiffreVirgule); // affiche 78.99
```


# Les conditions

## Cas simple : les booléens
La structure de contrôle `if` va vérifier si la condition est `true`
```php
<?php
$condition = true;

if ($condition) {
	echo "Bonjour !";
}
```

## Car réel : Les comparaisons

**Le test avec `if`**
```php
<?php

$age = 21;

if ($age >= 18) {
    echo "Vous êtes majeur";
}
```

**Le test avec `if...else`**
```php
<?php

$age = 21;

if ($age >= 18) {
    echo "Vous êtes majeur";
}
else {
    echo "Vous êtes mineur";
}
```

**Le test avec `if/else et else if`**
```php
<?php

$age = 16;

if ($age == 16) {
    echo "Notification : Vous êtes en âge de commencer la conduite accompagnée";
}
else if ($age >= 18) {
    echo "Vous pouvez passer le permis";
} else if ($age >= 90) {
    echo "Notification: Merci d'efectuer un examen de révision";
} else {
    echo "Je ne rentre dans aucun de ces cas";
}
```

## Les opérateurs de comparaison
[Fiche récap sur les opérateurs](https://github.com/O-clock-Alumni/fiches-recap/blob/master/php/conditions.md#cas-r%C3%A9el--les-comparaisons)

- `<` : inférieur à 
    - Exemple : `10 < 20` renvoie `true`

- `>` : supérieur à
    - Exemple : 40.5 > 50 renvoie `false` _Attention : 40 > 40 renvoie `false` !_

- `<=` : inférieur ou égal à
    - Exemple : 142 <= 31 renvoie `false`

- `>=` : supérieur ou égal à
    - Exemple : 40 >= 35 renvoie `true` _Cette fois-ci : 40 >= 40 renvoie `true` !_
 
- `==` : égal à
    - Exemple : 40 == 39.999 renvoie `false`
 
- `!=` : différent de
    - Exemple : 40 != 39.999 renvoie `true`

- `!` : "not", c'est-à-dire, l'inverse
    - Exemple : !`true` renvoie false
    - Exemple : !(20 < 10) renvoie `true`


## Les opérateurs logiques

### l'oéparteur logique OU
le `OU` logique s'écrit de ces façons : `OR` ou `||`
Le code est executé si _au moins_ l'une des conditions est vraie
```php
<?php
// Renvoie false
false || false;

// Renvoie true
true || false;

// Renvoie true
false || true;

// Renvoie true
true || true;
```

### L'opérateur logique ET
L'opérateur logique ET s'écrit de ces façons : `AND` ou `&&`
Le code est exécuté lorsque _les 2_ conditions sont vraies
```php
<?php
// Renvoie false
false && false;

// Renvoie false
true && false;

// Renvoie false
false && true;

// Renvoie true
true && true;
```


# Ressources
```php
```

```
```


# Raccourcis
- F12 : ouvrir la console sur Google Chrome
- CTRL + MAJ + T : ouvrir un autre terminal
- CTRL + C : quitter `php -a`

