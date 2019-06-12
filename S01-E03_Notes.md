# Mon fichier html
## réflexes
- lier le fichier à reset.css

## La barre de navigation
```
<nav>
    <a href=""> Lien 1 </a>
    <a href=""> Lien 1 </a>
    <a href=""> Lien 1 </a>
</nav>
```
## Insérer une image
```
<img src="../images/chaussons-oclock.gif" alt="" title="">
```
**Remarques**
- `alt` sert notamment aux liseuses et aux robots des moteurs de recherche (très pratique au niveau du SEO)
    - S'il s'agit d'une image décorative, pas besoin d'attribut `alt`
    - Si ces images ont une importances, alors ça peut être pertinent (exemple : schéma, graphique, etc)

- L'attribut `title` permet de faire apparaitre une petite bulle de texte lorsqu'on laisse le curseur de la souris sur l'image

# Mon fichier css
## réflexes
- lier le fichier à style.css
- définir dans body une police `font-family` et une taille `font-size` par défaut

## Utilisation d'une `div`
une div qui englobe une grosse partie de la page est généralement appelé container
```
<div class="container">
    <header></header>
    <main></main>
    <footer></footer>
<div>
```

Pour mettre une marge extérieur `margin` automatique :
```
.container {
margin: auto;
}
```
C'est le navigateur qui gère les marges et applique donc la même marge à gauche qu'à droite. `container` sera automatiquement centré

La taille de l'élément `<div class="container">` est égale à sa largeur + padding + border + margin

Pour que la largeur de l'élément corresponde à la largeur définie :
``` 
* { 
    box-sizing: border-box;
}
```
La largeur sera égale à `width`

` box-sizing: content-box` correspond à la valeur par défaut (ce qu'il se passe lorque je ne déclare pas box-sizing)


**remarque**
Si h1 est placé au-dessus de nav :
- si `nav { margin-top:16px }` et `h1 { margin-bottom: 16px}` alors la marge finale sera de 16 pixel
- si nav { margin-top: 20px } et h1 { margin-bottom: 16px} alors la marge finale sera de 20 pixel
- les marges ne se cumulent pas, il n'est pas utile de spécifier les 2 marges

## Changer le style de mes liens
```
a {
    text-decoration: none;
    color: #ED2350;
}
```
`text-decoration: none;` permet de supprimer la ligne en dessous du lien

```
a { 
    margin: 5px 0;
}
```
Il y aura une marge extérieur de 5px en haut et en bas et 0 à gauche et à droite

## Image
```
img {
    width: 500px;
}
```

En définissant uniquement la largeur ou la hauteur, la proportion est conservée.

Pour centrer mon image :
```
img {
    width: 400px;
    display: block;
    margin: auto;
}
```
La marge extérieur n'est présente que sur les côtés
```
img {
    width: 400px;
    display: block;
    margin: 10px auto;
}
```
Les `10px` correspond aux marges extérieurs haut et bas et `auto` correspond aux marges droite et gauche

Pour mettre une bordure :
```
img {
    border: 1px solid #000000;
}
```

Pour arrondir la bordure :
```
img {
    border-radius: 15px;
}
```

## Espacement des liens dans la barre de navigation
```
nav a {
    margin-right: 10px;
}
```

**remarques**
- le margin ne fait pas partie de l'élément, il est non-cliquable (c'est l'espace vital)
- le padding lui fait partie de l'élément, il est cliquable

### Mettre une marge sauf pour le dernier de son type
```
nav a:last-of-type {
    margin-right: 10px;
}
```

Tous les les `<a>` compris dans `<nav>` sauf le dernier auront un `margin-right` de `10px`

## Créer un lien vers une ancre

Le code HTML
```
<a href="#oclock"> O'clock </a>
<h1 id="oclock"></h1>
```

On peut utiliser sur un même élément :
- plusieurs class `clas=" container toto tutu titi"`
- des `id` des class sur le même élément