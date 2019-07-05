# Gerer une session
1. Récupérer les données du form

2. Vérifier l'exactidtude du couple id/mdp

3. Si la verif est true, créer une session

Pour cela :

- Commencer la session en inscrivant `session_start()`  dans `header.tpl` pour être sûr d'avoir accès au tableau $_SESSION partout sur le site.

- Récupérer les infos dont nous auront besoin, en les stockant dans le tableau `$_SESSION`

- Si la vérif du couple id/mdp est true, je récupère l'identifiant de l'utilisateur
```php
$_SESSION['user'] = $username;
```

4. Créer les fonctions `logout()` et `check_auth()`

- Détruire la session lorsque l'utilisateur se déconnecte
```php
function logout() {
    session_start();
    session_destroy();
    redirect('index'); 
}
```

- Vérifier l'autentification pour gérer l'affichage du bouton déconnexion
```php
function check_auth() {

    $currentPage = basename($_SERVER['PHP_SELF']);

    if (!isset($_SESSION['user']) && $currentPage != 'index.php') {
        redirect('index');
    }

}
```

- Appeler la fonction dans `header.tpl`, et modifier le test d'affichage de déconnexion 

```php
require './inc/utils.php';
check_auth();
```

```php
<?php if (isset($_SESSION['user'])) { ?>
    <a href="logout.php">Déconnexion</a>
<?php } ?>
```

# Encrypter un mot de passe
```php
$mdpSaisi = "bonjour";
$mdpEncrypte = password_hash($motDePasseSaisiParLUtilisateur, PASSWORD_DEFAULT);

// autre forme d'encryptage
$motDePasseEncrypte = sha1($motDePasseSaisiParLUtilisateur);

var_dump($motDePasseEncrypte);
```
```php
``` 