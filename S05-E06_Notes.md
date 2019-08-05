# 1-Séparer la configuration du code source

## 1. Créer un dossier config et y mettre database.ini
```
DB_HOST=localhost
DB_USERNAME=oshop
DB_PASSWORD=oshop
DB_NAME=oshop
```
le mttre dabs .gitignore car on ne veut pas l epusher
```
/config/database.ini
```

## 2. Créer un database.dist.ini (un fichier de config vide)
```
DB_HOST=
DB_USERNAME=
DB_PASSWORD=
DB_NAME=
```

## 3. Créer un dossier Utils et y mettre DBData.php
[Fonction parse_ini_file](https://www.php.net/manual/fr/function.parse-ini-file.php)

prend en charge un fichier et le transforme en tableau

instanciayion de PDO dans le construct de la classe DBData

## 4. instancier la class DBData dans les controllers
```php

require_once __DIR__ . "/../Utils/DBData.php";

class MainController 
{
    public function home($params) {
        $dbData = new DBData();
        $categories = $dbData->getHomeCategories();

        $this->show('home');
    }

    private function show($templateName, $templateVars = array()) {
        include(__DIR__ . '/../views/header.tpl.php');
        include(__DIR__ . '/../views/' . $templateName . '.tpl.php');
        include(__DIR__ . '/../views/footer.tpl.php');
    }
}
```
#2-Récupérer les données 
Dans DBData.php

## Récupérer les catégories à afficher sur la home
```php
    /**
     * Méthode permettant de retourner les 5 catégories sur la page d'accueil
     *
     * @return Category[]
     */

    public function getHomeCategories() {

        $sql  = "SELECT * 
                    FROM category 
                    WHERE home_order != 0 
                    ORDER BY home_order 
                    LIMIT 5 
                ";

        $pdoStatement = $this->pdo->query($sql);

        $results = $pdoStatement->fetchAll(PDO::FETCH_CLASS, 'Category');

        return $results;
    }
```
**remarques**
- fetchAll prend dans notre cas 2 paramètres : le fetch style(`PDO::FETCH_CLASS`) et la classe (`'Category'`) à instancier pour chaque élément de la table
- fetchAll est une méthode de l'objet PDOStatment
- query est une méthode de l'objet PDO


#3-Passer les données au controller

Dans les controller (MainController.php)

On va utiliser le deuxième argument de la méthode show pour stocker les données utiles
```php
class MainController {
    public function home($params) {
        $dbData = new DBData();
        $categories = $dbData->getHomeCategories();

        $this->show('home', array('categories' => $categories));
    }
}
```
**remarques**
- `array('categories' => $categories)` est un tableau qui contient un tableau

#4-Affichage 

- Utiliser le tableau $templateVars dans la template home.tpl.php

```php
        <?php foreach($templateVars['categories'] as $index => $category) : ?>

        // structure html qui affiche la catégorie

        <?php endforeach; ?>
```

```php
// tableau sur lequel boucler
$templateVars['categories']

// index va nous ervir à différencier l'affichage des catégories (grandes div vs petites div)
as $index 

// $category est une instance de la classe Category, on peut donc accéder à ses propriétés via les getters
$category
```

```php
```

```php
        <?php foreach($templateVars['categories'] as $index => $category) : ?>

        // structure html qui affiche la catégorie

        <?php endforeach; ?>
```
**remarques**
- penser à modifier le chemin de picture dans la BDD

## Conditionner "la taille" des div catégories
```php
        <?php foreach($templateVars['categories'] as $index => $category) : ?>

            <?php if($index >2) : ?>
                // structure html avec les grandes div

            <?php else : ?>
                // struture avec html les petites div
            <?php endif; ?>

        <?php endforeach; ?>
```

## Résultat final
```php
<section>
    <div class="container-fluid">
      <div class="row mx-0">


        <?php foreach($templateVars['categories'] as $index => $category) : ?>

          <?php if($index < 2) : ?>
            <div class="col-md-6">
              <div class="card border-0 text-white text-center">
              <img src="<?= $_SERVER['BASE_URI'] . "/" . $category->getPicture() ?>"
                  alt="Card image" class="card-img">
                <div class="card-img-overlay d-flex align-items-center">
                  <div class="w-100 py-3">
                    <h2 class="display-3 font-weight-bold mb-4"><?= $category->getName() ?></h2><a href="category.html" class="btn btn-light"><?= $category->getSubtitle() ?></a>
                  </div>
                </div>
              </div>
            </div>

          <?php else : ?>   
          
            <div class="col-lg-4">
              <div class="card border-0 text-center text-white"><img src="<?= $_SERVER['BASE_URI'] . "/" . $category->getPicture() ?>"
                  alt="Card image" class="card-img">
                <div class="card-img-overlay d-flex align-items-center">
                  <div class="w-100">
                    <h2 class="display-4 mb-4"><?= $category->getName() ?></h2><a href="category.html" class="btn btn-link text-white"><?= $category->getSubtitle() ?>
                      <i class="fa-arrow-right fa ml-2"></i></a>
                  </div>
                </div>
              </div>
            </div>

          <?php endif ?>

        <?php endforeach; ?>

      </div>
    </div>
  </section>
```
# Tuto : Mettre à jour des données du la BDD

dans notre cas l'url de l'image est fausse (img au lieu de images)
Aller sur phpmyadmin
```sql
UPDATE product
SET picture = REPLACE(picture,'/img','/images')
--- optionnel (dû à une protection de workbench)
WHERE id != 9999
```
```sql
UPDATE category
SET picture = REPLACE(picture,'/img','/images')
--- optionnel (dû à une protection de workbench)
WHERE id != 9999
```

# Questions des helpeuses
## try catch

le bloc try{} : si jamais il y a un problème à l'intérieur, ça va leve rune exception (un object qui contient les raisons de l'erreur) Pour capturer cette erreur on va utiliser throw
si dan smon bloc try je soulève une eception(trhrow) je passe dan sle bloc catch{}

La getsion de lexception se fait dan sla partie ctach {}


**inès**
ok donc c'est un throw exception mais en 2 étapes, le bloc à analyser et le bloc d'erreurs (si on a des erreurs ?)
```php
        try {

            $exception = new Exception("J'ai pas reussi a me connecter car patati patata");

            throw $exception;
            
            $this->pdo = new PDO(
                "mysql:host={$configData['DB_HOST']};dbname={$configData['DB_NAME']};charset=utf8",
                $configData['DB_USERNAME'],
                $configData['DB_PASSWORD'],
                array(PDO::ATTR_ERRMODE => PDO::ERRMODE_WARNING) // Affiche les erreurs SQL à l'écran
            );
        }
        catch(\Exception $exception) {
            echo 'Erreur de connexion...<br>';
            echo $exception->getMessage().'<br>';
            echo '<pre>';
            echo $exception->getTraceAsString();
            echo '</pre>';
            exit;
        }
    }
```

## fetchAll vs setFetchMode

setFetchMode permet de configurer les fetch à venir pour un objet donné

```php
$sql  = "SELECT * 
            FROM category 
            WHERE home_order != 0 
            ORDER BY home_order 
            LIMIT 5 
        ";

$pdoStatement = $this->pdo->query($sql);

$pdoStatement->setFetchMode(PDO::FETCH_CLASS, 'Category');

$results = $pdoStatement->fetchAll();
$pdoStatement->fetch()

return $results;
```

# résumé

La class DBData gère la connection à la BDD et la récupératin des données.

DBData va donc servir à associer les propriétes aux valeurs récupérées dans la BDD. 

Les classes sont comme des penderies vides. Les propriétés sont des cintres. DBData (via PDO) sert à récupérer les vêtements (données). Grâce à fetchAll(PFO::FETCH_CLASS, 'nomDeTaClasse'), on va enfiler les vêtements sur les cintres(propriétés)

La méthode query renvoie un PDO statement qui contient les donées

PDOstatement fait le lien entre le nom des propriétés et le nom des colonnes

- FETCH_CLASS est un fetch style (une constante de PDOstatement qui permet de décrire le type de résultat)


si le nom de la propriété ne correspond pa sua nom de la colonne dans la BDD, il ajoute une proriété à la classe. La prooriété qui est vide (car pas de correspondance avec une colonne) aura pour valeur null;


# Héritage

[Fiche recap](https://github.com/O-clock-Alumni/fiches-recap/blob/master/php/heritage.md)
Dans Model > CoreModel.php
Créer la class

```php

// Dans CoreModel.php
class CoreModel 
{
  // propriétés communes à tous les models

  // getters et setters communes à tous les models
}


// Dans Brand.php (ou tout autre model)
require_once __DIR__ . "/CoreModel.php";

class Brand extends CoreModel
{
  //...
}
```

Une classe ne peut hériter d'une clase à la fois, mais on peut faire un héritage en waterfall

Protected (accessible par la classe mère et les enfants), si on avait mis la propriété en privée


# challenge de ce soir
```php
// dans Controller > CoreController.php
class CoreController {
      protected function show($templateName, $templateVars = array()) {
        include(__DIR__ . '/../views/header.tpl.php');
        include(__DIR__ . '/../views/' . $templateName . '.tpl.php');
        include(__DIR__ . '/../views/footer.tpl.php');
    }
}

// dans MainController
require_once __DIR__ . "/CoreController.php";
class MainController extends CoreController {
  // supprimer la méthode show
}
```

# Signleton

Le problème avec l'instanciation de la classe DBData, on va se connecter à la BDD. Donc à chaque nouvelle instanciation on multiplie les connexions à la BDD. Pour éviter cela on va empecher l'instanciation :
```php
private function __construct() {}
```

L'intanciation n'est possible que dans la classe elle-même, car le constructeur est privé

On crée un getter pour vérifier si l'instance est instancier 
```php
	/** 
     * @var DBData 
     */
	private static $instance;

    /**
     * Constructeur se connectant à la base de données à partir des informations du fichier de configuration
     */

    static public function getInstance() {
        if(empty(self::instance)) {
            $instance = new DBData();
        }
        return $instance;
    }
```
**remarques**

- grâce à private la variable $instance n'est accessible que dans DBData
Dans MainController

- static  fait référence à la classe-type de l'objet sur lequel est appelée la méthode. (cette partie n'est pas instanciée)

Comme la varaible est static elle est accessible via la classe, mais comme elle est privée on ne peut y accéder qu'au sein de la classe

```php

require_once __DIR__ . "/../Utils/DBData.php";
require_once __DIR__ . "/CoreController.php";

class MainController extends CoreController
{
    public function home($params) {
        $dbData = DBData::getInstance();
        $categories = $dbData->getHomeCategories();

        $this->show('home', array('categories' => $categories));
    }
}
```

Et pour récupérer la propriété statique d'une classe parente on utilise le mot clé "parent::"