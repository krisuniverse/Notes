# Agrandir la taille au survole d'un élément

## Augmenter la taille
La propriété `transform` permet de modifier l'espace de coordonées utilisé pou rla mise en forme visuelle.
```
.gallery__thumbnail:hover {
  transform: scale(1.4);
}
```
**Remarque**
- La fonction `scale()` modifie la taille de l'élément

## Augmenter la taille de façon progressive
Rendre le grossisement progressif
```
.gallery__thumbnail{
  transition: 1.5s;
}
```
**Remarques**
- Toutes les transition de mon élément prendront 2sec
- En mettant la transition hors du :hover, la transition se produit quoiqu'il arrive


**Ressources**

[Transition en CSS](https://developer.mozilla.org/fr/docs/Web/CSS/transition-timing-function)

# Faire une rotation au survole d'un élément

## Faire une rotation 
```
.socials__icon:hover {
  transform: rotate(360deg);
}
```

## Faire une rotation avec un agrandisement
```
.socials__icon {
  transition: transform 1s;
}
.socials__icon:hover {
  transform: rotate(360deg) scale(2);
}
```

## Appliquer des filtres sur un élément

## Le mettre en nuance de gris
Par défaut le camélon est en noir et blanc
```
.cam-of-the-week__image {
  filter: grayscale(100%);
}
```
```
.cam-of-the-week__image:hover {
  filter: grayscale(0%);
  transition: ease 3s;
}
```
## Floutter l'arrière plan
Dans cette exemple, je floute le `container`
```
.container {
    filter: blur(10px)
}
```

## Appliquer plusieurs transitions sur 1 élément

Ici, la bordure n'a pas la même durée de transition que le reste de `<aside>`
```
aside:hover {
  transform: scale(1.2);
  border: 1px solid red;
  transition:
    transform ease 2s,
    border ease 5s;
}
```


## Créer une animation

`@keyframes` permettent de gérer le déroulement de l'animation de manière plus précise qu'avec la propriété `transition`

### Faire "disparaitre" puis "réaparaitre" mon élément 
```
@keyframes heartbeat {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
```
`opacity: 0;` le rend transparent et `opacity: 1;` le rend totalement opaque

### Apliquer l'animation à mon élément

```
.heart {
  animation-name: heartbeat;
  animation-duration: 0.5s; 
  animation-iteration-count: infinite;
  animation-direction: alternate;
}
```
**Remarque**
- ` animation-name: heartbeat;` est le nom de l'animation à appliquer
- `animation-duration: 0.5s;` correspond à la durée de l'animation
- `animation-iteration-count: infinite;` permet de faire une boucle infinie
- `animation-direction: alternate;` l'animation fait des aller-retours


# Liens utiles
[La Bible des liens](https://github.com/TaLoche/Helpdesk/blob/master/Liens/Liens.md)

```
```

# Le responsive web design

## 1. C'est quoi le responsive ?

## 2.Les solutions

### 2.1 Mobile/device specific
Application ou site dédié mobile

### 2.2 L'adaptive design
Détection de l'appareil et chargement de contenus ou templates adaptés. Servver-side et/ou client-side. 
Le résultat ressemble au responsive.

### 2.3 Le responsive design (slide 9)
Utiliser CSS pour adapter laprésentation des contenus à la taille et aux caractéristiques du device

**Problème de performance** car le téléphone télécharge tous les éléments puis les masque à mesure qu'il télécharge le code CSS. Mais ce problème tend à disparaitre.

## 3. Les 5 étapes du responsive design

### 3.1 Les metaviewport
Dans le `<head>`
```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### 3.4 Les médiaqueries
Les média queries permettent de dire la chose suivante au navigateur :
> " Au delà de telle taille, comporte-toi comme ça"

### Taille de texte flexibles

Les `em` et les `rem`

## Fluid layout
les % et les vh sont des unités relatives, elles se basent sur la taille de l'écran

## Images flexibles
`max-width` permet de fixer une taille maximum à son image. Elle sera limitée à la taile de son conteneur

## Media queries
Pemrttent de fixer des breakpoints (poinst de rupture)
>"Au-delà de telle taille d'écran on fait ça "

## Responsive font sizes

- Cible: valeur en px (dans body)
- Contexte: taille par défaut ou taille du parent
- Résulat = taille en `em` ou en `rem`

## Meta "viewport"

On déclare la façont dont le navigateur doit se comporter par rapport au device

## Exemple

Le mobile first est une façon de coder qui implique de commencer l'intégration par le mobile puis d'agrandir progressivement (ex: téléphone > tablette > desktop)

Il est plus facile d'ajouter un élément que de le supprimer.

### Cibler un élément avec ` mediaqueries`
Je cible le premier élément qui a la classe "gallery__thumbnail", dans l'ordre du code HTML
```
@media (max-width: 768px) {
    .gallery__thumbnail:first-child {
    width: calc(50% - 8px);
  }
}
```
> "À partir de cette largeur d'écran là tu exécute le code suivant"

### Changer le nombre d'images par ligne
Dans cette exemple, on va changer le nombre d'image par ligne en fonction du device. On a également agrandit l'image quand on est desktop.

```
.gallery__thumbnail {
  float: left;
  width: calc(33% - 8px);
  margin: 0 8px 8px 0;
}

@media (min-width: 768px) {
  .gallery__thumbnail {
    width: calc(25% - 8px);
  }
}

@media (min-width: 1024px) {
  .gallery__thumbnail:first-child {
    width: calc(50% - 8px);
  }
}
```
### Passer un élemnt en dessous de l'autre

```
.gallery-submit {
  margin-top: 1em;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  flex-wrap: wrap;
}
```

### Changer le taille de police ne fonction du device

```
@media (min-width: 1024px) {
  body {
    font-size: 18px;
  }
}
```

**Support**
- [Slides-Responsive Web Design](https://drive.google.com/drive/folders/1Vj12UWytncuV3tISstKyDya4CELBjBHC?usp=sharing)