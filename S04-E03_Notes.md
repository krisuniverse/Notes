# Bootstrap

## 1.Charger la librairie pré-existante

1. Lier les fichiers css dans la balise `<head>`


```html
<head>
    <!-- code classique-->

    <!-- Latest compiled and minified CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">

    <!-- Optional theme -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap-theme.min.css" integrity="sha384-rHyoN1iRsVXV4nD0JutlnGaslCJuC7uwjduW9SVrLvRYooPp2bWYgmgJQIXwl/Sp" crossorigin="anonymous">
</head>
```

2. Charger les scripts dans le footer
```html
    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
    <!-- Latest compiled and minified JavaScript -->
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
```

## Inclusion de la class Article
```php
require_once __DIR__.'/classes/articles.php';
```

## La balise time
```html
<time datetime="<?= $article->date ?>"><?= $article->getDateFr(); ?></time>

```

## Gerer l'affichge grâche à `$_GET`

Passer dans l'url la clé et la valeur 
ici clé = template te valeur = article
```html
<a class="nav-link" href="index.php?template=article&id=1"> Article </a>
```

# Vérifier l'existence d'un article
```php
array_key_exists
```
```php
```