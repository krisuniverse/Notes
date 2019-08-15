Pour utiliser une inteface on utilise le mot-clé `implements`

```php
<?php


namespace App\Models;


use JsonSerializable;

class ListModel extends CoreModel implements JsonSerializable
{
    protected $name,
              $page_order;

    /** Interface Methods */

    /**
     * @return mixed data which can be serialized by <b>json_encode</b>,
     * which is a value of any type other than a resource.
     */
    public function jsonSerialize()
    {
        return array (
            "id"         => $this->getId(),
            "created_at" => $this->getCreatedAt(),
            "updated_at" => $this->getUpdatedAt(),
            "name"       => $this->getName(),
            "page_order" => $this->getPageOrder()
        );
    }
}
```

# les méthodes et propriétés statiques
Les méthodes et propriétés statiques sont __partagées__ par toutes les instances et accessibles diretement à partir du nom de la classe.

# les constantes de classe

## une consante
une constante est une zone mémoire qui change pas de valeur( et le programmeur ne doit pas essayer de le faire ) durant l'exécution d'un programme. donc on peut dire que c'est une information en mode de lecture.

##variable statique
Au sens Orienté objet, une variable statique déclarée dans une classe A est une zone mémoire partagée par tous les objets de type A.
donc tous ces objets peuvent lire/modifier cette variable..

##une donnée statique et constante
c'est une donnée partagée par tous les objets de la classe qui déclare cette donnée mais peut être accéder qu'en mode lecture. c'est à dire aucune objet ne peut modifier cette donnée.

# Les interfaces

une interface est une classe vide qui déclarte des méthodes abstract

le simple fait d'utiliser le mot clé interface, les methodes n'ont plu sbesoin du mot-clé abstract



utilisre une interafce
implements nomDeLInterface

les interfaces permettent de contourner ce pb d'héritage unique

# Les constantes magiques (la suite)

##`::class`
Depuis PHP 5.5, le mot clé class est également utilisé pour la résolution des noms de classes. Vous pouvez récupérer une chaîne contenant le nom qualifié complet de la classe ClassName en utilisant ClassName::class. C'est particulièrement pratique avec les classes utilisant des espaces de noms.


## get_class($this)
Retourne le nom de la classe d'un objet

# Rappel

Utiliser les namespaces et les use
```json
// dans composer.json
"autoload": {
       "psr-4": {"Okanban\\": "app/"}
   }
```

puis dans le terminal faire
```
composer dump-autoload
```

      // autre version, qui pose problème si je passe ma classe en static
      //this n'est plus définit car il fait parti de l'instance del'objet
      //$results = $statement->fetchAll(\PDO::FETCH_CLASS, get_class($this))