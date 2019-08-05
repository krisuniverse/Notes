# STRUCTURE
[Fiche récap](https://github.com/O-clock-Alumni/fiches-recap/blob/master/gestion-projet/modele-vue-controller.md)

\DateTime est une classe propre à php

##MVC
- Model
    - logique de l'application

- Views
    - templates

- Controller
    - le controller ne s'occupe pas du traitement


un point d'entrée qui appelle une méthode du controller qui va afficher des vues (view)


Inès (index.php) est le point d'entrée, il va se charger de définir les actions à eécuter pour tel ou tel url. le front controller contient toute l'intteligence des différents accès notre site 

## Renommer l'url

1. créer un fichier `.htaccess` (il sera lu par apache)

2. coller le code suivant dedans pour activer la réecriture html
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

Si l'url demandé n'existe pas, on sera redirigé sur la page index

## le dispatcher vs route
```php
// Le Dispatcher
if ($url === "/home") {

    $controller = new MainController();
    $controller->home();

} else if ($url === "/about") {

    $controller = new MainController();
    $controller->about();

} else if ($url === "/products") {

    $controller = new MainController();
    $controller->products();

} else if ($url === "/store") {

    $controller = new MainController();
    $controller->store(); 

} else {
    echo "Page not found";
}
```



- Une route :
    - une URL (/about)
    - Un controler (MainController)
    - Une méthode du controller (about())



 - Exemple avec le bon coin
 L'url complete c'est https://www.leboncoin.fr/annonces/offres/pays_de_la_loire/
 Le site c'est https://www.leboncoin.fr
 La route ca serait l'URL = "/annonces/offres/[région]/"
 Controller = AnnonceController et la methode = offre()
 [region] sera un parametre variable de notre route
