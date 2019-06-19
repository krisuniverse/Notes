# Exercice 1 : Les variables

Définir une variable
```php
$maVariable = 45;
```

# Exercice 2 : Les calculs

Faire un calcul
```php
// En utilisant uniquement les variables suivantes, créer une variable "calculC" ayant la valeur CALCULEE suivante : 26
$a = 5;
$b = 8;
$c = 3;
$d = 9;

$calculC = ($d * $a) - ($b * $c) + $a;
```

# Exercice 3 : Les conditions

## Exercice A 

```php
$estAdulte = null; 

if ($age >= 18) {
    $estAdulte = true;
} else {
    $estAdulte = false;
}
```

**Remarques**
- `null` ne veut pas dire 0 ou false 
- `null` est un type à part qui veut dire **vide**


## Exercice B
1. Découper le traitement
    ```php
    if( $age >= 18 ){ 

        $estAdulte = true;
        $estEnfant = false;

    } else {

        $estAdulte = false;
        $estEnfant = true;
 
    }
    ```

2. Tester si en plus de son statut (Adlute/Enfant) si il s'agit d'un adolescent 
```php
if($age >= 10 && $age <= 19){ // comprend 10,11,12,13,14,15,16,17,18,19

    $estAdolescent = true;
} else {
    $estAdolescent = false;
}
```



## Exercice bonus
```php

if( $age <= 6 ){ //si mon enfant à 6 ans ou moins
    
    $protectionMaternelleEtInfantile = true;
    $creche = false;
    $halteGarderie = true;
    $jardinDEnfants = true;
    $jardinDEveil = true;
    $assistanteMaternelle = true;
    $ecoleMaternelle = false;
    $centreDActionMedicoSocialePrecoce = true;

    if($age <= 3) { //si mon enfant à moins de 7 ans et qu'il a 3 ans ou moins  = creche

        $creche = true;
    }

    if( $age >= 2 ){ // si mon enfant à 6 ans ou moins, 3ans ou moins mais a au moins 2ans 
        $ecoleMaternelle = true;
    }
} else {
     
    $protectionMaternelleEtInfantile = false;
    $creche = false;
    $halteGarderie = false;
    $jardinDEnfants = false;
    $jardinDEveil = false;
    $assistanteMaternelle = false;
    $ecoleMaternelle = false;
    $centreDActionMedicoSocialePrecoce = false;

}
```

**remarques**
- Si il y a plusieurs conditions, PHP rentrera uniquement dans la condition qui correspond à la situation
- Il n'executera pas les autres conditions
- Il procède à l'examen des conditions dans l'ordre


# Exercice 4 : La concatenation

## Exercice A

```php
$bestVideoGames1 = 'les meilleures portables sont ' . $videoGamesPortable . '.';
```
**Remarques**
- Lorsqu'on utilise  les double quotes, les opérateurs logiques et mathématiques ne sont pas évalués
- Seules les variables sont évaluées


## Exercice B
```php
$bestVideoGames2 .= ', et ' . $bestVideoGames1;
```
`.=` signifie que je souhaite concatener ma variable actuelle avec la chaîne qui suit

La ligne précédente est l'équivalent de la ligne qui suit
```php
$bestVideoGames2 = $bestVideoGames2 . ', et ' . $bestVideoGames1;
```

# Exercice 5 : Le megamix

```php
if($age < 14 ){ //(pour -14ans)

		$montant = $tarifEnfant;

	} elseif ($age > 60 || $age < 16 ) {
		 //(pour +60ans et -16ans)
		$montant = $tarifReduit;

	} else {
		$montant = $tarifPlein;
	}

```

**Qu'est ce qu'un argument ?**
Les arguments permettent de passer une valeur de façon dynamique (code générer par l'utilisateur)

```php


$ageArgv = $argv[1]; // ici je recupere la valeur située dans la zone 1 visible dans ma console avec var_dump()
```
Pour passer une valeur dynamique manuellement a l'appel de mon script dans ma console : `php script.php value1 value2`

```php
var_dump($argv);
$ageArgv = $argv[1];
```


# Commandes sur le terminal
## Executer les fichiers en ligne de commande

- Variables : php -f exos/01-variables.php
- Calculs : php -f exos/02-calculs.php
- Conditions : php -f exos/03-conditions.php
- Concaténation : php -f exos/04-concatenation.php
- Exercice : php -f exos/05-megamix.php

## Réutiliser une commande

1. Saisir `history` sur le terminal
```
mint@amy-ndiaye /var/www/html/S02 $ history
```
2. L'historique des commandes utilisées va apparaître
```
.....
11731 git add.
11732 git commit -m "Ceci est un message"
11733 git push
.....
```
3. Il suffit alors d'écrire le numéro de la commande précédé d'un point d'exclamation `!11733`
```
mint@amy-ndiaye /var/www/html/S02 !11733
mint@amy-ndiaye /var/www/html/S02 git push
```

# Ressources
[Réaliser un calcul avec des nombres imposées](https://www.dcode.fr/compte-est-bon)