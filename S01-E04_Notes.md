# 1. La propriété Display

La propriété display définit le type d'affichage utilisée pour le rendu d'un élément. Ce type d'affichage possède deux composantes : 
- le type d'affichage extérieur (définit comment la boîte participe au flux)
- le type d'affichage intérieur (définit l'organisation des éléments enfants)

## 1.1 Les valeurs Display courantes :
```
display: block;
display: inline;
display: inline-block;
display: none;
```

### Block
Le `inline-block` ne provoque pas de retour à la ligne à la différence de `block` mais conserve toutes les propriétés de `block`.

**Remarque**
- Un élément block est souvent appelé un élément block-level

### Inline
Un élément inline n'interrompt pas le flux de son élément parent.

### None
`none` est une autre valeur display courante. Quelques éléments spéciaux comme script l'utilisent par défaut. 
 
 display: none; est très utile pour masquer ou afficher facilement des éléments en CSS ou en Javascripts sans avoir à les supprimer et les recréer.

**Attention !** 
Ne pas confondre `display: none;` et `visibility: hidden;` ! 
- `display: none;` masque totalement l'élément et annule des propriétés (margin, padding, width, height...)
- `visibility: hidden;` masque seulement l'élément, sans en annuler ses propriétés


# 2. Marges et taille maximum d'un élément

## 2.1 margin

```
#main {
  width: 600px;
  margin: 0 auto; 
}
```

## 2.2 max-width
```
#main {
  max-width: 600px;
  margin: 0 auto; 
}
```
Permet de fixer une limite maximum de largeur

## 2.3 box-model
```
.fancy {
  width: 500px;
  margin: 20px auto;
  padding: 50px;
  border-width: 10px;
}
```

## 2.4 box-sizing
```
.fancy {
    box-sizing: border-box;
}
```

# 3. La position d'un élément
## 3.1 static
```
.static {
  position: static;
}
```

## 3.2 relative
```
.relative1 {
  position: relative;
}
.relative2 {
  position: relative;
  top: -20px;
  left: 20px;
  background-color: white;
  width: 500px;
}
```
Par rapport à son placement d'origine: je vais demander à ce que relative2 se déplace de 20 vers le haut et de 20px vers la droite

## 3.3 fixed
Un élément positionné en `fixed` est positionné par rapport a la fenêtre du navigateur. Il reste donc toujours à la même place même si la page défile.

```
.fixed {
  position: fixed;
  bottom: 0;
  right: 0;
  width: 200px;
  background-color: white;
}
```

## 3.4 absolute
la valeur ``absolue` se comporte comme fixed, sauf qu'elle se base sur l'élément parent le plus proche qui est en `relative`.

```
.absolute {
  position: absolute;
  top: 120px;
  right: 0;
  width: 300px;
  height: 200px;
}
```
**Remarque**
- Un élément n'a pas forcément de parent `relative` mais il a toujours un parent (`<body>`)

## 3.5 exemple de position

```
.container {
  position: relative;
}
nav {
  position: absolute;
  left: 0px;
  width: 200px;
}
section {
  /* position is static by default */
  margin-left: 200px;
}
footer {
  position: fixed;
  bottom: 0;
  left: 0;
  height: 70px;
  background-color: white;
  width: 100%;
}
body {
  margin-bottom: 120px;
}
```
Ici le margin-left de section, lui permet de ne pas écraser la navigation qui mesure 200px (soit la taille du margin de section)

## 3.5 float
```
img {
  float: right;
  margin: 0 0 1em 1em;
}
```

## clear
Le HTML
```
<div class="box">...</div>
<section>...</section>
```
Le CSS
```
.box {
  float: left;
  width: 200px;
  height: 100px;
  margin: 1em;
}
.after-box {
  clear: left;
}
```
`after-box` va ignorer le float:let de box, ainsi la section after bix et la div ne se rencontreront pas.

## le hack clearfix

## Largeur en pourcent
```
article img {
  float: right;
  width: 50%;
}
```
le pourcentage se base sur l'élément parent

## media queries
```
@media screen and (min-width:600px) {
  nav {
    float: left;
    width: 25%;
  }
  section {
    margin-left: 25%;
  }
}
@media screen and (max-width:599px) {
  nav li {
    display: inline;
  }
}
```
Permet d'appliquer des propriété css en fonction des cas :
Dans cette exemple, cela donne :
> si la largeur d'écran est supérieur ou égale à 600px alors mon écran flotte à gauche et ma section a une margin de 25% 
> mais si latille est inférieur à600 px la navigation est inline

## inline-block
```
.box2 {
  display: inline-block;
  width: 200px;
  height: 100px;
  margin: 1em;
}
```
Plus besoin d'utiliser `clear`, contrairement à à la propriété `float`.
Cependant, cette propriété n'est pas supporté par tous les navigateurs. 

## colonne
```
.three-column {
  padding: 1em;
  -moz-column-count: 3;
  -moz-column-gap: 1em;
  -webkit-column-count: 3;
  -webkit-column-gap: 1em;
  column-count: 3;
  column-gap: 1em;
}
```
Pour tester la compatibilité on peut utiliser le site [Can I use...](https://caniuse.com/)

## flexbox
```
.container {
  display: -webkit-flex;
  display: flex;
}
nav {
  width: 200px;
}
.flex-column {
  -webkit-flex: 1;
          flex: 1;
}
```
[Guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
pour plus d'information

fonctionne globalement bien sur les différents navigateurs

L'idée est de déclarer une boite comme étant une boite flexbo
à partir de là on va aoir la possiblité deplacer ses éléments comme on le veut dan sla flex box
chaque éllément à l'interieur de cette boite est donc un flax-item

on va pouvoir décider de l'ordre des élément, dans quel sens, de quel côté, etc

par défaut tous les élément enfant de flexbox, cad les flex item auront tous par défaut lamême largeur

mais on ppeut décider viaw une proppété fflex-grow augmenter la taille d'un élément

on peut également utiliser flex-wrap pour autoriser le retour à la ligne des élément flex-item





les lééments layout sont de sgros élément dans la page. 






#Ressources
[Apprendre les mises en page CSS](http://fr.learnlayout.com/)
[Can I use...](https://caniuse.com/)
[Apprendre les flexbox](https://flexboxfroggy.com/#fr)
```
```

# Question-Réponse
- Q: Comment centrer le container ? => définir une `width` + ?
    - R: `margin:auto;`
- Q: Comment faire en sorte que le `padding` ne s'ajoute pas à la `width` du container ?
    - R: `box-sizing: border-box`;
- Q: D'ailleurs, définir la largeur du container avec width, est-ce une si bonne idée ?
    - R: non car on aura une scrollbar borizontale sur les écrans inférieur à cette largeur
    -   **astuce**: l'astuce c'est d'utiliser max-width à la place de width
- Q: Comment centrer le texte "Hero Corp" dans le <h1> ?
    - R: `text-align:center;`
- Q: Comment placer l'image "Hero Corp" à droite avec le texte auto
    - R: `float-right;`
