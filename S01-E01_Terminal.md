# Le Terminal

## Le prompt
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks
```
Traduction d ela commande :
mint chez la machine qui s'apelle amy-ndiaye se trouve ici (/var/html/oclock)
## Savoir où je me trouve
pwd

## Se rendre quelque part
```
cd 
```
cd signifie change directory 
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks$ cd html/
```
## Auto-tabulation
appuyer sur la touche TAB pour généré de l'auto-complétion

## Remonter dans le dossier parent
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks/html$ cd ..
```
** remarque **
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks/html$ cd .
```
reste dans l'endroit où on se trouve

## Lister les fichiers
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks/html$ ls
```
sous forme de liste :
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks/html$ ls -l
```

## Créer un dossier
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks/html$ mkdir S01
```
cette commande crée le dossier S01
mkdir signifie make a directory

## La commande man
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks/html$ man ls
```
Cette permet d'afficher le manuel d'une commande

## Utiliser git en ligne de commande

Aller sur le dossier source présent sur GitHub
Cliquer sur **Clone or download**
Sélectionner **clone with SSH**
Copier la commande directement dans le terminal
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks/html$ git@github.com:o-clock-universe/S01-E01-challenge-markdown.git
```

## Annuler une commande
ctrl + c ??
```
^C
```

# Correction challenge n°01

## Étape 1 - Fichier zip
Déziper un fichier
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks/html$ unzip nom_du_fichier.zip
```
## Étape 2 - Analyse

## Étape 3 - Markdown
- Créer un fichier (markdown) en ligne de commande
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks/html$ touch nom_du_fichier.md
```

- Ouvrir vs code
    - ouvrir un dossier
    ```
    mint@amy-ndiaye ~ $ /var/www/html/oclocks/html/s01-E01-challenge-markdown$ code .
    ```
    - Ouvrir un fichier en particulier
    ```
    mint@amy-ndiaye ~ $ /var/www/html/oclocks/html/s01-E01-challenge-markdown$ code nom_du_fichier.md
    ```
- Déterminer le type de documents
    - Avec la couleur
        - bleu : dossier
        - blanc : fichier
        - vert :

    - Avec les info
    ```
    drwxr 
    ```
    le **d** signifie directory

- Lancer le terminal dans vs code
    - Terminal > New terminal

## 
Lister toute l'arborescence
```
mint@amy-ndiaye ~ $ /var/www/html/oclocks/html/s01-E01-challenge-markdown/arborescence$ tree
```

Pour activer cette commande il faut installer le paquet
```
sudo apt install tree
```