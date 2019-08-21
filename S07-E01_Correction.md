# Procédure à suivre pour toute création de page en MVC

## 1. La Route

- Définir la route
  - l'URL
  - le nom du Controller
  - le nom de la méthode du Controller
  - la nom de la route (permet de générer une URL à partir de ce nom)

## 2. La Méthode (et le controller)
- Créer le Controller si nécessaire
- Définir la méthode du Controller
  - écrire un petit `return echo 'Test'` permettant de tester
- Tester la route

## 3. La View
- Créer la View dans le bon dossier
- depuis la méthode de Controller, appeler/faire référence à la View
- tester que la réponse HTTP contient bien le code de la View


# Syntaxe de Lumen
## Route
**Fichier cible :** routes/web.php
```php
// route en get
$router->get(
    '/url',
    [
        'uses' => 'ExempleController@method',
        'as' => 'routeName'
    ]
);

// route en post
$router->post(
    '/url',
    [
        'uses' => 'ExempleController@method',
        'as' => 'routeName'
    ]
);
```

## Controller
**Dossier cible :** app/Http/Controllers

### Sans données à transmettre
```php
<?php

namespace App\Http\Controllers;

public function myMethod()
{
    return view('templateName');
}
```

### Avec des données à transmettre
```php
<?php

namespace App\Http\Controllers;

// on rajoute cette ligne pour pouvoir utiliser la classe Request
use Illuminate\Http\Request;

public function myMethod(Request $request)
{
    // récupérer toutes les données
    $allInputs = $request->all();

    // récupérer un input précis
    $input = $request->input('inputName');

        return view('templateName', ['inputName'=> $input]);
}
```

## View
**Fichier cible :** resources/views
### home.php

Exemple de liens générés automatiquement et de liens prenant des paramètres en url
```html
<!-- Lien vers une autre page -->
<a href="<?= route('admin') ?>" class="btn btn-success float-right">Admin</a>

<!-- Lien avec des paramètres en url-->
<a href="?order=name" class="btn btn-primary">Trier par nom</a>&nbsp;
<a href="?order=editor" class="btn btn-info">Trier par éditeur</a>&nbsp;
<!-- Lien pour recharger la page -->
<a href="<?= route('home'); ?>" class="btn btn-dark">Annuler le tri</a><br>
```
### Le dossier layout
Pour le header et le footer, on va créer un sous-dossier `layout`
```php
```
### Le dossier  partials
Le dossier partials contient les vues partielles, celles qui seront incluses dans d'autre vues. On pourrait y mettre une barre de navigation. Les vues footer et header ne sont pas dans ce dossier, car elles sont un cas à part. 

**astuce**
```php
view('layout/header');
// équivaut à
view('layout.header');
```
**remarques**
- la constante magique `__DIR__` : dossier du fichier courant
- éviter la fonction `view()` sur les templates