# Méthode waterfall vs Méthode agile

La méthode waterfall permet difficilement d'implémenter les demandes de changements du client 

## Agile et méthodes agiles

**4 valeurs**
- Les individus et leurs interactions plus que les processus et les outils.
- Un logiciel qui fonctionne plus qu’une documentation exhaustive.
- La collaboration avec les clients plus que la négociation contractuelle.
- L’adaptation au changement plus que le suivi d’un plan.

**12 principes**
- Notre plus haute priorité est de satisfaire le client en livrant rapidement et régulièrement des fonctionnalités à grande valeur ajoutée.
- Accueillez positivement les changements de besoins, même tard dans le projet.
- Livrez fréquemment un logiciel opérationnel avec des cycles de quelques semaines à quelques mois et une préférence pour les plus courts.
- Les utilisateurs ou leurs représentants et les développeurs doivent travailler ensemble quotidiennement tout au long du projet.
    > pourvoir parler aux utilisateurs finaux (feedback)
- Réalisez les projets avec des personnes motivées. Fournissez-leur l’environnement et le soutien dont elles ont besoin et faites-leur confiance pour atteindre les objectifs - fixés.
- Privilégiez la co-location de toutes les personnes travaillant ensemble et le dialogue en face à face comme méthode de communication.
- Un logiciel opérationnel est la principale mesure de progression d'un projet.
- Les processus agiles encouragent un rythme de développement soutenable. Ensemble, les commanditaires, les développeurs et les utilisateurs devraient être capables de maintenir - indéfiniment un rythme constant.
    > éviter le rush et la pression pour tenir les délais, motivation avec des objectifs à court termes
- Une attention continue à l'excellence technique et à un bon design.
    > ne pas se contenter de la médiocriter, rester attentifs à ce qui se fait pour utiliser la solution la plus optimale
- La simplicité – c’est-à-dire l’art de minimiser la quantité de travail inutile – est essentielle.
- Les meilleures architectures, spécifications et conceptions émergent d'équipes auto-organisées.
    >
- À intervalles réguliers, l'équipe réfléchit aux moyens possibles pour devenir plus efficace. Puis elle s'adapte et modifie son mode de fonctionnement en conséquence.
    > ce que je fais aujourd'hui, ce que je fais demain, mes difficultés
    > stand-up meeting

## Le scrum

> Cadre pour réalisé des projets, basé sur Agile

1. Product backlog : Ensemble de besoins exprimés par l'utilisateur traduits en terme de fonctionnalités
2. Sprint backlog Période de temps (pouvant aller de 2 à 4 semaines) pour travailler sur les fonctionnalités essentielles (déterminées par le client)
    - On fait un sprint : on travaille sur les fonctionnalités choisies qu'on livre à la fin du sprint au client
    - le sprint est ponctué de daily scrum meeting ()
    - le scrum master agit comme un facilitateur
3. Livraison du produit
4. On reitère les étapes 1, 2 et 3


# Projet Potato Shop

## Fonctionalité de site de vente de papate

Product Backlog
1. Catalogue
- Liste
- Filtres /tri
- Détail produit
- Avis clients

2. Compte client
- Avis
- Favoris
- Historique de commandes
- Moyens de paiement
- Adresses

3. Panier
- Ajouter des éléments
- Voir le panier
- transformer en commande

4. Gestion de la factuiration
- voir les factures

5. Tunnel de commande
- Voir les options de livraison
- Voir le soptions de paiement
- Validation

6. Formulaire de contact
7. Faq
8. Information légales
9. SAV
10. Recherche sur le site


## User story

### Qu'est qu'une user-story
- Qui veut queqluque (Qui ?)
- Qu'est ce qu'il veut (Quoi ?)
- Pour quelle usage (Pourquoi ?)

> en tant que [Utilisateur concerné], je veux [Action] afin de [Raisons]

**Exemples** 
> En tant que client, je veux pouvoir choisir mes options de livraison pour pouvoir livrer le produit à l'endroit qui me convient
> En tant qu'admin, je veux pouvoir connaitre le lieu de livraison pour pouvoir donner la bonne adresse de livraison à la compagnie de transport
> En tant que client, je souhaite pouvoir valider ma commande afin de sceller l'achat et d'obtenir mon produit


### Evaluer le nombre user-story réalisable dans 1 sprint donnée

De quoi dépend le nombre de user story à réaliser par sprint
- la taille de l'équipe
- la durée du sprint
- l'expérience (combien on reussi a faire de user-story avant)
- complexité des user-stories

Sur les cartes on va indiquer un niveau de complexité
- une équipe de dev peut "absorber" un certain nombre de points de difficulté
- une user-story a un nombre donné de points de difficulté

Noter la complexité d'une user-story
- utiliser la suite de fibonacci ([1 2 3 5 8 13 21 34] : rajouter le nombre précédent au suivant)
- pour se laisser une marge d'erreur dans l'évaluation de la difficulté


1 2 3 5 8 13 21 34

**Sur Trello**

1. Créer un tableau avec les user-stories
2. Créer un tableau avec les liste des todo
    - en indiquant le nombre de point de difficulté absobable par la scrum team


|             Product backlog           |              Todo Sprint              |   En cours   |   À tester  |     Fini     |
|---------------------------------------|---------------------------------------|--------------|-------------|--------------|
|    Fonctionality/Level : User-story   |    Fonctionality/Level : User-story   |              |             |              |



**Remarques**
- le sprnt 0 permet de poser les bases du projet


# Gestion du code

## Travailler sur une branche
Cloner le fichier
Aller sur une nouvelle branche
```
git checkout -b nomDeBranche
```

Faire les modifications ( ajout d'un fichie rà mon nom dan sle dossier students)

Pusher sur git
```
git add .
git commit -m "j'écris des choses ici"
git push --set-upstream origin amy
```

## Faire une demande de pull request

Appuyer sur le bouton vert en haut à gauche request pull request
Aller sur le menu latéral droit
- choisir approuvees
- sélectionner les "correcteurs"

Quand la pull request est acceptée on appuie sur le bouton pour la merger

[Pull request](https://github.com/O-clock-Alumni/fiches-recap/blob/master/ldc/git-pull-request.md)