

# Installer l'extension Stylelint
[Stylelint](https://github.com/O-clock-Alumni/fiches-recap/blob/master/css/stylelint.md)
Permet de vérifier la syntaxe CSS

#.gitignore
Tous les fichiers listés dans `.gitignore` seront ignorés par Git

Ignorer tous les fichiers qui ont l'extension `.log`
```
*.log
```

# Passer de 3 à 6 produits 
1. Dupliquer la `<div class="row">` pour ajouter les 3 nouveau produit


# Ajouter le décor au dessus du titre

```
.selection-title {
    ...
  background-image: url('../images/deco.png');
  background-repeat: repeat-x;
  padding-top: 2em;
}
```
# Ajouter une ombre portée

```
. { 
    box-shadow: 10px 5px 5px red;
}
```
La propriété box-shadow peut être définie grâce :

À deux, trois ou quatre valeurs de longueur (`<length>`) :
Avec deux valeurs, celles-ci sont respectivement considérées comme les coordonnées de décalage de l'ombre : `<offset-x>` et `<offset-y>`
Si une troisième valeur est fournie, celle-ci correspondra au rayon du flou : `<blur-radius>`
Si une quatrième valeur est fournie, celle-ci correspondra au rayon d'étalement : `<spread-radius>`.
Au mot-clé optionnel inset
À une valeur de couleur (`<color>`) optionnelle.

[Box-shadow via MDN](https://developer.mozilla.org/fr/docs/Web/CSS/box-shadow)


#  Le -20%

L'élément absolu se positionne devant les autres éléments (au premier plan)

L'élément va se placer de manière absolue dans le dernier élément relatif de la page
```
.product {
  ...
  position: relative;
}
.product__sales {
  position: absolute;
  top: 10px;
  right: 10px
}
```

Pour faire le cercle, il faut créer un carré puis donner un radius de 50%
```
.product__sales {
  width: 70px;
  height: 70px;
  line-height: 62px;
}
```

Pour centrer le texte, l'une des solution est de faire :
```
.product__sales {
  width: 70px;
  height: 70px;
  line-height: 62px;
}
```

# L'étiquette soldes

L'étiquette st purement décorative, on la met donc en dernier dans `body`.

Le HTML
```
<div class="fixed-sales">
    <a href="soldes.html" class="fixed-sales__link">Soldes</a>
  </div>
```
Le CSS
Si je souhaite positionner mon élément parfaitement au milieu de ma page; je dois prendre la hauteur de ma boîte, la diviser par 2, et enlever cette moitié à mes 50%.

En css il est possible de réaliser quelques opérations simples
```
.fixed-sales {
    top:calc(50% - 51px);
}
```
Changer l'orientation du texte
```

```
Si deux éléments se superposent, on peut changer l'ordre d'apparitoion dans la structure html ou utilise la propriété z-index. (Éviter d'avoir à l'utiliser)
```
element {
    z-index: 100;
}
```
```
```