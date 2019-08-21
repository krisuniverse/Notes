# Eloquent et les requêtes SQL
[Doc Eloquent](https://laravel.com/docs/5.8/eloquent)

## Le modèle


Sur Lumen, les modèles sont à créé dans le dossier `app`. Pour mieux s'organiser, on va créer un dossier `Models`

:warning: Il ne faut pas oublier de changer "l'arborescence" du `namespace` et par extension le `use`, en raison de la création du dossier `Models` (cf. psr-4 et autoload)

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Videogame extends Model
{
    // spécifier le nom de la table si la table n'est pas au format snake case (pluriel du nom de la classe)
    protected $table = 'videogame';
    
}
```

## Le contrôleur

```php
<?php

namespace App\Http\Controllers;


use Illuminate\Http\Request;

use Illuminate\Support\Facades\DB;

class MainController extends Controller
{
    public function home(Request $request)
    {
        $orderInput = $request->all();

        $videogames = \App\Models\Videogame::all();

        // transmettre les données à la vues
        return view('home', ['videogames' => $videogames]);
    }

}

```

### Mode debug : tester la connexion à la BDD et récupérer les données
```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\DB;

class MainController extends Controller
{
    public function home(Request $request)
    {
        $videogames = \App\Models\Videogame::all();
        // MODE DEBUG
        print_r($videogames);

        foreach($videogames as $videogame){
            echo "$videogame->name ($videogame->editor, $videogame->release_date, $videogame->platform_id)";
        }
        // FIN MODE DEBUG
        return view('home');
    }
}
```

## La vue

On a passé `$videogames` à la vue, on peut donc boucler sur chaque objet du tableau :
```php
    <?php foreach ($videogames as $videogame) : ?>
        <tr>
            <td><?= $videogame->id ?></td>
            <td><?= $videogame->name ?></td>
            <td><?= $videogame->editor ?></td>
            <td><?= $videogame->release_date ?></td>
            <td><?= $videogame->platform_id ?></td>
        </tr>
    <?php endforeach ?>
```

# Le query builder
[Doc Query Builder](https://laravel.com/docs/5.8/queries)
    
- Ordonner par ordre croissant `orderBy('name', 'ASC')`
- Sélectionner les 3 premiers résultas `take(3)` par exemple
- TOUJOURS récupérer les résultats `get()` ( se fait à la fin de la requête)

**exemples**
```php
    if ($order === 'name') {
        $videogames = \App\Models\Videogame::orderBy('name', 'ASC')->take(3)->get();
    }
    else if ($order === 'editor') {

        $videogames = \App\Models\Videogame::orderBy('editor', 'ASC')->take(3)->get();
    }
    else {
        $videogames = \App\Models\Videogame::all();
    }
``` 