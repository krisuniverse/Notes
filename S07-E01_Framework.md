# Programme du jour
1. Lumen
2. Composer ++

**support de cours**
- [first lumen project](https://github.com/O-clock-Universe/S07-E01-exo-first-lumen-project)

# Framework vs Micro-framework
suite d'élément servant de base, réulitisable d'un projet à l'autre

:warning:ne pas confondre avec une librairie

> La librairie, c'est une clé de 12. Le framework, c'est tout l'établi - Pierre

**quelques exemples de librairies**
- react
- angular

**quelques exemples de frameworks**
- Symfony (suit l'architecture mvc, français, prestashop et drupal sont basés dessus)
- Laravel
- Zend
- CakePHP
- Ruby on Rails
- Phalcon (particularité : C-extension, permet de ne pas devoir charger un script mais est plus difficile à mettre en place)

**quelques exemples de micro-frameworks**
- base de travail plus légère, permettant de répondre à des besois basiques (petits sites)
- Lumen
- Slim
- Silex (n'existe plus)

#  Lumen
version condenscé de Laravel (créer par Laravel)
lumen est particulière adapté pour faire des api
[Doc Lumen](https://lumen.laravel.com/)

## Installation de Lumen

###1. Créer un projet avec lumen

- Aller dans le dossier de la saison 7 puis faire la commande `composer`
- :warning: ne pas créer le repo à l'avance (pas de clonnage)
```
cd /var/www/html
cd S07
composer create-project --prefer-dist laravel/lumen S07-E01-lumen-videogame
```

###2. Activer le serveur web de PHP 
Se placer dans le dossier du projet puis saisir la commande suivante :
```
php -S localhost:8080 -t public
```
**remarques**
- port : localhost:8080
- fichier racine : public
- Couper le serveur web
    - faire ctrl+c

Permet d'accéder au dossier public sans écrire le chemin complet `http://localhost/S07/S07-E01-lumen-videogame/public/`
(ne fonctionne plus en fois le serveur désactivé)

###3. Faire le lien entre le repo local et GitHub
```
git init
git add .
git commit -m "init"
```
Pour pusher il faut c/c les commandes présentes dans le repo
```
git remote add origin git@github.com:O-clock-Universe/s07-e01-lumen-videogame-Amy-universe.git
git push -u origin master
```

Ou saisir manuellement les commandes suivantes :
```
git remote add <nom> <url>
git push <nom>
```

###4. Attribuer tous les droits à tout le monde (Version sauvage)
Dans le dossier du projet :
```
sudo chmod -Rf 777 storage
```

Vérifier que storage a bien les bon droit
```
ls -lsa
```

**Résultat attendu:**
```
  4 drwxr-xr-x  5 mint mint   4096 mai   27 20:11 storage
```
### 5. Renseigner le fichier de config`.env`
le fichier .env correspond au fichier de configuration (conf.init)

le fichier .env.example correspond au fichier distribué

en prod `APP_DEBUG=` est `false`


### 6. 
le dossier `boostrap` (lanière de démarrage) n'a aucun lien avec le framework bootstrap. 

Ce fichier contient toutes les choses à faire lorsqu'on démarre le projet, c'est l'amorce d'une page.

1. Activer les facades
- Décommenter la ligne `$app->withFacades();`

- permet d'avoir une interface statique pour les services de l'application.

```php
// Sans Facades
$results = app('db')->select("SELECT * FROM users");

// Avec Facades
$results = DB::select("SELECT * FROM users");
```

2. Activer Eloquent
- Décommenter `$app->withEloquent();`
- c'est un ORM
- CRUD déjà implémentés
- Seuls les Models sont à créer (et sans propriétés), Eloquent s'occupe du reste

```php
// modifier et sauvegarder une utilisateur donné
$user4 = User::find(4);
$user4->username = 'perceval';
$user4->save();
```


## Les routes avec Lumen
[Doc sur les routes](https://lumen.laravel.com/docs/5.8/routing)

**Les routes sont à définir dans le fichier`routes/web.php`** 

Les routes simples prennent 2 paramètres : l'URI et le callback(closure)

```php
$router->get('/', function () use ($router) {
    return "Hello World";
});
```

## les vues avec Lumen
[Vues avec Lumen(Laravel)](https://laravel.com/docs/5.8/views)

**Les vues se trouvent dans le dossier `resources/views`**

Exemple :
```html
<html>
    <body>
        <h1>Hello, {{ $name }}</h1>
    </body>
</html>
```

Pour fournir des données à la vue :
```php
Route::get('/', function () {
    return view('greeting', ['name' => 'James']);
});
```

Exo du cours :
```php
// dans resources/views/mavuetoto.php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Videogame</title>
</head>
<body>
    <h1>Bonjour Bulle</h1>
</body>
</html>
```
Sans transmettre de données à la vue
```php
// dans routes/web.php
$router->get(
    '/toto-route',
    function() {
        return view('mavuetoto');
    }
);
```

En transmettant des données à la vue
```php
$router->get(
    '/toto-route',
    function() {
        return view('mavuetoto', ['name' => 'tinyBulle']);
    }
);
```

Nommer la route
```php
$router->get(
    'foo',
    [
        'uses' => 'FooController@method',
        'as' => 'nomDeLaRoute'
    ]);
```

## Les controllers
[Doc sur les controllers](https://lumen.laravel.com/docs/5.8/controllers)

**les controllers sont dans le dossier `app/Http/Controllers`**

Structure de base :
```php
<?php

namespace App\Http\Controllers;

class ExempleController extends Controller
{
    /**
     * Méthode permettant de gérer le contenu pour l'URL /toto-route
     * HTTP-methode; GET
     * URL: /toto-route
     */
    public function maFonction()
    {
        //
    }

    //
}
```

Exemple du cours :
```php
// Dans le fichier app/Http/Controllers/MainController.php
<?php

namespace App\Http\Controllers;

class MainController extends Controller
{
    public function toto()
    {
        return view('mavuetoto', ['name' => 'Tutu']);
    }

}


// Dans le fichier routes/web.php
$router->get(
    '/toto-route',
    [
        'uses' => 'MainController@toto',
        'as' => 'main-toto'
    ]
);
```

## générer un lien à partir d'une route
[Doc pour la génération de lien ](https://lumen.laravel.com/docs/5.8/routing#named-routes)

```php
    <p>
        <a href="<?= route('main-toto'); ?>">Lien vers la page /toto-route</a>
    </p>
```
**remarques**
le chargement des classes se fait via l'autoload de composer dans le fichier composer.json

## Parametre en URL
[Doc sur Request](https://lumen.laravel.com/docs/5.8/requests)

Dans le controller :
 - ajouter la ligne `use Illuminate\Http\Request;` pour pouvoir accéder à la classe Request et récupérer les données de la requête HTTP
- passer `Request $request` en paramètre de la méthode en question, ici `toto()`

```php
// Dans le fichier app/Http/Controllers/MainController.php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class MainController extends Controller
{
    public function toto(Request $request)
    {
        // Permet de récupérer une données envoyées dans la requête HTTP (GEt ou POST)
        $chiffre = $request->input('chiffre');

        return view('mavuetoto', ['name' => 'tinyBulle']);
    }
}

```

## Donner une valeur par défaut
cf. replay

## Retourner une réponse Json
[JSON Responses](https://lumen.laravel.com/docs/5.8/responses#other-response-types)

```php
// Dans le fichier app/Http/Controllers/MainController.php
if ($chiffre == 51) {
  // données à convertir en JSON
  $data = [
    'name' => 'Pastis',
    'type' => 'Alcohol',
    'origin' => 'Marseille'
  ];
  return response()->json($data);
}
```

## La rédirection
```php
else if ($chiffre == 5) {
  // redirection vers une route nommée
  return redirect()->route('main-toto');
}
```

## Les messages d'erreur
[Doc sur les logs](https://laravel.com/docs/5.8/logging)
Pour cela on a obligatoirement besoin de la facade Log
```php
Log::emergency($message);
Log::alert($message);
Log::critical($message);
Log::error($message);
Log::warning($message);
Log::notice($message);
Log::info($message);
Log::debug($message);
```

Exemple du cours :
```php
// Dans le fichier app/Http/Controllers/MainController.php
else if ($chiffre == 5) {
  Log::info('on rediriger vers la même page');
  // redirection vers une route nommée
  return redirect()->route('main-toto');
}
```

# Info en plus
## La fonction `exctract()`
La fonction `extract()` associe les clés et les valeurs d'un tableau associatif, et les retourne sous forme de variables (portant le nom des clés)

# Astuces
## 1.Mettre à jour php
sudo apt-get update
sudo add-apt-repository ppa:ondrej/php
sudo apt update

sudo apt-get install php7.2 php7.2-common php7.2-cli libapache2-mod-php7.2  php7.2-mbstring php7.2-json php7.2-cli php7.2-mysql php7.2-xml

sudo sed -i -e s/"display_errors = Off"/"display_errors = On"/ /etc/php/7.2/*/php.ini

sudo a2dismod php7.0
sudo a2enmod php7.2
sudo service apache2 restart

## 2.Vérifier les erreurs PHP
```
cat /etc/php/7.2/apache2/php.ini | grep "display_errors ="
```
## 3.Problème de cache
```
sudo chown -R $USER $HOME/.cache
sudo chown -R $USER $HOME/.composer
```

## 4.Vérifier la version 
Permer de créer me fichier `info.php` qui comporte la version de PHP
```
echo "<?php phpinfo();" > /var/www/html/info.php
```
si tout va bien, il ne se passe rien

## 5.Pusher un repo existant via la ligne de commande
```
git init
git add .
git commit -m "init"
```
Pour pusher il faut c/c les commandes présentes dans le repo
```
git remote add origin git@github.com:O-clock-Universe/s07-e01-lumen-videogame-Amy-universe.git
git push -u origin master
```

Ou saisir manuellement les commandes suivantes :
```
git remote add <nom> <url>
git push <nom>
```

