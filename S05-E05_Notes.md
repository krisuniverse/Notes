#MCD

```
BRAND: name, updatedAt, createdAt
made, 1N BRAND, 11 PRODUCT
PRODUCT: name, description, picture, price, updatedAt, createdAt
belongs to, 11 PRODUCT, 0N CATEGORY
CATEGORY: name, picture, subtitle, updatedAt, createdAt

is a, 11 PRODUCT, 0N TYPE
TYPE: name, updatedAt, createdAt
```
# Dictionnaire de données

## Product

|Champ|Type|Spécificité|Description|
|-|-|-|-|
|id|INT(10)|PRIMARY KEY, NOT NULL, UNSIGNED, AUTO_INCREMENT|L'identifiant de notre produit|
|name|VARCHAR(64)|NOT NULL|Le nom du produit|
|price|DECIMAL(10,2)|NOT NULL|Le prix du produit|
|createdAt |TIMESTAMP|CURRENT_TIMESTAMP|Date de création du produit |
|picture|VARCHAR(128)|NULL|L'URL de l'image du produit|
|brand_id|INT(10)|FOREIGN KEY, UNSIGNED, NOT NULL|Contient l'id de la marque de ce produit|
| | | | |

**remarques**
price : 10 CHIFFRES AU TOTAL DONC 2 APRÈS L VIRGULE
DBA data base administrator
entity: object qui représente 1 ligne dans la BDD


## Brand
|Champ|Type|Spécificité|Description|
|-|-|-|-|
|id|INT(10)|PRIMARY KEY, NOT NULL, UNSIGNED, AUTO_INCREMENT|L'identifiant de la marque|
| | | | |
**remarques**
- footer_order : ordre d'affichage des marques dans le footer
- si = 0 on ne fait pas apparaitre la marque
## Category

|Champ|Type|Spécificité|Description|
|-|-|-|-|
|id|INT(10)|PRIMARY KEY, NOT NULL, UNSIGNED, AUTO_INCREMENT|L'identifiant de notre produit|
| | | | |
**remarque**
- home_order 
- nous permet d'afficher les catégorie dans un ordre précis
- si = 0, il n'apparait pas su rla page d'accueil
- si ce champs est égale à 0 on affiche pas la catégorie sinon on affiche (dans l'ordre home_order)
## Type
|Champ|Type|Spécificité|Description|
|-|-|-|-|
|id|INT(10)|PRIMARY KEY, NOT NULL, UNSIGNED, AUTO_INCREMENT|L'identifiant de notre produit|
| | | | |
| | | | |

# Ressources
[PHPmyadmin](https://github.com/O-clock-Alumni/fiches-recap/blob/master/bdd/phpmyadmin.md)

# Importer la bdd

1. créer un utilisateur (oshop, mdp : oshop)
2. aller dans l'onglet sql ou import
- sql : coller le contenu du fichier d'import
- import : importer le fichier


# les jointures
[Doc sur les jointures](https://sql.sh/cours/jointures)
[Inofgraphie sur le sjointures](https://sql.sh/2401-sql-join-infographie)

```sql
SELECT * FROM product
JOIN brand
    ON brand.id = product.brand_id
WHERE product.id = 1
```

Pour chaque produit, on va associer la marque grâce à l'id de la marque

> récupérer les produit associé à leur marques

en récuprant l'id de la marque dans la table des produits et en lui spécifiant que l'id de la marque (dans la table produit) est égale à l'id de la marque dans la table brand
je lui spécifie en plus que l'id du produit 

Depuis notre table (`SELECT * FROM product`) on ajoute (`JOIN brand`) à cette condition (`ON brand.id = product.brand_id
WHERE product.id = 1`)


# Model

1. Créer un dossier Model

Créer un fichier pour chaque classe, elle nous permettrons de "transformer" nos données (des tableaux) en object

**le cheminement**
- Créer les propriétés (elles correspondent aux colonnes)
- Créer les getters (car les propriétés sont privées)
- Créer les setters (pour modifier les propriétes)

```php
<?php


class Brand 
{
    private $id;
    private $name;
    private $footer_order;
    private $created_at;
    private $updated_at;

    /**
     * Getters
     */ 
    public function getId()
    {
        return $this->id;
    }
 
    public function getName()
    {
        return $this->name;
    }

    public function getFooter_order()
    {
        return $this->footer_order;
    }

    public function getCreated_at()
    {
        return $this->created_at;
    }

    public function getUpdated_at()
    {
        return $this->updated_at;
    }

    /**
     * Setters
     */ 

    public function setName($name)
    {
        $this->name = $name;

        return $this;
    }

    public function setFooter_order($footer_order)
    {
        $this->footer_order = $footer_order;

        return $this;
    }

    public function setUpdated_at($updated_at)
    {
        $this->updated_at = $updated_at;

        return $this;
    }
}
```


# Gestion des clés étrangères (Product.php)


# lectures suppl.
[héritage](https://github.com/O-clock-Alumni/fiches-recap/blob/master/php/heritage.md)

# Hors-cours

## 

Créer une class qui va représenter l'application `App.php` dans le dossier `App`

Dans index.php :
```php
// Autoload permet de charger automatiquement toutes les classes présentes dans le dossier vendor
require_once __DIR__ . '/../vendor/autoload.php';
require_once __DIR__ . '/../App/App.php';

// instancier
$app = new App($_SERVER['BASE_URI']);
```

Dans App.php
```php
// On importe les fichiers qui décrivent les classes des controleurs
require_once __DIR__ . '/../App/Controller/MainController.php';
require_once __DIR__ . '/../App/Controller/CatalogController.php';
require_once __DIR__ . '/../App/Controller/CartController.php';

class App
{
    private $router;

    public function __construct($baseUri) {
        $this->router = new AltoRouter();
        $this->router->setBasePath($baseUri);
        $this->initRouter();
    }

    // gestion de la requête en cours
    public function handlerequest() {
        $match = $this->router->match();
        if($match !== false) {
            
            $nomDuControlleur = $match['target']['controller'];
            $nomDeLaMethode = $match['target']['methode'];
            $parametresDeLaRoute = $match['params'];
            $controller = new $nomDuControlleur();
            $controller->$nomDeLaMethode($parametresDeLaRoute);

        } else {
            echo "Page not found";
        }
    }

    // définition des routes
    private function initRouter() {
                $this->router->map(
            'GET', 
            '/', 
            array(
                'controller' => 'MainController', 
                'methode' => 'home'
            ), 
            'homepage'
        );
        
        $this->router->map(
            'GET', 
            '/mentions-legales',  
            array(
                'controller' => 'MainController', 
                'methode' => 'legalMentions'
            ), 
            'legal-mentions'
        );
        
        $this->router->map(
            'GET',
            '/catalogue/categorie/[i:categoryId]',
            array(
                'controller' => 'CatalogController', 
                'methode' => 'category'
            ),
            'catalogue-category'
        );
        
        $this->router->map(
            'GET',
            '/panier',
            array(
                'controller' => 'CartController', 
                'methode' => 'cart'
            ),
            'cart'
        );
    }

}
```

Dans index.php :
```php
// Autoload permet de charger automatiquement toutes les classes présentes dans le dossier vendor
require_once __DIR__ . '/../vendor/autoload.php';
require_once __DIR__ . '/../App/App.php';

// instancier
$app = new App($_SERVER['BASE_URI']);
$app->handleRequest();
```
##Moteur de template
Dans le dossier App
```php

class TemplateEngine
{
    

    public function show($templateName, $templateVars = array()) {
        include(__DIR__ . '/../views/header.tpl.php');
        include(__DIR__ . '/../views/' . $templateName . '.tpl.php');
        include(__DIR__ . '/../views/footer.tpl.php');
    }
}

```

Dans les controlleurs 

```php
class CartController
{
    private $templateEngine;

    public function __construct($templateEngine) {
        $this->templateEngine = $templateEngine;
    }

    public function cart() {
        $this->templateEngine->show('cart');
    }
}
```

dans App.pĥp

```php
// On importe les fichiers qui décrivent les classes des controleurs
require_once __DIR__ . '/Controller/MainController.php';
require_once __DIR__ . '/Controller/CatalogController.php';
require_once __DIR__ . '/Controller/CartController.php';
require_once __DIR__ . '/TemplateEngine.php';

class App
{
    private $router;

    private $templateEngine;

    public function __construct($baseUri) {
        $this->router = new AltoRouter();
        $this->templateEngine = new TemplateEngine();
        // dans mon cas TemplateEngine($router,$_SERVER['BASE_URI]);
        $this->router->setBasePath($baseUri);
        $this->initRouter();
    }

    private function initRouter() {
        $this->router->map(
            'GET', 
            '/', 
            array(
                'controller' => 'MainController', 
                'methode' => 'home'
            ), 
            'homepage'
        );
        
        $this->router->map(
            'GET', 
            '/mentions-legales',  
            array(
                'controller' => 'MainController', 
                'methode' => 'legalMentions'
            ), 
            'legal-mentions'
        );
        
        $this->router->map(
            'GET',
            '/catalogue/categorie/[i:categoryId]',
            array(
                'controller' => 'CatalogController', 
                'methode' => 'category'
            ),
            'catalogue-category'
        );
        
        $this->router->map(
            'GET',
            '/panier',
            array(
                'controller' => 'CartController', 
                'methode' => 'cart'
            ),
            'cart'
        );
    }

    public function handleRequest() {
        $match = $this->router->match();
        if($match !== false) {
            
            $nomDuControlleur = $match['target']['controller'];
            $nomDeLaMethode = $match['target']['methode'];
            $parametresDeLaRoute = $match['params'];

            // On instancie le controleur
            // Le controlleur il a besoin du moteur de template
            // Donc on va lui filer
            $controller = new $nomDuControlleur($this->templateEngine);

            $controller->$nomDeLaMethode($parametresDeLaRoute);

        } else {
            echo "Page not found";
        }
    }
}
```

Dans index.php :
```php
// Autoload permet de charger automatiquement toutes les classes présentes dans le dossier vendor
require_once __DIR__ . '/../vendor/autoload.php';
require_once __DIR__ . '/../App/App.php';

// instancier
$app = new App($_SERVER['BASE_URI']);
$app->handleRequest();
```

# Autoload maison de Michaël
```
spl_autoload_register(function($class) {
require dirname(__DIR__) . '/App/Controller/' . $class . ".php";
});
```