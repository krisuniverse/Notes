# Exercice

## Étapes possibles avant de faire un développement 

1. Définir le besoin ( ce que l'on souhaite avoir comme finalité)
2. Définir les données dont on va avoir besoin puis les transposer en variables
3. Créer le traitement à partir de ces données pour obtenir  le résultat souhaité

## Créer la div

```php
 <div style="width:10px; background-color:#000;" title="" data-color="" class="box"></div>
```

**Remarques**
- `day-color` est un attribut utile poiur spécifier la couleur lorsqu'on utilise javascript
- isoler ce que je sais faire (ex: la div), puis les données puis commencer le traitement


## Créer le tableau

```php
$colors = [
    '0','1','2','3','4','5','6','7','8','9','A','B','C','D','E','F'
]; 
```


## Créer la boucle
```php
for($i = 0; $i <= count($colors); $i++){

        echo '<div style="width:10px; background-color:#000;" title="" data-color="" class="box"></div>';
}
```
**Remarque**
`count()` permet de compter tous les éléments d'un tableau ou quelque chose d'un objet


## Inclure le php

À chaque boucle, la valeur de color est récupérée grâce à son positionnement dans l'index :
    - index 0  => $colors[0] => '0'
    - index 1  => $colors[1] => '1'
    - ...
    - index 15  => $colors[15] => 'F'

```php
for($i = 0; $i < count($colors); $i++){

        echo '<div style="width:10px; background-color:#' . $colors[$i] . $colors[$i] . $colors[$i] .';" title="" data-color="" class="box"></div>';
      }

```
**Remarque**
`str_repeat($colors[$i], 3);` permet de répeter la variable `$colors[$i]` 3 fois


## Calculer dynamiquement la taille des div
`calc()` permet d'effectuer des calcul en CSS

- Prendre la taille totale du tableau 
- Diviser la largeur de lla fenêtre par cette taille
- Retirer les marges (- 4px)

Pour faciliter la lecture, on va créer une varible intermédiaire `$width`

```php
$width = 100 / count($colors);
```

On va insérer cette varible dans la boucle

```php
for($i = 0; $i < count($colors); $i++){

    $hexaValue = $colors[$i] . $colors[$i]. $colors[$i]; // 111, 222 etc
    $width = 100 / count($colors);

    echo '<div style="width:calc(' . $width. '% - 4px); background-color:#' . $hexaValue .';" title="" data-color="" class="box"></div>';
}
```

## Solution de @eredost
```php
<?php $request = $bdd->query("SELECT value AS hexa_value FROM hexa_values") or die(print_r($bdd->errorInfo())); ?>

  <?php while ($data = $request->fetch()): ?>

        <div class="box" style="width:calc(100% / 16 - 4px);background-color:#<?= str_repeat($data["hexa_value"], 3);?>"></div>

  <?php endwhile ?>
  <?php $request->closeCursor(); ?>
```

# Bonus 1

Dans ce bonus, les 3 valeurs s'incrémentent.

 **A quoi peuvent correspondre ces 3 valeurs ?**
En couleur nous avons le système RGB  qui permet de composer toutes les couleurs possibles.

On aura donc 3 compteurs :
- `$r` pour l'index red
- `$g` pour l'index green
- `$b` pour l'index blue

L'affichage resemblera à `#$r . $g . $b`

`$nbColors = count($colors)` correspond au nombre de case dans le tableau

**Visualiser la logique**
```php
 $nbColors = count($colors); 

      for($r = 0; $r < $nbColors; $r++){

          for($g = 0; $g < $nbColors; $g++){

            //ex lors que $g = 2

            for($b = 0; $b < $nbColors; $b++){ //je souhaite afficher les valeur de 0 à F
              // alors je vais obtenir les valeurs suivantes : 20,21,22, 23, 24, 25... 2F

              echo 'r:'. $r . 'g:' .$g .'b:' .$b.'<br>'; 
            }

          }
      }

```
Si mon vert est égale à 0 je veux que $g aille de 0 à F pour 
```php

```

```php
```