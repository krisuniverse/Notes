# Créer un tableau en PHP

## Le tableau indexé
Dans les tableau indexé, l'indexation est automatique :
    - 0 =>' valeur', 1 => 'valeur2', etc 
```php
$monTableau = ['0', '1', '2', 'carotte'];
```

## Le tableau associatif
Le tableau associtaif permet de créer ma clé au format `string`:
    - 'maclef' => 'mavaleur'
```php
$monTableau = [
    'Nom' => 'Doe',
    'Prenom' => 'John',
    'Age' => 20,
];
```

# La boucle foreach

- Récupérer la valeur
```php
foreach($monTableau as $chaqueElementDeMonTableau) {
    var_dump($value);
}
```

- Récupérer le clé et la valeur :
```php
foreach($monTableau as $cleDeMonTableau => $laValeurAssociee) {
    var_dump($laValeurAssociee);
}
```

**Visualiser le fonctionnement**
```php
foreach($abonnements as $key => $value){ 

  echo 'clef :' . $key . 'valeur:' . $value.'<br>';

}
```
> foreach($abonnements as $clefDeMonTableau => $saValeurAssociee){  recupere la clef ET la valeur de mon tableau }


Une autre écriture est possible pour simplifier la lecture
```php
<?php  foreach($abonnements as $key => $value):  ?>
        <li>Abonnement 5 places : -10%</li>
        <li>Abonnement 5 places -25ans : -20%</li>
<?php  endforeach; ?>
```

L'autre option (moins lisible) aurait été la suivante :
```php

```

# La commande echo raccourcie (openshorttag)
```php
<?php echo $maVariable ?>

<?= $maVariable?>
```



```php
```
```php
```