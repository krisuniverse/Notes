# Autoload

## PHP Standards recommendations
Liste de recommendations pour PHP, alimenté par PHP-FIG
[PSR](https://www.php-fig.org/psr/)

[PSR-4: Autoloader](https://www.php-fig.org/psr/psr-4/)

## `__autoload`
Tente de charger une classe indéfinie
[Autoload](https://www.php.net/manual/fr/function.autoload.php)
:warning: fonctionnalité OBSOLÈTE

## `spl_autoload_register`
Enregistre une fonction en tant qu'implémentation de __autoload()
[spl_autoload_register](https://www.php.net/manual/fr/function.spl-autoload-register.php)

## Les namespace
[Fiche récap](https://github.com/O-clock-Alumni/fiches-recap/blob/master/php/namespaces.md)

1. Créer un namespace (écrire 'linstruction dans le fichier que l'on souhaite "ranger" dans le namespace)
```php
namespace Okanban;
```

### Exemple d'instanciation de classe
```php
// Dans Dispatcher.php
namespace Okanban;

class Dispatcher
{
  public function disBonjour()
  {
    echo "Bonjour";
  }
}

// dans Application.php
require __DIR__.'/Dispatcher.php';
new Okanban\Dispatcher()

```
**remarque**
- l'instruction `namespace` doit être la première du fichier

### Exemple de classe sans namespace
Dans le ficheir Application.php on a spécifié un namespace Okanban. Sauf que la classe AltoRouteur n'appartient pas au namespace Okanban
```php
new \AltoRouter();
```

Quand est on est dans le namespace, plus besoin de spécifier le namespace devant la classe

### Exemple d'héritage
Version 1
```php
namespace Okanban\Controllers;

require_once __DIR__.'/CoreController.php';

class MainController extends CoreController
{
    // instruction
}
```
Version 2
```php
namespace Okanban\Controllers;

require_once __DIR__.'/CoreController.php';

class MainController extends CoreController
{
    // instruction
}
```

On doit spécifier dans quel namespace se trouve CoreController d'où `namespace Okanban\Controllers;`


# Exploiter composer pour créer notre autoload
[Composer - Autoload](https://getcomposer.org/doc/01-basic-usage.md#autoloading)

Dans composer.json ajouter les instructions suivantes
```
    "autoload": {
        "psr-4": {
            "Okanban\\": "app"
        }
    },
```

le premier anti-slash echappe le second

Faire la commande `composer dump-autoload` dans le terminal



Mettre tous les controller dans des namespaces (ils doivent correspondre aux noms des dossiers cf. psr-4)

Dans composer.json : dir que le namespace `Okanban` correspond au dossier `app`

Spoiler de michaël
```php
*use \Okanban\Controllers\{
    MainController,
    ErrorController,
    ListController
};
```

```php
spl_autoload_register(function($class) {
    require_once __DIR__ . DIRECTORY_SEPARATOR . "Controllers" . DIRECTORY_SEPARATOR . $class . ".php";
});
```

Un namespace est un sorte de dossier virtuel dans lequel il est possible de ranger des "fichiers"

l'instcrution namespace doit toujours être ne premier. On définit la lcasse par lasuite. cette classe se trouve donc dans le namespace.

Pour pouvour utiliser cette classe, je dois spécifier au moment de l'instncier dans quel namespace elle se trouve

On peut créer des sous namespace, ces sous-namespace correspondent PARFAITEMENt aux noms des sous dossiers (cf.psr-4)

Si le nomage est respecté,  on peut utiliser:
la fonction spl_auto_register :
```php
spl_autoload_register(function($class) {
    require_once __DIR__ . DIRECTORY_SEPARATOR . "Controllers" . DIRECTORY_SEPARATOR . $class . ".php";
});
```
-  autoload de composer :
```
    "autoload": {
        "psr-4": {
            "Okanban\\": "app"
        }
    },
```
Il suffirat alors de require l'autoload de composer ! Plus besoins de require chaque fichier contenant les
classes.


Utilisation des alias
- Sans alias
```php
require __DIR__.'/../vendor/autoload.php';

use Okanban\Application;

//$baseUri = isset($_SERVER['BASE_URI']) ? $_SERVER['BASE_URI'] : '';
$baseURI = $_SERVER["BASE_URI"] ?? "";

$app = new Okanban\Application($baseURI);
$app->handleRequest();
```

- Avec alias
```php
require __DIR__.'/../vendor/autoload.php';

use Okanban\Application as Application;

//$baseUri = isset($_SERVER['BASE_URI']) ? $_SERVER['BASE_URI'] : '';
$baseURI = $_SERVER["BASE_URI"] ?? "";

$app = new Application($baseURI);
$app->handleRequest();
```



Pour les routes
```php
$match ? $match["target"] = "Okanban\\Controllers\\" . $match["target"] : false;
$dispatcher = new Dispatcher($match, "Okanban\\Controllers\\ErrorController#page404");
```

ou en dur
```php
$this->router->map('GET', '/', 'Okanban\Controllers\MainController#home', 'homepage');
```

# Active record

## Rappel
Jusqu'à maintenant on faisait du data mapping.

Data Mapper :
- un point d'entrer vers la BDD qui s'occupe de mapper les données

## Tester ce qu'on récupéère de la BDD

1. Créer la route 
```php
  $this->router->map('GET', '/test', 'Okanban\Controllers\MainController#test', 'test');
```

Méthode de test
```php
    public function test()
    {
      $test = "Bonjour";
      dump($test);
    }
```

## Mettre ne place les méthodes relatives à la BDD
Dans ListModel.php
```php
    /**
     * Méthodes relatives à SQL
     */

    public function insert()
    {
        // cette méthode insère l'objet courant (donc $this) dans la table correspondante en BDD.
    }

    public function find($id)
    {
        // cette méthode renvoie une instance de ListModel, récupérée dans la BDD. Il s'agira de l'instance qui possède l'id passé en paramètre.
    }

    public function update()
    {
        // cette méthode va mettre à jour les données de la BDD, à partir des informations de l'objet courant ($this).
    }

    public function delete()
    {
      // cette méthode supprime l'objet courant de la BDD
    }

    public function findAll()
    {
      // cette méthode renvoie un tableau, qui contient des instances de ListModel, représentant toutes listes dans la BDD.
    }
```

### Récupérer l'id créer automtiquement lors des requêtes d'insertion
```php
        // on récupère l'id que SQL vient de générer pour cette ligne ...
        $leDernierIdInsere = $pdo->lastInsertId();
        // ... et on l'enregistre en tant qu'id de l'objet courant
        $this->setId($leDernierIdInsere);
```