# Étape 1 - Synchronisation des montres

Après avoir cloné le repo, aller sur le terminal et taper les commandes suivantes :

1. Aller sur la branche master (là où on veut "importer" la branche integration-html-css): 
```
git checkout master
```
2. Fusionner la branche integration-html-css avec la branche master : 
```
git merge origin/integration-html-css
```
**conseils**
Il est fortement recommendé d'utiliser des branches pour faciliter la gestion du code et limiter la "propagation" des erreurs


# Étape 2 - Dynamisation 

**Objectifs** : 
- dynamiser l'affichage des __articles__ sur la page home

- dynamiser l'affichage d'un __article__ sur la page article

- dynamiser l'affichage des __catégories__ dans la nav du header et dans la sidebar (footer)

- dynamiser l'affichage des __auteurs__ dans la sidebar (footer)


## 2.1 La classe Data et l'instance `$dataObject`
La classe Data est incluse grâce au `require 'inc/classes/Data.php'`

Cette classe permet d'avoir accès à la liste des articles, des catégories et des auteurs. 

De base, ses propriétés sont privées. Pour pouvoir agir sur ces propriétés on utilise des méthodes. ces méthodes constituent une interface (API) qui nous permet d'intéragir avec les propriétés (le state).

Pour pouvoir l'exploiter, on va l'instancier L12 sur `index.php`.

Au passage, lorsqu'on instancie Data L12, on a accès au fichier data.php car il est inclus dans la fonction `__construct()` via `require 'inc/data.php'`.

**remarque**
La portée de `require` et `include` est "globale".

```php
$dataObject = new Data();
```
Pour accéder à la liste des articles on va tout simplement accéder à la propriété de l'instance :

```php
$articlesList = $dataObject->getArticles();
$categoriesList = $dataObject->getCategories();
$authorsList = $dataObject->getAuthors();
```

## Le DocBlock
Le DocBlock sert à documenter son code
```
/**
 * Ceci est un DocBlock
 */
```

**Quelques exemples**
```php
/**
 * @var Article[]
 */
// indique la présence d'une variable qui contient un tableau d'objets de type Article

/**
 * @return Article []
 */
//indique que la fonction renvoie un tableau d'objects de type Article


/**
 * @param int
 */
// indique que la fonction prend un paramère de type entier
```


## 2.2 Dynamiser l'affichage des articles (sur home.tpl)

1. Créer une boucle foreach : elle boucle sur le tableau $articlesList (qu'on a récupérer grâce à l'instance de type Data dan sle ficheir index)
2. Dynamiser le titre `<h2>`, le text `<p>`, l'auteur et la ctagorie

```php
<?php foreach ($articlesList as $currentId => $currentArticle) : ?>
    <!-- Affichage avec une card: https://getbootstrap.com/docs/4.1/components/card/ -->
    <article class="card">
        <div class="card-body">
            <h2 class="card-title"><a href="#"><?php echo $currentArticle->title ?></a></h2>
            <p class="card-text"><?= $currentArticle->content ?></p>
            <p class="infos">
              Posté par <a href="#" class="card-link"><?= $currentArticle->author ?></a> le <time><?= $currentArticle->getDateFr() ?></time> dans <a href="#" class="card-link"><?= $currentArticle->category ?></a>
            </p>
        </div>
    </article>
<?php endforeach ?>
```

## 2.3 Dynamiser l'affichage de la page article (article.tpl)

1. S'assurer de la présence des query parameters

**rappel**
Dans le routeur, on a défini `$page` comme étant `trim($_GET['page'])`

Dans la condition qui gère l'affichage de la page article :
- vérifier qu'il y a bien une valeur pour `id`
- au passage, on récupère l'article en question dans la variable `$article`

```php
else if ($page == 'article') {
    // récupérer l'id fournit en paramètre de l'URL
    if (!empty($_GET['id'])) {
        $articleId = intval(trim($_GET['id']));
    }
    else {
        $articleId = 0;
    }

    // version condensée (condition ternaire) :
    // $articleId = !empty($_GET['id']) ? intval(trim($_GET['id'])) : 0;

    // récupérer l'objet article pour l'id fourni
    $article = $dataObject->getArticle($articleId);
    $templateName = 'article';
}
```

2. Afficher grâce à `$article` les bonnes données
```php
<article class="card">
  <div class="card-body">
    <h2 class="card-title"><a href="#"><?php echo $article->title ?></a></h2>
    <p class="card-text"><?= $article->content ?></p>
    <p class="infos">
      Posté par <a href="#" class="card-link"><?= $article->author ?></a> le <time><?= $article->getDateFr() ?></time> dans <a href="#" class="card-link"><?= $article->category ?></a>
    </p>
  </div>
</article>
```

## 2.4 Dynamiser l'affichage des catégories et des auteurs (sur header.tpl)

1. Créer la méthode `getCategories()` dans la classe `Data`
```php
public function getCategories() {
    return $this->categoriesList;
}
```

2. Boucler sur tableau `$categoriesList` contenant la liste des catégories

3. Inclure les données de manières dynamiques
```php
<ul class="navbar-nav ">
    <?php foreach ($categoriesList as $categoryId => $category) : ?>
        <li class="nav-item">
            <a class="nav-link" href="index.php?page=category&id=<?= $categoryId ?>"><?= $category->category ?></a>
        </li>
    <?php endforeach; ?>
</ul>
```

**Rappel**
Sur index.php on avait défini :
```php
$categoriesList = $dataObject->getCategories();
```

## 2.5 Dynamiser l'affichage des catégories et des auteurs (sur footer.tpl)

1. Créer la méthode `getAuthors()` dans la classe `Data`
```php
public function getAuthors() {
    return $this->authorsList;
}
```

2. Boucler sur tableau `$authorsList` contenant la liste des auteurs et inclure les données de manières dynamiques

```php
<?php foreach($authors as $authorId => $authorName): ?>
    <li class="list-group-item">
        <a href="#"><?= $authorName ?></a>
    </li>
<?php endforeach ?>
```

3. Boucler sur tableau `$categoriesList` contenant la liste des auteur et inclure les données de manières dynamiques

```php
<?php foreach($categories as $categoryId => $categoryName): ?>
    <li class="list-group-item">
        <a href="#"><?= $categoryName ?></a>
    </li>
<?php endforeach ?>
```

**Rappel**
Sur index.php on avait défini :
```php
$categoriesList = $dataObject->getCategories();
$authorsList = $dataObject->getAuthors();
```

# Étape 3 - Gestion des liens

1. Changer les attributs href dans les différentes templates
2. Faire une danse de la joie quand tout fonctionne

```php
// header.tpl
<a href="index.php?page=category&id=<?= $categoryId ?>"></a>

//footer.tpl
<a href="index.php?page=category&id=<?= $categoryId ?>"></a>
<a href="index.php?page=author&id=<?= $authorId ?>"></a>

// home.tpl
<h2 class="card-title"><a href="index.php?page=article&id=<?= $articleId ?>"><?= $article->title ?></a></h2>
```
```php
```
# Étape 4 - Classes `Category` & `Author`

clé étrangère : identifiant pour aller chercher une info dans un autre tableau
1.
1. Créer un fichier Author.php et un fichier Category.php dans le dossier classes 

2. Créer les class Author et Category dans leurs fichiers respectifs
```php
// dans le fichier Category.php
class Category {
  public $name;

  public function __construct($name) {
    $this->name = $name;
  }
}

// dans le fichier Author.php
class Author {
  public $name;

  public function __construct($name) {
    $this->firstName = $name;
  }
}
```

3. Inclure les classes dans le fichier index.php

```php
require 'inc/classes/Category.php';
require 'inc/classes/Author.php';
```

4. Modifier la boucle d'affichage des catégories dans le header

:warning: CategoryName n'est plus une simple valeur, c'est une instance de type Category

```php
// avant
<?php foreach($categories as $categoryId => $categoryName): ?>
    <li class="nav-item">
    <a class="nav-link" href="index.php?page=category&id=<?= $categoryId ?>"><?= $categoryName ?></a>
    </li>
<?php endforeach ?>

// après 
<?php foreach($categories as $categoryId => $categoryObj): ?>
    <li class="nav-item">
    <a class="nav-link" href="index.php?page=category&id=<?= $categoryId ?>"><?= $categoryObj->name ?></a>
     </li>
<?php endforeach ?>
```

5. Répéter l'étape 4 pour les catégories et les auteurs dans le footer.tpl
```php
// pour les catégories
<?php foreach($categories as $categoryId => $categoryObj): ?>
    <li class="nav-item">
    <a class="nav-link" href="index.php?page=category&id=<?= $categoryId ?>"><?= $categoryObj->name ?></a>
    </li>
<?php endforeach ?>

// pour les auteurs
<?php foreach($authors as $authorId => $authorObj): ?>
    <li class="list-group-item">
     <a href="index.php?page=author&id=<?= $authorId ?>"><?= $authorObj->name() ?></a>
    </li>
<?php endforeach ?>
```


# Étape 5 - Page catégorie

1. Dans Data.php, créer une méthode qui va créer un tableau d'articles d'une même catégorie
```php
/**
 * Retourne la liste d'articles pour une catégorie donnée.
 *  
 * @param int $categoryId ID de la catégorie
 * @return Article[]
 */

public function getArticlesByCategoryId($categoryId) {
    // créer un tableau vide, qu'on remplira des articles de la catégorie
    $articles = [];

    // pour chaque article du site
    foreach ($this->articlesList as $currentId=>$currentArticle) {
        // si l'id de la catégorie correspond à l'id fourni en paramètre
        if ($currentArticle->category == $categoryId) {
            // alors ajouter l'article dans le tableau
            $articles[$currentId] = $currentArticle;
        }
    }
    // à la fin, retourner le tableau
    return $articles;
}

```

2. Modifier le routeur pour utiliser la méthode sur index.php

```php
// Page catégorie.
else if ($page == 'category') {
    $templateName = 'category';
    $articlesList = $dataObject->getArticlesByCategoryId($_GET['id']);
}

```
3. Modifier category.tpl pour dynamiser le `<h1>` (titre de la catégorie) et la structure des articles obtenus dans le tableau

4. Créer une méthode pour récupér le nom de la catégorie passée en url

```php
<h1><?= $category->name ?></h1>

<?php foreach ($articlesList as $currentId => $currentArticle) : ?>
<ul class="list-group">
  <li class="list-group-item">
    <a href="index.php?page=article&id=<?= $currentId ?>"><?= $currentArticle->title ?></a>
    <span class="badge badge-light badge-pill"><?= $currentArticle->author ?></span>
    <span class="badge badge-secondary badge-pill"><?= $currentArticle->getDateFr() ?></span>
  </li>
</ul>
<?php endforeach ?> 
```

Dans le routeur, stocker le résulat dans la variable `$category` :
```php
// Page catégorie.
else if ($page == 'category') {
    //$templateName = 'category';
    $category = $dataObject->getCategory($_GET['id']);
    //$articlesList = $dataObject->getArticlesByCategoryId($_GET['id']);
}

```

# Étape 6 - Page auteur
 
C'est la même chose que pour l'étape 5, donc débrouille-toi !


