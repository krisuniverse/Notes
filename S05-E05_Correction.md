# Requêtes

- Récupérer les catégories (en les triant selon leur ordre d'affichage dans la home et en s'assurant de n'avoir que 5)
```sql
SELECT *
  FROM type
  WHERE home_order != 0
  ORDER BY home_order
  LIMIT 5
```

- Récupérer les types à afficher dans le footer
```sql
SELECT * 
FROM type 
WHERE footer_order != 0 
ORDER BY footer_order 
LIMIT 5
```

- Récupérer les marques à afficher dans le footer

```sql
SELECT * 
FROM brand 
WHERE footer_order != 0 
ORDER BY footer_order 
LIMIT 5
```


- Récuperer le nom et le sous-titre d'une categorie (par exemple catégorie ID 2)

```sql
SELECT * 
FROM category 
WHERE id = 2
```

- Récuperer les produits d'une categorie (par exemple catégorie ID 4)

```sql
SELECT * 
FROM product
WHERE category_id = 4

```