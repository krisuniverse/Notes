# Étape 1 

1. Créer la base de données

Supprimer data.php et le dossier étape 4

supprimer la ligne qui fait le require de data.php

Aller dans Data.php etre tirrer le require de data.php

## Étape 2 - Se connecter à la base de données et récupérer les tables

Créer un nouveau fichier qui va s'appeller DbData.php

Dedans on va créer une classe qui servira à se connecter à la base donnée

```php
class DbData 
{
    // Fonction qui permet de se connecter à la base données 
    public function dbConnect() {

        new PDO("mysql:host=localhost;dbname=blog;charset=utf8", "root", "Ereul9Aeng");

    }

    // étape 3 - récupéer les articles
    public function getArticles() {
        // connection à la base de données
        $db = $this->dbConnect();

        // récupérer la table articles
        $res_select = $db->query('SELECT * FROM articles');
        
        $articles = [];

        while ($data = $res_select->fetch()) {

            $articles[$data['id']] = new Article($data['title'], $data['content'] ,$data['author_id'],$data['publish_date'],$data['category_id'] )
        }

        return $articles;
    }

    // étape 4 - récupérer les catégories
    public function getCategories() {
        $db = $this->dbConnect();
        $categoryQuery = $db->query("SELECT * FROM categories");

        $categories = [];

        while($data = $categoryQuery->fetch()) {

            $categories[$data['id']] = new Category($data["category"]);

        }
        return $categories;
    }

    // étape 5 - récupérer les auteurs
    public function getAuthors() {

        $db = $this->dbConnect();
        $res_select = $db->query("SELECT * FROM authors");

        $authors = [];
        // Le fetch retourne à la ligne à chaque fois
        while ($data = $res_select->fetch()) {
      
            $authors[$data['id']] = new Author($data["author"]);

        }

        return $authors;
    }

}
```

Sur index.php
```php

require 'inc/classes/DbData.php';

$data = new DbData();
//var_dump($data->getArticles());


```

Sur DbData.php 
on va instancier la class DbData dans la fonction __construct()  et utiliser sa méthode getArticles

```php

// étape 3, 4 et 5
public function __constrcut() {
        // étape 3 (instancier la class DbData et appeler sa méthode getArticles())
        $data = new DbData();

        $this->articlesList = $data->getArticles();
        // étape 4 (appeler la méthode getCategories())
        $this->categoriesList = $data->getCategories();
        // étape 5 (appeler la méthode getAuthors())
        $this->categoriesList = $data->getAuthors();
}

```


## Récupérer les différentes tables 

```php


```

```php
```

```php
```

```php
```