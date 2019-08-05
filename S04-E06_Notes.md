#PDO : PHP Data Object

[Fiche récap PDO](https://github.com/O-clock-Alumni/fiches-recap/blob/master/bdd/pdo.md)

[Doc officielle](https://www.php.net/manual/fr/book.pdo.php)


1. Se connecter
$dbh = new PDO('mysql:host=localhost;dbname=blog;charset=utf8', 'root', 'Ereul9Aeng', array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));

```php

// Établissement d'une connexion sur le socket MySQL.
$dsn = 'mysql:dbname=blog;host=localhost';
$user = 'oclock';
$password = 'oclock';

$conn = new PDO($dsn, $user, $password);
var_dump($conn);

var_dump($conn->query('select * from authors')->fetchAll());

```
2. Faire une requête 

DSN (data source name) : info concernat la BDD à laquelle on veut se connecter

en gros l'obejt PDO a plein de propriété et de méthode déjà créés
query c'est une méthode
du coup on a instancier la class PDO
dans $dbh
du coup pour faire une requête on va utiliser la méthode query()

Claudine
14:54
(mais c'est tellement génial 2 écrans !!!)

Heymi
14:54
(yeees)
du coup c'est $dbh->query($requete)
$requete = "SELECT * FROM authors"
par exemple

La méthode query() prépare la requête 

$resultat= $conn->query('select * from authors');
$res_requete = $resultat->fetchAll();

astuces
$res_requete = $resultat->fetchAll(PDO::FETCH_ASSOC);

pour afficher 


// Établissement d'une connexion sur le socket MySQL.
$dsn = 'mysql:dbname=blog;host=localhost';
$user = 'oclock';
$password = 'oclock';

$conn = new PDO($dsn, $user, $password);
var_dump($conn);

var_dump($conn->query('select * from authors')->fetch(PDO::FETCH_ASSOC));

une course de vélo, qui a lieu quelque part, avec un classement final. Commencer simple et complexifier étape par étape


Race : race_id, name, date, location
Racer: racer_id, first_name, last_name, address
Bike: bike_id, model, prod_year, color
Commissioner : com_id
History: racer_id, raceList, rankList, weightList, timeList

BELONGS TO, 11< Bike, 1n> Racer : bib_number, time, weighing 
TAKES PART TO, 1n< Racer, nn> Race
RANKING, 11 Race, 1n Racer : rankOfRacersByTime, rankOfRacersByAge
SENDS TO, 0n< Commissioner, 0n> Racer : rankings
USER_ACCOUNT, 01 Racer, 11 History