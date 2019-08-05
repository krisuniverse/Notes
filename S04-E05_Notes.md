# Les bases de données

## 1. Objectif d'un base de données
Une base de données sert à stocker, organiser et gérer des données.

**Notes**
Dans l'atelier le point le point d'entrée s'appelle adminer-4.7.1.php (l'équivalent de index.php)
## 2. Les DBSM ou Database Management System
(en français : SGBD ou Système de gestion de bases de données)

:warning: à compléter !

# Installer adminer
Sur le terminal, taper les commandes suivantes :

- Pour vérifier la "présence" de mysql
```
sudo systemctl status mysql
```

- Pour je sais pas quoi
```
mysql -u root -p
```

- Pour pourvoir accès à adminer via localhost (se placer dans /var/www/html)
```
sudo wget https://github.com/vrana/adminer/releases/download/v4.7.1/adminer-4.7.1.php adminer.php
```

**Identifiants**
- Utilisateur : root
- MDP : Ereul9Aeng


1. Créer une base de données

- Cliquer sur __Créer une base de données__
- Nommer la base de données
- Choisir utf8mb4_general_ci dans le menu déroulant

**remarques**
ci : case insensitive

2. Créer une table

- Cliquer sur Créer une table

**exemple**
Nom de la table : profs

| Nom de la colone |    Type    |   Longuer |   NULL    |   AI  |   +   |
|------------------|------------|-----------|-----------|-------|-------|
|        id        |     int    |           |           |   x   |       |  
|       name       |   varchar  |    163    |           |       |       |
|       email      |   varchar  |    255    |           |       |       |
|      address     |    text    |           |           |       |       |

Ici, on a crée 4 colonnes (id, name, email, addresse).

Les types de données sont plus nombreux qu'en PHP. Il y a, par exemple, blob qui peut être utile pour stocke run fichier volumineux (comme une image).

3.  Ajouters des éléments dans la table

- Cliquer sur __Nouvelle élément__

|           |                                           |
|-----------|-------------------------------------------|
|   nom     |   jd                                      |
|   mail    |   jd@oclock.io                            |
|  adresse  |   1 rue du code 46260 LIMOGNE-EN-QUERCY   |

**Astuce**
- Cliquer sur __Reqête SQL__ (au milieu de la page) pour faire apparaitre l'encadré vert

- Dans __Reqête SQL__ (à gauche), on peut taper les requêtes en SQL
Voici quelques exemples de requêtes (à modifier si besoin après correction du challenge et du bonus) :

    - Lister les auteurs par ordre alphabétique (sur le nom)
        ```sql
        SELECT * FROM author ORDER BY name ASC
        ```

    - Lister les auteurs dont l'e-mail contient @gmail.com
        ```sql
        SELECT * FROM author WHERE email LIKE "%gmail.com"
        ```

    - Lister les auteurs qui n'ont pas d'image de profil
        ```sql
        SELECT * FROM author WHERE image = "NULL" 
        ```

    - Lister le titre et la date de publication de tous les articles 
        ```sql
        SELECT title, publish_date FROM post
        ```
    - Afficher le titre d'un article en particulier (en passant l'id de l'article) 
        ```sql
        SELECT title FROM post WHERE id = "1"
        ```
    - Trier par ordre décroissant tous les articles par la date de publication
        ```sql
        SELECT * FROM post ORDER BY publish_date DESC
        ```
    - Compter le nombre d'articles et renommer la colonne en nbArticles
        ```sql
        SELECT COUNT(*) AS nbArticles FROM post
        ```

# Créer un serveur

1. Se connecter 
- Utilisateur : root
- MDP : Ereul9Aeng


2. Cliquer sur Privilèges

3. Créer un utilisateur
- Utilisateur : oclock
- MDP : oclock
- oclock.* (permet de limiter ses droits à la base oclock)
- cocher all privilges

# Exo en cours (matinée)
- Créer une bdd __oclock__

**commandes sql**
```sql
CREATE DATABASE `oclock` COLLATE 'utf8_general_ci';
```

- Créer une table __students__

| Nom de la colone |    Type    |   Longuer |   Options    |   NULL    |   AI  |   +   |
|------------------|------------|-----------|--------------|-----------|-------|-------|
|        id        |     int    |           |              |           |   x   |       |
|     nickname     |   varchar  |     32    |              |           |       |       |    

**remarque**
`unsigned` permet de ne pas gérer les nombres négatifs

**commandes sql**
```sql
CREATE TABLE `eleves` (
  `id` int unsigned NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `nickname` varchar(32) NOT NULL
);
```

# MCD : Modèle Conceptuel de Données

Logiciel utilisé :
[Mocodo(en ligne)](http://mocodo.wingi.net/)

## 1. Lister les tables
Dans la fenêtre, écrire :

> Students : id, nickname
Teachers : id, name, email
Courses : id, title, difficulty, content
Cohorts : id, name, created_at

**Format**
> Table : colonne1, colonne2

## 2. Créer les relations

### Cardinalité :
- on se pose la question de la relation entre deux entités
- on détermine quel nombres minimum et maximum d'entités vont etre en relation
- il y a trois possibilités : 0, 1 ou n (> 1)
- c'est comme les feux de l'amour (célibataire, en couple, avec 1 ou plusieurs amants, amour à sens unique, etc) (copyright Claudine & Amy)

## Exemple
> APPARTENIR À, 11 Students, 1nCohorts

> INTERVENIR SUR, 0n Teachers, 1n Cohorts

> EST DONNÉ À, nn> Cohorts, nn< Courses

**Format**
> APPARTENIR À, minmax Students, minmax Cohorts

Du point de vue d'un prof, la relation est 0n car il peut être relié à aucun étudiant(0) ou plus d'un étudiant (n)

**Remarques**
- Ici, les mots APPARTENIR À et INTERVENIR SUR sont crées par nous
- Appuyer sur "shuffle" à gauche pour redisposer les élements du  diagramme

Lorsqu'on appuie sur "shuffle" la disposition dans le champ de saise change

On passe de :
> Teachers : id, name, email
Students : id, nickname
Cohorts : id, name, created_at
Courses : id, title, difficulty, content

INTERVENIR SUR, 0n Teachers, 1n Cohorts
APPARTENIR À, 11 Students, 1n Cohorts

À :
> Teachers : id, name, email
Courses : id, title, difficulty, content
Students : id, nickname
INTERVENIR SUR, 0n Teachers, 1n Cohorts
Cohorts : id, name, created_at
APPARTENIR À, 11 Students, 1n Cohorts

- On peut avoir plus de 3 relations, mais généralement on considèerar qu'il y un problème au niveau des realtions entre les entités
- les relations n,n sont plus lourdes et donc induisent une moins bonne performance




On a modélisé le lien entre les promo et les cours de la manières suivante:
> EST DONNÉ À, nn> Cohorts, nn< Courses

Dans notre exemple, les cours sont donnés à une promo à un moment donné. 
C'est donc la relation qui se produit à un moment donnée. 
On va réifier cette relation, c'est-à-dire la concrétiser !
On va la renommer en Planning et lui attribuer une colonne (scheduled_at)

> Planning À, nn> Cohorts, nn< Courses : sheduled_at


# MLD : modèle logique de donnée
Un MCD a vocatoion a être transformé en un MLD.

En MCD on parle d'entité, en MLD on parle de table.

## Les 3 commandements du MLD

__Règle n°1__
Toute entité du MCD devient une table du MLD. L'identifiant de l'entité devient la clé primaire de la table.

__Règle n°2__
Si les deux cardinalités max. sont n, donc une relation "plusieurs à plusieurs" la relation devient une table à part entière en relation avec les deux entités. On parle de table de liaison, d'association, de jonction ou de correspondance.

__Règle n°3__
Si l'une des cardinalités max. vaut 1, dans notre exemple chaque livre est écrit par un seul auteur, la relation est directe entre ces deux tables : l'identifiant de la table Auteur devient une nouvelle propriété de la table Livre. Autrement dit la clé primaire de l'entité Auteur devient un nouvel attribut de la table Livre qu'on appelle également clé étrangère.


## MCD & MDL (pour le blog À la derive)

1. MCD
Category : id, name
WRITTEN BY, 0n< Author, 1n> Post
Author : id, name, image, mail

BELONGS TO, 11< Post, 0n> Category
Post : id, title, resume, content, date, author_id, category_id

2. MLD

http://sql.sh/ressources/document/mysql-aide-memoire-sql.pdf