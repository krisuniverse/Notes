# Atelier révison avec Michaël 


1. Créer la base de données 
contenant 

2. Créer la table users :
- id
- pseudo
- password 
    - Crypter le mot de passe via le terminal 
        Activer PHP :
        ```
        php -a
        ```
        Crypter le mot de passe :
        ```
        password_hash("root", PASSWORD_DEFAULT);
        ```

id: 1 
pseudo : Eredost
mdp : root
## Créer une class qui va gérer les intéractions avec la BDD

1. Créér une méthode pour se connecter

```php
class DbData 
{   
    public function dbConnect() {

            return new PDO("mysql:host=localhost;dbname=jesaispas;charset=utf8", "root", "Ereul9Aeng");
    }
}
```

2. Créer une fonction pour vérifier les inputs (pseudo et username)


```php

class DbData 
{   
    // public function dbConnect() { ... }

    public function checkInputs($pseudo, $password) {
        // connexion à la base de données 
        $db = $this->dbConnect();

        // Récupérer les informations de la BDD selon le pseudo fournit
        $res_select = $db->query("SELECT id, pseudo, password FROM users WHERE pseudo = '{$pseudo}' ");
        if ($res_select) {
            $data = $res_select->fetch();

            if (password_verify($password, $data["password"])) {
                
                return true;
            }
        }

        return false;
    }
}
```

La méthode checkInputs() renvoie :
- false si le pseudo est erroné
- false si le pseudo est bon mais le mdp erroné
- true si les 2 sont bons



3 Résultat :
```php

class DbData 
{   
    public function dbConnect() {

       return new PDO("mysql:host=localhost;dbname=jesaispas;charset=utf8", "root", "Ereul9Aeng");
    }

    public function checkInputs($pseudo, $password) {
        // connexion à la base de données           
        $db = $this->dbConnect();
        // Récupérer les informations de la BDD selon le pseudo fournit
        $res_select = $db->query("SELECT id, pseudo, password FROM users WHERE pseudo = $pseudo");
        if ($res_select) {
            $data = $res_select->fetch();

            if (password_verify($password, $data["password"])) {
                
                return true;
            }
        }

        return false;
    }
}
```

## Gérer les messages d'erreurs 
Sur index.php

**Plan d'attaque**
1. On démarre une session
2. On teste si le formulaire a été envoyé
    - on inclut le fichier DbData.php
    - on instancie la classe DbData
3. On teste les inputs avec la méthode checkInput
4. On affiche le message en fonction de la situation (connexion/non-connexion)

Tout en haut d'index.php :
```php
session_start();

 if(!empty($_POST["pseudo"]) && !empty($_POST["password"])) {

   require 'classes/DbData.php';
   $data = new DbData();

   $message = "";

   if($data->checkInputs($_POST["pseudo"],$_POST["password"])) {

    $_SESSION['username'] = $_POST["pseudo"];

    $message = <<< HTML
            <div class="alert alert-success">Vous êtes bien connecté !</div>
HTML;

   } else {

        $message = <<< HTML
            <div class="alert alert-danger">Vos identifiants sont incorrects !</div>
HTML;

   }

 }
```

On inclut le message $message entre le champs mot de passe et le bouton dans la structure html

```php
<?= $message ?>
```


/etc/php/7.2/apache2/php.ini


Changer en :
error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT

display_errors = On

# Faille de sécurité

Injection sql
- pseudo : 'OR"='

avec le bon mdp on peut se connecter où on veut

On change le query() en prepare()
le execute() va "assaisnir" ce qi est saisie dan sle champs pseudo (il échappe les caractères  qui pourrait lui être fatal)
```php
class DbData 
{   
    // nouvelle version 
    public function checkInputs($pseudo, $password) {
        // connexion à la base de données         
        $db = $this->dbConnect();
        // Récupérer les informations de la BDD selon le pseudo fournit
        $res_select = $db->prepare("SELECT id, pseudo, password FROM users WHERE pseudo = :pseudo");
        $res_select->execute(array(
            "pseudo" => $pseudo
        ));

        if ($res_select) {
            $data = $res_select->fetch();

            if (password_verify($password, $data["password"])) {
                
                return true;
            }
        }

        return false;
    }
}
```