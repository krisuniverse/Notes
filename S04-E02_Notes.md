[les fonctions PHP](https://github.com/O-clock-Alumni/fiches-recap/blob/master/php/fonctions.md)

[fiche récap](https://github.com/O-clock-Alumni/fiches-recap/blob/master/php/programmation-objet.md)

# POO

## Vocabulaire

classe d'objet : catégorie d'object

instance : un objet créé par une classe


`public` permet de préciser si la méthode ou la propriété peut être récupéré à l'extérieur de la classe ou non

`private`



Les propriétés commence par un `$`


## Les class
```php
class Person {
  public $name;
  public $birthdate;
  public $gender;
  public $weight;
}
```
Créer une instance
```php
$instance = new Person();
```

Remplir une instance
```php
$instance->name = 'Amy';
$instance->birthdate = '29011995';
$instance->gender = 'queen';
$instance->weight = 0;
```

Accéder à une propriété de l'instance en cours de création avec `$this`
```php

class Person {
  //propriétés
  public $name;
  private $birthdate; 
  public $gender;
  public $weight;

// ici $name, $birthday, etc sont les valeurs. on aurait pu les nommer différemment $nom $ naissance
  function __construct($name, $birthdate, $gender, $weight) {
    $this->name = $name;
    $this->birthdate = strtotime($name);
    $this->name = $name;
    $this->name = $name;
  }

  function getBirthdate() {
    return date('d/m/y', $this->birthdate);
  }
}
```

**remarque**

public, class sont des mots clés et non pas des fonctions


Convertir une date en timestamp
```php
strtotime("01/29/1995"); // m/d/y

```

Accéder à une proriété privée
```php

$amy = new Person ('Amy', '01/29/1995', 'f', 65);
$amy->birthdate // renvoie false


// la fonction getBirthdate() est un getter 
$amy->getBirthdate()
```

Exercice : Modéliser un compte bancaire


```php
```

```php
```