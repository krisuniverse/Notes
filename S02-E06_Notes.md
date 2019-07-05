# Fonction

## Créer une fonction (le cas simple)

Pour défininir une fonction, on utilise `function`
```php

function helloWorld() {
    echo "Hello World!";
}
```
**Bonne pratique**
- donner un nom explicit à la fonction

## Appeler sa fonction (le cas simple)

```php
helloWorld();
```

## Créer une fonction (avec un ou plusieurs paramètre)

```php
function verreMesureur($quantiteEnCl) {

    $quantiteEnLitre = ($quantiteEnCl / 100);

    return $quantiteEnLitre;
}

```

## Appeler sa fonction (avec un ou plusieurs paramètre)

Pour appeler la fonction, il suffit d'écrire son nom et de lui définir un ou plusieurs arguments (selon le nombre de paramètre nécessaire au fonctionnement de la fonction)

Dans cet exemple, la fonction prend 1 argument :
```php
verreMesureur(80);
```

## La portée des variables

Dans l'exemple précédent, je n'ai pas accès aux variables de ma fonction à savoir : `$quantiteEnLitre` et `$quantiteEnCl`

Je ne peux donc pas les appeler en dehors de ma fonction
Donc si je fais un var_dump() d'une de ces variables elles seront `NULL`
```php
function verreMesureur($quantiteEnCl) {

    $quantiteEnLitre = ($quantiteEnCl / 100);

    return $quantiteEnLitre;
}

var_dum($quantiteEnCl)
```

# Utiliser les fonctions grâce à include ou require

- Créer un ou plusieurs fichiers contenant les fonctions
- Inclure les fichiers avec un `include` ou un `require`
- Appeler la fonction


# Exemple Onews (Reprendre la correction de Djyp)

- Créer le tableau contenant les donées à afficher ne dynamique
```php
$articleList = [
    
]
```
- Créer une boucle qui affiche les articles de manière dynamique

> Pour chaque article, j'aimerais afficher ce contenu

```php
$articleList = [
    [
    "title" => "Lorem ipsum dolor article 1",
    "author" => "Darren Collison",
    "text" => "Lorem ipsum dolor sit amet,",
    "category" => "team",
    "date" => "2018-02-10",
    "image" => "../images/icon-dar.png",
    "link" => "article1.php"
    ],

    [
        "title" => "Lorem ipsum dolor article 2",
        "author" => "Darren Collison",
        "text" =>  "Lorem ipsum dolor sit amet,",
        "category" => "team",
        "date" => "2018-02-10",
        "image" => "../images/icon-dar.png",
        "link" => "article2.php"
    ]
];
```


```php
<?php foreach($articleList as $value): ?>

    <article class="post">
        <a href="" class="post__category post__category--color-<?= $value['category'] ?>">
            <?= $value['category'] ?>
       </a>
        <h3>
            <?= $value['title'] ?>
        </h3>
        <div class="post__meta">

            <img class="post__author-icon" src="<?= $value['image'] ?>" alt="">

            <strong class="post__author">
                <?= $value['author'] ?>
            </strong>

            <time datetime="2018-03-27">
                <?= date('d F Y', strtotime($value['date'])); ?>
            </time>
        </div>
        <p>
            <?= $value['description'] ?>
        </p>

        <a href="<?= $value['link'] ?>" class="post__link">Continue reading</a>

    </article>

<?php endforeach; ?>
```

- On va maintenant mettre la structure de l'article dans une fonction

    - Créer la fonction `showArticledescription`
    ```php

    function showArticleDescription($article) {
        // instructions
    }
    ```
    - Je donne des instruction à ma fonction

> Pour chaque tour de boucle je souhaite appeler `showArticleDescription`
Je vais donc reprendre la structure, puis passer la structure dans une variable `$articleHTML` qu'on va concatenner grâce à `.=` à mesure que la structure se construit

```php
<?php

function showPostOnIndex($post, $numero) {
    ?>
    <article class="post">
      <a href="" class="post__category post__category--color-<?= $post['categorie'] ?>"><?= $post['categorie'] ?></a>
      <h3><?= $post['titre'] ?></h3>
      <div class="post__meta">
        <img class="post__author-icon" src="../images/<?= $post['avatar'] ?>" alt="">
        <strong class="post__author"><?= $post['auteur'] ?></strong>
        <time datetime="<?= $post['date'] ?>">le <?= date('d F Y', strtotime($post['date'])) ?></time>
      </div>
      <p><?= substr($post['texte'], 0, 100) ?>…</p>
      <a href="article<?= $numero ?>.php" class="post__link">Continue reading</a>
    </article>
<?php
}
function showTitle ($title) {
    echo '<h2 class="right__title">' . $title . '</h2>';
}

```
:warning: 

- J'apelle ma fonction en incluant le fichier contenat les fonctions dans la page puis 