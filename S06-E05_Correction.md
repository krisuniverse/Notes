# Simuler le nom de domaine

En simulant un nom de domaine, le base_uri est égale à `null`. Ce qui empêche le fonctionnement de AltoRouter. Pour résoudre le problème, on va créer une condition :

## Version classique
```php
if (isset($_SERVER['BASE_URI']) {
    $base_uri = $_SERVER['BASE_URI'];
} else {
    base_uri = '';
}
```

## Version ternaire
```php
$baseUri = isset($_SERVER['BASE_URI']) ? $_SERVER['BASE_URI'] : '';
```
## Version michaël
```php
$baseURI = $_SERVER["BASE_URI"] ?? "";
```

**remarque**
- Le `BASE_URI` est généré par le code présent deans le .htacess

# Informer le navigateur d'une 404

## Dans le AltoDispatcher (Ben)
AltoDispatcher le fait déjà, grâce à ces lignes :
```php
if (!$match) {
    header('HTTP/1.0 404 Not Found');
    $this->parseTarget($fourOFourAction);
    return;
}
```

## Sans AltoDispatcher
```php
// la fonction 
http_response_code(404);

// exemple
class ErrorController extends CoreController
{

    public function err404()
    {
        http_response_code(404);
        $this->show('404');
    }
}
```
**remarque**
- Un header doit toujours être envoyé en premier
- les termes `nndpoint` et `route` sont similaires. On préfera le terme endpoint à celui de route lorsqu'on parle d'api.