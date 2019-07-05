# Introduction

## Les requêtes HTTP
- header dans lequel il y a des smétainformation 
- body : corps de la requête (requête elle-même)

[Méthodes de requête HTTP](https://developer.mozilla.org/fr/docs/Web/HTTP/M%C3%A9thode)


## Les superglobales
les 4 fantastiques (supergloables) sont 4 tableau toujours présent en PHP
- GET ($_GET) pas vide quand information dans l'url
- POST ($_POST) pas vide quan récupère le formulaire
- COOKIE ($_COOKIE) pas vide quand PHP capte qu'il y a des cookies sur le navigateur du client
- SESSION


# Créer un cookie

```php
setcookie("nomCool", "contenuCookie", time() + 31536000);
//31536000 coreespondt à 1 année en seconde car la loi interdit le stockage de cookies pour plus de 13 mois
```

# Login.php

```php
if (isset($_GET['username']) && isset($_GET['password'])) {

    // Inclusion des users
    require 'inc/users.php';

    // Parcours de tous les users
    foreach ($users as $currentId => $currentUser) {
    
        // Si le username du user courant correspond au username saisi
        if ($currentUser['username'] == $_GET['username']) {
        
            // Si le password correspond aussi
            if ($currentUser['password'] == $_GET['password']) {
            
                // Connecter le user en stockant son id
                setcookie('userId', $currentId);
                // rediriger vers la page index.php
                // header('Location: index.php');
            }
                
            // Arrêter la boucle, on a trouvé le bon user, même si le mot de passe est faux
            break;
        }
    }
}
```

# Index.php
```php
// Si j'ai un utilisateur connecté, afficher Bonjour + son nom !
if (isset($_COOKIE['userId'])) { // TODO place la bonne condition

    // On récupère les données sur le user connecté
    $userId = $_COOKIE['userId'];

    // Inclusion de la liste des users
    require __DIR__.'/inc/users.php';

    $connectedUser = $users[$userId];

    // templates à afficher
    $templateName = 'home-ok';
}
// Sinon, afficher une page d'erreur + bouton vers la page de connexion
else {
    // templates à afficher
    $templateName = 'home-not-connected';
}
```
Remarque, ici on va rendre l'inculsion de fichier dynamique

```php
include './templates/'.$templateName.'.php';
```

```php
```



