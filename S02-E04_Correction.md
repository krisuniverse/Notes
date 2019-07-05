# Étape 1

## Objectif
Rediriger l'internaute sur la page du premier article avec son texte complet

## Comment faire ?
1. Copier la structure de index.html dans le fichier html/article.html
2. Faire les modifications html adéquates (lorem400, lien : Back to home)
3. Créer une nouvelle class pour le page article 

    ```php
    <article class="post post--solo"> </article>
    ```

    ```css
    .post--solo {
        width: 100%;
    }
    ```
**L'inétrêt d'avoir un deuxième fichier css**
Le second fichier vient compléter ou modifier ce qui est existant


# Étape 2

## Objectif
Factoriser ce code HTML, c'est-à-dire éviter les répétitions

## Comment faire ?
1. Copier les fichiers HTML dans le répertoir php puis les renommer
2. Analyser le code pour repérer le HTML qui se répète
3. Créer les templates header et footer et les placer dans le dossier inc  :
    - Le header
    ```php
    <header class="left"> 
        <!-- HTML -->
    </header>
            <main class="right">
    ```
    - Le footer
    ```php
            </main>
        </div>
    </body>

    </html>
    ```
3. (bis) Créer les templates head, 
```php
<!DOCTYPE html>
<html>

<?php
    require '../php/inc/head.php';
?>

<body>
    <div class="wrapper">
        // Inclusion de la balise <header> qui correspond à la partie gauche
        <?php
            require '../php/inc/header.php';
        ?>
        // Inclusion de la balise <main>  qui correspond à la partie de droite
            <?php
            require '../php/inc/article.php';
            ?>
    </div>
</body>
</html>

```

4. Inclure les templates avec `require` ou `include`
    - Inlude : tente d'inclure le fichier, s'il ne le trouve pas il nous avertit qu'il y a un problème mais continue d'executer le script 
    - Require : la page requiert ce fichier pour fonctionner, si la ressources n'est pas trouvée le script s'arrête avec une erreur fatale (Parse error)

**Remarques**
- Lorsque qu'un fichier va être inclus une et une seule fois par page,  `require_once` va verifier si mon fichier a été inclu  une fois sinon il ne repetera pas l'operation
- On ne peut inclure qu'un `require_once` par page


# Étape 3

## Objectif
Rendre les données de la page "article" dynamiques

## Comment faire ?
1. Créer un tableau associatif contenant les données nécessaire sà la création de l'article 
```php
$article = [
    'title' => 'Lorem ipsum dolor article 1',
    'author' => 'Darren Collison',
    'text' => [
        'para_1' => 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat possimus sunt, deserunt ipsum molestiae vitae porro rerum quibusdam, earum deleniti nostrum itaque, doloremque libero quae distinctio necessitatibus inventore exercitationem excepturi aliquam. Dolores libero soluta porro delectus, minima fugiat ab eum iusto totam doloremque magnam harum quasi, eius deserunt laboriosam numquam, tempore obcaecati maxime ullam tenetur consectetur quidem! Nesciunt praesentium atque dolor amet adipisci aliquam et minus ipsa? Laborum optio harum libero? Veritatis ad maiores similique, ut minima consequatur, expedita fugiat provident cupiditate sequi exercitationem ullam delectus officia, omnis corrupti ratione deleniti? Harum accusantium est provident. Tenetur hic sapiente autem quidem harum mollitia eaque odio rem voluptatibus vero adipisci nesciunt ad accusantium aliquid ducimus, fuga excepturi cupiditate quaerat enim illum ullam illo nobis necessitatibus consectetur? Aut quos mollitia et qui obcaecati fugiat, autem quidem ea debitis consequuntur facilis veniam cupiditate. Sint iure ea quidem aliquid ipsum? Voluptate expedita similique impedit aspernatur? Maiores similique, ratione fugit excepturi iusto magnam, dolores nemo tenetur, pariatur eligendi sapiente asperiores unde. Ea quae nemo consequuntur libero. Vero hic, ipsam quas asperiores sit sed! Necessitatibus cupiditate reprehenderit mollitia ipsam vitae similique quam voluptate minima asperiores veritatis magni non repudiandae, laborum at iste! Illo minima ducimus provident cum autem beatae libero fugit doloribus error, nihil id quisquam ratione sunt architecto sequi numquam? Amet voluptatum obcaecati consectetur minus. Vel praesentium temporibus dolores ipsam?',
        'para_2' => 'Sequi qui, eveniet sunt ipsam ad porro aspernatur iste debitis quas dignissimos dolore facere magnam vero tenetur ipsa quidem laboriosam aliquid voluptatum a quo veritatis iure eos deleniti nesciunt? Molestias ab laudantium veritatis maiores eveniet tempora saepe rerum. Ratione autem expedita odit in quaerat exercitationem veniam, aut veritatis quasi beatae a obcaecati, iure minima? Iusto deleniti temporibus porro nemo, quod pariatur reiciendis corporis odio voluptas cum magni asperiores numquam delectus qui possimus laborum! Accusamus asperiores assumenda illum quisquam, magni consequuntur, natus quasi, ex reiciendis aspernatur labore? Maiores distinctio, a ratione eligendi temporibus perferendis odio beatae cupiditate sunt enim non repudiandae quod eius, aspernatur reiciendis accusantium debitis! Fuga voluptate magnam veniam, dignissimos unde ratione, consequuntur sapiente iste hic tempora suscipit doloremque, harum id incidunt voluptatibus aliquam neque eum fugiat! Temporibus deserunt, facere tempore qui ducimus maxime doloribus adipisci aut. Perferendis hic atque perspiciatis ipsum? Sunt, aliquid quos inventore tempora cum aspernatur iste pariatur ex libero est a, saepe porro. Dolor, accusantium voluptatem excepturi earum, perferendis dicta odit ad, nobis nostrum assumenda voluptas necessitatibus dolorum incidunt debitis voluptatibus!'
        ],
    'category' => [
        'class' => 'post__category post__category--color-team',
        'nom' => 'team',
        ] ,
    'date_publi' => [
        'date_robot' => '2018-02-10',
        'date_human' => 'le 10 février 2018',
        ],
    'img_author' => '../images/icon-dar.png'
];
```
2. Remplacer le HTML par les inclusions PHP `<?= $article['maClef']?>`
```php
// Structur HTML de l'article
<h2 class="right__title"><?= $article['title'];?></h2>
<div class="posts">
    <article class="post post--solo">
        <a href="" class="<?= $article['category']['class'];?>"><?= $article['category']['nom'];?></a>
        <div class="post__meta">
            <img class="post__author-icon" src="<?= $article['img_author']?>" alt="">
            <strong class="post__author"><?= $article['author'];?></strong>
            <time datetime="<?= $article['date_publi']['date_robot']; ?>"><?= $article['date_publi']['date_human']; ?></time>
        </div>
        <p><?= $article['text']['para_1'];?></p>
        <p><?= $article['text']['para_2'];?></p>
        <a href="../php/index.php" class="post__link">Back to home</a>
    </article>
</div>
```
**Remarques**
Pour distinguer clairement les templates des pages, on peut utiliser la notation `nomDeMaTemplate.tpl.php`

## La date en PHP
```php
<time datetime="<?=$article['date'] ?>"> 
    le <?= date('d F Y', strtotime($article['date'])); ?>
</time>
```


# Étape 4

## Objectif
Rendre le menu de gauche dynamique

## Comment faire ?
1. Créer le tableau de données contenant les clé (nom d'affichage du lien) et les valeurs (les url respectifs)
    ```php
    <?php 

        $navigation = [ 
            'Plan du site' => '../php/index.php',
            'Mentions légales' => '../php/index.php',
            'Contact' => '../php/contact.php'
        ];
    ?>
    <nav>
        <ul class="left__nav">
        <!--  AFFICHAGE DE LA LISTE ('<li class="left__nav-item"><a href="'. $value .'" class="left__nav-link">'. $key .'</a></li> ')-->
            <?php foreach ($navigation as $key => $value) {
                  echo  '<li class="left__nav-item"><a href="'. $value .'" class="left__nav-link">' . $key . '</a></li>';
                }
            ?>
        </ul>
    </nav>
    ```
2. Isoler cette partie dans un template
3. Appeler le fichier dans la page cible


**Remarques**
1. Utiliser la notation raccourci de foreach
```php
<ul class="left__nav">
    <?php foreach($menu as $key => $value): ?>
    <li class="left__nav-item"><a href="<?= $value ?>" class="left__nav-link"><?= $key ?></a></li>
    <?php endforeach; ?> 
</ul>
```
2. Ne pas hésiter à faire des `var_dump()` pour visualiser les informations contenues dans le tableau


# Étape 5

##Objectif
Créer une page pour chaque article

## Comment faire ?

1. Inclure toutes les templates nécessaires 
2. Créer le tableau  `$article` contenant les données à afficher
```php
<?php
$article = [
    'title' => 'Lorem ipsum dolor article 1',
    'author' => 'Darren Collison',
    'text' => [
        'para_1' => 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat possimus sunt, deserunt ipsum molestiae vitae porro rerum quibusdam, earum deleniti nostrum itaque, doloremque libero quae distinctio necessitatibus inventore exercitationem excepturi aliquam. Dolores libero soluta porro delectus, minima fugiat ab eum iusto totam doloremque magnam harum quasi, eius deserunt laboriosam numquam, tempore obcaecati maxime ullam tenetur consectetur quidem! Nesciunt praesentium atque dolor amet adipisci aliquam et minus ipsa? Laborum optio harum libero? Veritatis ad maiores similique, ut minima consequatur, expedita fugiat provident cupiditate sequi exercitationem ullam delectus officia, omnis corrupti ratione deleniti? Harum accusantium est provident. Tenetur hic sapiente autem quidem harum mollitia eaque odio rem voluptatibus vero adipisci nesciunt ad accusantium aliquid ducimus, fuga excepturi cupiditate quaerat enim illum ullam illo nobis necessitatibus consectetur? Aut quos mollitia et qui obcaecati fugiat, autem quidem ea debitis consequuntur facilis veniam cupiditate. Sint iure ea quidem aliquid ipsum? Voluptate expedita similique impedit aspernatur? Maiores similique, ratione fugit excepturi iusto magnam, dolores nemo tenetur, pariatur eligendi sapiente asperiores unde. Ea quae nemo consequuntur libero. Vero hic, ipsam quas asperiores sit sed! Necessitatibus cupiditate reprehenderit mollitia ipsam vitae similique quam voluptate minima asperiores veritatis magni non repudiandae, laborum at iste! Illo minima ducimus provident cum autem beatae libero fugit doloribus error, nihil id quisquam ratione sunt architecto sequi numquam? Amet voluptatum obcaecati consectetur minus. Vel praesentium temporibus dolores ipsam?',
        'para_2' => 'Sequi qui, eveniet sunt ipsam ad porro aspernatur iste debitis quas dignissimos dolore facere magnam vero tenetur ipsa quidem laboriosam aliquid voluptatum a quo veritatis iure eos deleniti nesciunt? Molestias ab laudantium veritatis maiores eveniet tempora saepe rerum. Ratione autem expedita odit in quaerat exercitationem veniam, aut veritatis quasi beatae a obcaecati, iure minima? Iusto deleniti temporibus porro nemo, quod pariatur reiciendis corporis odio voluptas cum magni asperiores numquam delectus qui possimus laborum! Accusamus asperiores assumenda illum quisquam, magni consequuntur, natus quasi, ex reiciendis aspernatur labore? Maiores distinctio, a ratione eligendi temporibus perferendis odio beatae cupiditate sunt enim non repudiandae quod eius, aspernatur reiciendis accusantium debitis! Fuga voluptate magnam veniam, dignissimos unde ratione, consequuntur sapiente iste hic tempora suscipit doloremque, harum id incidunt voluptatibus aliquam neque eum fugiat! Temporibus deserunt, facere tempore qui ducimus maxime doloribus adipisci aut. Perferendis hic atque perspiciatis ipsum? Sunt, aliquid quos inventore tempora cum aspernatur iste pariatur ex libero est a, saepe porro. Dolor, accusantium voluptatem excepturi earum, perferendis dicta odit ad, nobis nostrum assumenda voluptas necessitatibus dolorum incidunt debitis voluptatibus!'
        ],
    'category' => [
        'class' => 'post__category post__category--color-team',
        'nom' => 'team',
        ] ,
    'date_publi' => [
        'date_robot' => '2018-02-10',
        'date_human' => 'le 10 février 2018',
        ],
    'img_author' => '../images/icon-dar.png'
];

require_once('inc/header.tpl.php');

require('inc/article.tpl.php');

require('inc/footer.tpl.php');

?>
```

# Bonus : Le formulaire

## Comment faire ?

Un formulaire est constitué de :
- La balise <form> 
```php
<form action="" class="">
</form>
```
- Les 3 grands types de saisie
    - les input
        - text
        radio
        email
        password
        submit
        ...
    - les select
        - permet d'afficher une liste déroulante avec les différentes options
    - les textarea
        -permet de saisir du texte dans un grand champ

- 
```php
<form action="" class="">
    <label> nom </label>
    <input type="text" name="myName"><input>

    <button>Envoyer</button>
</form>
```

```css
/* Contact */
.left--background-face {
  background-image: url(../images/face.jpg);
}

.contact-form {
  border: 1px solid #eaeaea;
  padding: 2em;
  margin: 2em;
  font-size: 0.8em;
}

.contact-form__row {
  display: flex;
  align-items: baseline;
}

.contact-form__row--bottom {
  border-bottom: 1px solid #eaeaea;
  padding-bottom: 12px;
  margin-bottom: 14px;
}

.contact-form__label {
  width: 10px;

  /* très petit, mais c'est un choix car [voir ligne suivante] */
  flex: 1;

  /* permet de dire aux items de s'agrandir en "récupérant" les espaces vides */
}

.contact-form__item {
  width: 10px;

  /* très petit, mais c'est un choix car [voir ligne suivante] */
  flex: 1;

  /* permet de dire aux items de s'agrandir en "récupérant" les espaces vides */
  background-color: #f9f9f9;
  border: 0;
  border-bottom: 1px solid #4cced3;
  padding: 3px 1px;
  margin: 4px;
}

/* exemple syntaxe ciblage input type "email" (attribut)
input[type=email] {
  width: 100%;
}
*/

.contact-form__item--textarea {
  height: 100px;
  padding: 1em;
}

.contact-form__item--checkbox {
  flex: 0 1 auto;

  /* je retire le flex-grow pour cet item */
  width: 1.5em;
}

.contact-form__submit {
  background-color: #4cced3;
  color: white;
  font-weight: 700;
  padding: 5px 10px;
  border-radius: 4px;
  border: 0;
  font-size: 1.2em;
}

```

##  Les méthodes $_GET et $_POST

Pour récupérer les données d'une requête HTTP, il existe actuellement 2 méthodes
```php
<form action="" method="GET">
</form>
<form action="" method="POST">
</form>
```
La méthode :
- GET : permet de passer des données dans une URL (format appelé query string). En utilisant cette méthode l'url se transforme en fonction des données passées : [...]/contact.php?firstname=Claire&lastname=Fortin&email=test%40o.io&source=fb&message=&file=
- POST :

**Remarques**
- dAN SUN CAS, LES FONFORMATIONS OSNT ENVOYÉES VIA L'URL DU NAVIGATEUR, DAN SL'AUTRE LES DONNÉES SONT "CACHÉES"
- Ainsi contrairement au GET le pOST est plus sécurisé car ses données sont transmises par la requête HTTP
- La attributs `name=""` seront utilisés en tant que clés dans les tableaux `$_GET` ou `$_POST` 

Pour récupérer les données on peut procéder en appelant la clé renseignée dans l'attribut name="" :
```php
$_POST['firstName'];
```

## Vérifier si une donnée/clé de tableau est vide ou non

Pour verifier si une donnée/clé d'un tableau est vide ou non 

```php
if( isset($_POST['firstName'])){
    echo 'Ok envoi de formulaire !';die; // die interrompt le chargement de la page après l'execution de la condition
}
```


```php
```