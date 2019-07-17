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

- Pour pourvoir accès à adminer via localhost
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
