# Remarques générales
- Par défaut, Localhost (i.e Apache) va chercher le dossier html ou le dossier php
- Dorénanvant, l'intégration se fera dans le fichier index.php
- Apache est capable de lire le html dans le fichier .php
- En revanche, le navigateur n'est pâs capable de lire le PHP
- Apache lis le PHP. Le PHP crée le HTML. Le HTML appelle le CSS


# Exercice Places de cinéma

## Étape 1
### L'inclusionde code php et les templates

1. Créer un dossier templates à la racine
    - on y trouvera les modèles qui serviront à l'intégration de la page

2. Créer les templates et y placer le code adéquat
    - nav.php

3. Dans le document index.php, créer les inclusions de code PHP
    - Pour appeler une template
    ```php
    <?php
    require('../dosisserParent/monfichier.php');
    require('../templates/nav.php')
    ?>
    ```

**Remarques**
- Les templates facilitent la maintenance. Pour changer le code sur toutes les pages qui l'utilise, il suffit de modifier la template.
- `require` est une fonction PHP

### Inclure le challenge (Tarifs en fonction de l'âge)
```php
<p>
    <?php 
        
        $montant = 0;
        $is3D = true;
        $age = 43;

        $tarifPlein = 8.3;
        $tarifReduit = 6.8;
        $tarifEnfant = 4.5;
        
        //tarif en fonction de l'âge
        if ($age < 14) {

            $montant = $tarifEnfant;
        }

        else if ( $age < 16 || $age > 60) {
            
            $montant = $tarifReduit;
        }

        else {
            $montant = $tarifPlein;
        } 

        //supplément 3D = 1€
        if ($is3D == true) {

            $montant += 1;
        } 

    ?>

    Tarif du capitaine (€): <?php echo $montant ?>

</p>
```

## Étape 2

### Les boucles en PHP

- La boucle **while**
Cette boucle effectue l'instruction _tant que_ la condition est vraie

- La boucle **for**
Cette boucle effectue l'instruction un certainnombre de fois "pour"

- La boucle **foreach**
Cette boucle est spécéfique aux tableaux


### La boucle **while**

Tant que je suis en égale ou inférieur 99, j'effectue l'instruction.

Pour éviter, un boucle infinie on va définir une valeur de départ à la variable à tester

```php
$ageToTest = 1;

while(mavaleur <= 99) {

    $ageToTest += 1;
}
```

On veut que le tarif soit affiche de 1 à 99 ans. je veux donc que le montant revienne à 0 à chaque nouvelle personne 

```php
<?php

    $ageToTest = 1;

    while($ageToTest <= 99) {
          $montant = 0;
          $is3D = true;

          // traitement Tarif en fonction de l'âge
          if ($age < 14) {

            $montant = $tarifEnfant;
          }

          else if ( $age < 16 || $age > 60) {
            
            $montant = $tarifReduit;
          }

          else {
            $montant = $tarifPlein;
          } 

          //supplément 3D = 1€
          if ($is3D == true) {

            $montant += 1;
          } 
        
        echo "Si la personne a l'âge suivant : $ageToTest le tarif est de $montant <br>";

        $ageToTest += 1; // équivaut à $ageToTest ++
    }
?>
```

## Étape 3

### Les tableaux

```php
$monTableau = ['valeur 1', 2, 'carotte'];
```
Les tableaux commence à 0, ici la dernière case a pour indice 2

Afficher le contenu d'une cellule 
```php
echo $movieList[5];
```

### La boucle **for**

La boucle for a besoinde 3 éléments pour fonctionner :
- la valeur de départ
- la condition
- le pas

```php
for ($maValeurInitiale; $maValeurInitiale < $nombreTotalDeTour; $iteration++ )
```