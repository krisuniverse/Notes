# Le HTML

## Intro

HTML n'est pas un langage de programmation. C'est un langage de balises qui définit la structure de votre contenu.

> C'est le squelette de la page web.

**remarque**
http : protocole utilisé 

## Les commentaires en HTML
Texte non-lu (non-interprété) par le navigateur
```
<!-- Ceci est un commentaire HTML -->
```

## Les balises

Les balises ont un rôle sémantique. Elles sont interprétées par le navigateur mais pas affichées sur la page finale. 
> Elles indiquent au navigateur la signification des balises, et non pas un rôle ! (exemple: `<b></b>`)

**remarque**
La sémantique sert énormément au niveau du SEO (référencement sur les moteurs de recherche)

Il existe 2 types de balises :
- les balises simples
```
<balise> Ici, du contenu </balise>
```
- les balises auto-fermantes
```
<balise />
```
HTML permet désormais d'utiliser les balises auto-fermantes de la manière qui suit :
```
<balise>
```
Exemple :
```
<img src="chemin/de/mon/image">
```

## Les attributs
```
<balise attribut="valeur">
```
Les attributs contiennent des informations supplémentaires qui portent sur l'élément et qu'on ne souhaite pas afficher avec le contenu.

## Construire une page HTML
```
<!DOCTYPE html>
```
DOCTYPE est une balise auto-fermante

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title></title>
    </head>
    <body>
    </body>
</html>
```
Les pages HTML sont divisées en 2 parties :
    - la balise `<head>` ou en-tête, qui contient les méta-informations
    - la balise `<body>` ou corps, qui contient le contenu à afficher

## Les différentes balises 
- La balise H
    - titre `<h1>` (jusqu'à 6 niveaux différents)
    - c'est une balise de type "block" (elle prend toute la place sur la ligne)
- La balise `<p>`
    - paragraphe `<p>`
- Les balises liste
    - liste ordonnée `<ol>` (balises-enfants : <li></li>)
    - liste non-ordonnée `<ul>` (balises-enfants : <li></li>)
- la balise `<em>` (balise inline)
    - pour mettre en vant un contenu
- les balises d'insertion ou de suppression (balise inline)
    - insertion de contenu : `<ins></ins>`
    - supression de contenu : `<del></del>`

## Block vs Inline
Block : provoque un retour à la ligne
Inline : peut s'insérer dans d'autres balises, ne provoque pas de retour à la ligne

## Balise à velur sémantique ou non
- pas de valeur sémantque : div, span

# Ajouter du CSS
## Technique 1  : dans une balise HTML (peu recommandé)
```
 <balise attribut"propriété:valeur">
 <body style="background-color:olivedrab">
```
Intégrer du css directement dans la page HTML


## Technique 2 : dans la balise style (peu recommandé)
```
<style>
    sélecteur css {
        propriété : valeur;
    }
</style>
```
```
<style>
    h1 {
        color : red;
    }
</style>
```
**remarque** mettre la balise `<style>` dans la balise `<head>`

## Technique 3 : lier un fichier css

**remarque**
Priorité en css
    - instruction spécifique : prioritaire
    - instruction générale : secondaire

Il n'y a rien de plus précis qu'écrir du style dans un élément :
```
 <balise attribut"propriété:valeur">
 ```
 ```
 <body style="background-color:olivedrab">
```

Cibler tous les éléments dans la pages
```
*{
                    }
```

###Faire un commentaire en css
```
/* ceci est un commentaire*/
```

###Cibler plusieurs éléments à la fois
```
h2,h3 {
    propriété1: valeur;
    propriété2: valeur;
}
```

Lier le fichier css à fichier html
```
    <link rel="stylesheet" href="style.css">
```
Si il faut remonter d'un cran
```
    <link rel="stylesheet" href="../style.css">
```
# Ressources
## Sites internet
https://developer.mozilla.org/fr/docs/Web/HTML : site officiel
https://htmlreference.io : pour se documenter sur les balises HTML

## Extensions VS code
HTMLHint 0.6.0 : permet de proposer des suggestions
 : permet de dupliquer un fichier/dossier sur VS code

## raccourcis
Ctrl + Maj +Flèche : permet de placer le curseur sur plusieurs lignes à la fois

lorem + TAB : génère un texte fictif (Lorem Ipsum)

Maj + Entréé : aller à la ligne dans le chat


