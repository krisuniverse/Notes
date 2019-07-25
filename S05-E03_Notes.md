# Création de l'architecture

- `App` (gère le back)
    - Controllers
    - views
    - .htaccess
- `public` (gère le front)
    - assets 
        - css
        - js
        - images
    - .htaccess
    - index.php


**Bonne pratique**
- Mettre des majuscules à tous les dossiers/fichiers qui comportent des classes

# 1. Mettre en place le Front Controller

## Le fichier `.htaccess`
1. Créer le fichier `.htaccess` (obligatoire pour que le front controller fonctionne)
2. Copier le code ci-dessous
```
RewriteEngine On

# dynamically setup base URI
RewriteCond %{REQUEST_URI}::$1 ^(/.+)/(.*)::\2$
RewriteRule ^(.*) - [E=BASE_URI:%1]

# redirect every request to index.php
# and give the relative URL in "_url" GET param
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.*)$ index.php?_url=/$1 [QSA,L]
```
**Remarques**
- Ce fichier permet la redirection vers index lorsqu'une page qui n'existe pas est demandée
- Il permet également la réécriture de l'url

3. Bloquer l'accès à la partie back

- Créer un fichier .htaccess contenant l'instruction suivante dans le dossier que l'on souhaite protéger
```
Require all denied
```

# 2. Créer les routes

## Gestion des classes

1. Dans le dossier Controller créer des fichiers respectifs pour chaque classe
    - MainController
    - CatalogController

2. Dans ces fichiers, créer les classes correspondantes

```php
// sur MainController.php
class MainController 
{
    public function home() {
        $this->show('home');
    }

    public function legalMentions() {
        $this->show('legal-mentions');
    }

    private function show($templateName, $templateVars = array()) {
        include(__DIR__ . '/../views/header.tpl.php');
        include(__DIR__ . '/../views/' . $templateName . '.tpl.php');
        include(__DIR__ . '/../views/footer.tpl.php');
    }

}

// sur CatalogController.php
class CatalogController 
{
    public function category($categoryId) {
        $this->show('category', array('category_id' => $categoryId));
    }


    private function show($templateName, $templateVars = array()) {
        include(__DIR__ . '/../views/header.tpl.php');
        include(__DIR__ . '/../views/' . $templateName . '.tpl.php');
        include(__DIR__ . '/../views/footer.tpl.php');
    }

}
```

## Création des templates

1. Dans le dossier views, créer les templates header, footer et home (et toutes celles nécessaires)

```php
// header.tpl.php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>oShop</title>
</head>
<body>

// home.tpl.php
<h1>Home</h1>


// footer.tpl.php
</body>
</html>
```
## Instanciation des classes 

__Objectif__ : accéder aux méthodes nécessaires au chargement de la template

Dans `index.php`, instancier les classes MainController et CatalogController
Ne pas oublier d'inclure les fichier sur `index.php`


## Router vs AltoRouter

### La version manuelle (Router classique)
```php
if (!empty($_GET ['_url'])){
    $url = $_GET['_url'];
} else {
    $url = "/";
}

if($url === "/") {

    $controller = new MainController();
    $controller->home();

} else if ($url === "/mentions-legales") {

    $controller = new MainController();
    $controller->legalMentions();

} else if ($url === "/catalogue/categorie/1") {

    $controller = new CatalogController();
    $controller->category($id);

}
```
> Le problème avec cette façon defaire c'est que le routage se complique lorsque l'url est "dynamique" (changement d'affichage en fonction d'un id donné)
> On va donc se tourner vers un elibrairie qui facilite la tâche : AltoRouter 

### La version AltoRouter (utilisation de la librairie)

1. Après l'installation de composer et de la librairie AltoRouter, il faut obtenir l'accès à la classe AltoRouter pour pouvoir l'instancier

```php
// Autoload permet de charger automatiquement toutes les classes présentes dans le dossier vendor
require_once __DIR__ . '/../vendor/autoload.php';

```
2. Instancier la classe AltoRouter et stocker cette nouvelle instance dans la variable `$router`
```php
$router = new AltoRouter();
```

3. On va spécifier à partir d'où commence la route ("suppression" de la partie inutile de l'url)
```php
// configurer le router pour spécifier la partie de l'url à utiliser
$router->setBasePath($_SERVER['BASE_URI']);
//dump($_SERVER);
```

```php
/* informer AltoRouter des routes possibles */
// format : $router->map(méthode http, route ,target(controller, méthode),nom de la route )

// homepage (Dans les shoe)
$router->map(
    'GET', 
    '/', 
    array(
        'controller' => 'MainController', 
        'methode' => 'home'
    ), 
    'homepage'
);

// legal-mentions (Mentions légales)
$router->map(
    'GET', 
    '/mentions-legales',  
    array(
        'controller' => 'MainController', 
        'methode' => 'legalMentions'
    ), 
    'legal-mentions'
);
```

4. Après l'utilisation de la méthode map(), il faut matcher (faire corrrespondre) la route à la bonne méthode (et donc au bon controller)

```php

// demander au routeur de détecter sur quel route on se trouve
$match = $router->match();
//dump($match);

if($match !== false) {
    
    $nomDuControlleur = $match['target']['controller'];
    $nomDeLaMethode = $match['target']['methode'];
    $parametresDeLaRoute = $match['params'];

    //instancier le bon controller et appeler la méthode désirée
    $controller = new $nomDuControlleur();
    $controller->$nomDeLaMethode($parametresDeLaRoute);

} else {
    echo "Page not found";
}
```
**Remarque**
- `match()` renvoie un tableau

```php
array(
    'target' => [
        "controller" => "ProductController",
        "methode" => "productDetails"
    ],
    'params' => ['productId' => '2'],
    'name' => 'product-details'
)
``` 
- si on donne un argument à une fonction qui prend 0 paramètre, elle ne le traitera pas, en revanche si on fonction n'a pas assez de parametre elle ne fonctionnera pas


### Générer un lien grâce à AltoRouter

- méthode 1
```php
$categorieId = 456;
$lien = $router->generate('catalogue-category', array('categoryId' => $categorieId));

echo '<a href="' . $lien . '">Lien</a>';
```

- méthode 2 (en utilisant le nom de la route)
```php
$categorieIds = array(1,2,3,4,5,6,7,8,9);

foreach ($categorieIds as $value) {
    $lien = $router->generate('catalogue-category', array('categoryId' => $value));
    echo '<a href="' . $lien . '">Lien</a><br>';
}
```

```php
$lienAccueil = $router->generate('homepage') ;
echo '<a href="' . $lienAccueil . '">Accueil</a><br>';
```

On pourrait récuprer les id de catégorie via une requete sql (bdd)



# Installer composer

[Lien  pour installer composer](https://getcomposer.org/download/)

**Commandes d'installation:**
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

**Pour connaitre sa version de composer, écrire :**
```
composer -v
```

**À la racine du projet, faire :**
```
composer require symfony/var-dumper
```

**Remarques**
- Il ne faut pas mettre le dossier `vendorè sur git 

- Dès qu'on recupère le code de github, il suffit de faire `composer install` et le fichier vendor sera recréé.

- Par contre, il faut garder le fichier composer.json

- Pour pouvoir pusher son repo en toute tranquilité, mettre `/vendor` dans le fichier `.gitignore`


- Pour utiliser le var_dump de synfony il faut utiliser `dump()`

# Installer AltoRouter

[lien vers altorouter](http://altorouter.com/)
[lien cool sur AltoRouter](https://www.longren.io/basic-routing-in-php-with-altorouter/)

Commande :
```
composer require altorouter/altorouter
```

#Installer xdebug
recopier le truc de slack (par Kirs)
