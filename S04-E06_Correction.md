# Interface de gestion de jeux vidéo

- affichage de la liste des jeux vidéo (TODO #1)
- tri de cette liste (TODO #2)
- ajout d'un jeu vidéo (TODO #3)
- liste des plate-formes (consoles de jeu) dynamique (depuis la DB) (TODO #4)


## TODO 0 : Importer la bdd et établir la connexion
1. Copier le contenu de `videogame.sql` et coller la requête dans __Requête SQL__ (à gauche)

2. Établir la connexion 
Avant de pouvoir procédé aux TODO suivants, il faut établir une connetion entre la BDD et le serveur.

Dans le fichier db.php, saisir les instructions suivantes :
```php
$host = 'localhost';
$dbname = 'videogame';
$user = 'videogame';
$password = 'videogame';

$pdo = new PDO('mysql:host=' . $host . ';dbname=' . $dbname, $user, $password);
// DSN (Data Source Name) : 'mysql:host=localisationDeMySQL;dbname=nomDeLaBase
```
**Remarques** 
- La classe PDO est natif à PHP
- L'organisation des fichiers suit la logique suivante :
    - fichier de connexion à la BDD : `db.php`
    - fichier d'utilisation de la BDD : `index.php`
    - fichier de gestion de l'affichage : `videogame.php`

## TODO 1 :

**Plan d'attaque**
1. Se connecter à la base de données avec un instanciation de la classe PDO(TODO 0)
2. Écrire la requête SQL permettant de récupérer les jeux vidéos dans $sql
3. Exécuter la requête contenue dans $sql
4. Boucler sur le tableau contenat l'étape 3



__Sur index.php__
- Saisir et récupérer la requête SQL
```php
// écrire la requête SQL
$sql = '
    SELECT * FROM videogame 
';
// exécuter la requête
$videogameList = $pdo->query($sql)->fetchAll(PDO::FETCH_ASSOC);
```
**Remarque :**
La méthode query() "prépare" la requête, pour exécuter la requête il faut utiliset la méthode fetch() ou ses variaiantes (fetchAll(), fetchColumn(), etc)

__Sur index.php__
```php
<?php foreach($videogameList as $result) : ?>
    <tr>
        <td><?= $result['id'] ?></td>
        <td><?= $result['name'] ?></td>
        <td><?= $result['editor'] ?></td>
        <td><?= $result['release_date'] ?></td>
        <td><?= $platformList[$result['platform_id']] ?></td>
    </tr>
<?php endforeach; ?>
```

## TODO 2 :

**Plan d'attaque**
1. Tester la présence de query parameters dans $_GET (`!emty()`)
2. Si c$_GET n'est pas vide, tester $_GET['order'] 
    - si la valeur est `name`, faire le tri par nom (ordre croissant)
    - si la valeur est `editor`, faire le tri par éditeur (ordre croissant)

```php
$sql = '
    SELECT * FROM videogame
';
// --- END OF YOUR CODE ---

// Si un tri a été demandé, on réécrit la requête
if (!empty($_GET['order'])) {
    // Récupération du tri choisi
    $order = trim($_GET['order']);
    if ($order == 'name') {
        // TODO #2 écrire la requête avec un tri par nom croissant
        // --- START OF YOUR CODE ---
        $sql = $sql . ' ORDER BY name ASC';
        // --- END OF YOUR CODE ---
    }
    else if ($order == 'editor') {
        // TODO #2 écrire la requête avec un tri par editeur croissant
        // --- START OF YOUR CODE ---
        $sql = $sql . ' ORDER BY editor ASC';
        // --- END OF YOUR CODE ---
    }
}
```

## TODO 3 :

**Plan d'attaque**

```php
if ($name != '' && $editor != '' && $release_date != '' && $platform != '') {
    
    // Insertion en DB du jeu video
    $insertQuery = "
        INSERT INTO videogame (name, editor, release_date, platform_id)
        VALUES (:name, :editor, :release_date, :platform_id)
    ";
    // TODO #3 exécuter la requête qui insère les données
    // TODO #3 une fois inséré, faire une redirection vers la page "index.php" (fonction header)

    $statement = $pdo->prepare($insertQuery)
    $statement->execute([
        'name' => $name,
        'editor' => $editor,
        'release_date' => $release_date,
        'platform_id' => $platform
    ]);


}
```
**Note**
Pour les insertions, il faut utiliser la méthode exec(). Pour les requêtes basiques, on utilisera qla méthode query();
la méthode prepare() va "assenir" les informations à envoyer dans la base (bon en matière de sécurité)

Lecture : on considère que la requête est fiable donc query() + fetch() (léger, pas sécurisé, une seule utilisation)
Ecriture : il faut s'assurer de l'intégrité des données envoyé à la BDD, on va donc 

**questions**
et bindValue() ça fait la même chose que le tableau passé en argument dans la méthode execute ? 
## TODO 4 :


**Plan d'attaque**
1. Récupérer la table platform
2. Récupérer dans $key la clé de ta table platform
3. Récupérer dans $value le nom de la platform qui correspond à la $key
4. Dans $platformList, associer la clé $key au bon nom $value 

```php
$sqlPlatforms = 'SELECT * FROM platform'; // expression d'une requête SQL
$statement = $pdo->query($sqlPlatforms); // préparation de la requête SQL


$results = $statement->fetchAll();
$platformList = [];

foreach($results as $result) {
// À chaque tour de boucle, je suis entrain de traiter un des résultats.
// Le résultat m'a été envoyé sous forme d'un tableau associatif :
// j'en extrait les informations qui m'intéressent…
$key = $result['id'];
$value = $result['name'];
    // … je balance ces informations dans un autre tableau, plus simple,
    // qui sera exploité par le template videogame.php
$platformList[$key] = $value;
}
```

Une version plus simple existe :
```php
$sqlPlatforms = 'SELECT * FROM platform'; // expression d'une requête SQL
$statement = $pdo->query($sqlPlatforms); // préparation de la requête SQL
$platformList = $statement->fetchAll(PDO::FETCH_KEY_PAIR);
```

```php
```

```php
```



## Échange client-serveurfrontal-bdd

**Explication de Claudine the Queen** :
Je suis un client dans un restau chinois, je vais commander ma boisson et mon plat au comptoir, le barman Apache peut me servir direct mais il va passer en cuisine derrière pour dire en chinois au cuistot qu'il faut un plat
et c'est le commis qui va rapporter le plat une fois prêt au barman qui le rapporte au client


## Rappel : les conditions ternaires
```php
// condition ternaire
$name = isset($_POST['name']) ? $_POST['name'] : '';

// équivalent avec une condition if/else
if(isset($_POST['name'])) {
    $name = $_POST['name'];
} else {
    $name = '';
}
```