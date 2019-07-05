Passer un parametre en get 

Dans index

pour caque artucle du tableau $articleList tu déoupe ta ligne et tu va mettre ta clé dan sl avariable clé et la donnée qui est la clé associatif de la valeur $articleData


Dan sma boucle 'affiche ma fonction $showArtucleDescription, je lui passe ene paramettre $articledata (la référence) et l'index de mon tableau ($key)

supprimer artcile1.php, etc

# Validation d'un formulaire

Le formulaire contact.php utilise la méthode POST

1. Vérifier que tous les champs sont remplis

Cela permet d'éviter une modifcation ( via l'inspecteur) du formulaire par un utilisateur

Je vérifie que tout mes champs existent
```php

if( 
  isset($_POST['firstname']) &&
  isset($_POST['lastname']) &&
  isset($_POST['email']) &&
  isset($_POST['source']) &&
  isset($_POST['message']) &&
  isset($_POST['infos-ok'])
){
    echo 'Ok envoit de formulaire !';die;
} 


```
**remarque**
input = "require" permet de bloquer l'envoie du formulaire si le champs n'est pas rempli
la vérification avec isset n'empêche l'intérêt de son utilistaion

2. Récupérer les données
On passe nos données dans des variables
```php
/*
if( 
  isset($_POST['firstname']) &&
  isset($_POST['lastname']) &&
  isset($_POST['email']) &&
  isset($_POST['source']) &&
  isset($_POST['message']) &&
  isset($_POST['infos-ok'])
){ */

    $firstname = $_POST['firstname'];
    $lastname = $_POST['lastname'];
    $email = $_POST['email'];
    $source = $_POST['source'];
    $message = $_POST['message'];
    $checkVerif = $_POST['infos-ok'];

    echo 'Ok envoit de formulaire !';die;
} 
```
**remarque** le champ check a pour valeur on ou off 

3. Vérifier si les champs texte sont à minima remplis

 - On vérifie si ils sont vides (dans le if (isset())
```php

    if( empty($firstname)) {
      echo 'le champ firstname est vide';
    }

    if( empty($lastname)) {
      echo 'le champ lastname est vide';
    }

    if( empty($email)) {
      echo 'le champ email est vide';
    }

    if( empty($source)) {
      echo 'le champ source est vide';
    }
```

- On supprime les espaces avant et après grâce à `trim()`
[Fonction trim](https://www.php.net/manual/fr/function.trim.php)

```php
    $firstname = trim($firstname);
    $lastname = trim($lastname);
    $email = trim($email);
    $source = trim($source);
    $message = trim($message);
```


- On vérifie la valeur minima de la chaîne
```php
    $errors = false;

    if( empty($firstname)) {
      echo 'le champ firstname est vide';
      $errors = true;
    }

    if( empty($lastname)) {
      echo 'le champ lastname est vide';
      $errors = true;
    }

    if( empty($email)) {
      echo 'le champ email est vide';
      $errors = true;
    }

    if( empty($source)) {
      echo 'le champ source est vide';
      $errors = true;
    }
```

Si je n'ai pas d'erreur je continue, sinon :

```php
    if(!$errors){

      //je choisis que ma chaine foit avoir arbitrairement 4 caractere ou plus
      //if( count($firstname) < 4 ){ //ici 2 solutions fonctionne le count qui comptera l nombre de caracteres et strlen qui va evaluer la longueur d'une chaine de caractere
      if( strlen($firstname) < 4 ){

        echo 'firstname trop court ! 4 caracteres minimum attendus';
      }

      if( strlen($lastname) < 4 ){

        echo 'lastname trop court ! 4 caracteres minimum attendus';
      }

      if( strlen($email) < 4 ){

        echo 'email trop court ! 4 caracteres minimum attendus';
      }

      if( strlen($source) < 4 ){

        echo 'message trop court ! 4 caracteres minimum attendus';
      }

    }
```
```php
```
```php
```
```php
```
# Fonctions natives

Supprimer un espace avant et après la chaîne de caractère
- `trim();`