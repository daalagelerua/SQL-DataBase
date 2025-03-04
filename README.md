## 1. What’s a database (Qu'est-ce qu'une base de données ?)

Une base de données est une collection organisée d'informations qui peuvent être facilement consultées,
gérées et mises à jour.
Elle permet de stocker des données de manière structurée afin de les retrouver efficacement.

💡 **Analogie** : 
Une base de données est comme un cahier de recettes, où chaque page contient une recette spécifique.
Si tu veux retrouver une recette, tu peux chercher par catégorie (plats, desserts...) ou par ingrédient principal.

A solid database is expected to be **ACID**, which means it guarantees:

- **Atomicity**: transactions are atomic, which means if a transaction fails, the result will be like it never happened.
- **Consistency**: you can define rules for your data, and expect that the data abides by the rules, or else the transaction fails.
- **Isolation**: run two operations at the same time, and you can expect that the result is as though they were ran one after the other.
- **Durability**: unplug your server at any time, boot it back up, and it didn’t lose any data.

## 2. What’s a relational database (Qu'est-ce qu'une base de données relationnelle ?)

Une base de données relationnelle (RDB - Relational Database) est un type de base de données
qui stocke les informations sous forme de tableaux reliés entre eux par des relations.

💡 **Analogie** :
C'est comme un restaurant où tu as plusieurs listes :

- Une liste de clients (nom, téléphone...)
- Une liste de commandes (plat, prix, client...)
- Une liste de plats (nom, prix, ingrédients...)

*Ces listes sont connectées* : une commande est liée à un client, un plat fait partie d’une commande, etc.

**Pourquoi appelle-t-on ça des bases de données "relationnelles" ?**
Les bases de données sont appelées "relationnelles" parce qu'elles organisent les données sous forme de tables qui sont reliées entre elles.

Le mot "relationnel" vient du fait que les tables étaient historiquement appelées "relations",
car elles regroupent des données qui partagent une structure commune. Aujourd'hui, on parle plutôt de tables,
mais le concept de relation existe toujours, avec une signification plus précise.

**Qu'est-ce qu'une relation aujourd'hui ?**
Dans le contexte actuel, une relation est un lien qui connecte deux enregistrements (rows) entre eux, souvent entre deux tables différentes.

Prenons un exemple concret avec un blog qui contient des articles et des commentaires :

*Table posts (articles)*

|id |	title        |	body       |
|---|----------------|-------------|
|1  |Mon premier post|	Contenu... |
|2  |	Un autre post|	Contenu... |

*Table comments (commentaires)*

|id |	body         |post_id|
|---|----------------|-------|
|1  |Super article ! |	1    |
|2  |Très intéressant|	1    |
|3  |J'adore ce post |	2    |

***Comment relie-t-on les données entre elles ?***

Dans la table posts, chaque article a un id unique (c'est la clé primaire).
Mais comment savoir à quel article appartient un commentaire ?

👉 On ajoute un champ post_id dans la table comments, qui stocke l'id du post associé.

C'est ce qu'on appelle une clé étrangère (foreign key). Elle fait référence à la clé primaire d'une autre table.

Dans posts, id est une clé primaire.
Dans comments, post_id est une clé étrangère qui pointe vers id dans posts.

**Grâce à cela** :

- Depuis un commentaire, on peut retrouver son article (avec post_id).
- Depuis un article, on peut retrouver tous ses commentaires en recherchant les lignes où post_id = l'id de l'article.

## 3. What does SQL stand for (Que signifie SQL ?)

SQL (**Structured Query Language**) est un langage utilisé pour interagir avec les bases de données relationnelles.
Il permet de **créer**, **modifier**, **supprimer** et **interroger** les données.

💡 **Analogie** :
SQL est comme la langue commune entre toi et la base de données, permettant de lui poser des questions et de lui donner des ordres.

## 4. What’s MySQL (Qu'est-ce que MySQL ?)

MySQL est un système de gestion de bases de données relationnelles (RDBMS - Relational Database Management System)
qui utilise SQL pour manipuler les données.

💡 **Pourquoi MySQL ?**

- Gratuit et open-source 🎉
- Utilisé par les grandes entreprises (YouTube, Facebook…)
- Fiable et rapide 🚀

## 5. How to create a database in MySQL (Comment créer une base de données en MySQL ?)

Créer une base de données en MySQL est simple. Voici la commande SQL :

```sql
CREATE DATABASE my_database;
```

💡 **Explication** :

CREATE DATABASE → indique à MySQL de créer une nouvelle base de données.
my_database → nom de la base de données.

👀 Vérifier si la base a bien été créée :

```sql
SHOW DATABASES;
```

## 6. What does DDL and DML stand for (Que signifient DDL et DML ?)

*Les commandes SQL sont regroupées en plusieurs catégories* :

**DDL (Data Definition Language)** : définit la structure de la base de données (création/modification de tables).

- `CREATE` → crée une table ou une base de données.
- `ALTER` → modifie une table existante.
- `DROP` → supprime une table ou une base.

**DML (Data Manipulation Language)** : manipule les données.

- `INSERT` → ajoute des données.
- `UPDATE` → met à jour des données.
- `DELETE` → supprime des données.
- `SELECT` → récupère des données.

💡 **Analogie** :

- DDL = construire une maison 🏠 (définir la structure)
- DML = aménager la maison 🛋️ (ajouter des meubles, changer la déco...)

## 7. How to CREATE or ALTER a table (Comment créer ou modifier une table ?)

📌 ***Créer une table users*** :
```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100) UNIQUE
);
```

- id INT PRIMARY KEY AUTO_INCREMENT → clé primaire auto-incrémentée.
- VARCHAR(50) → champ texte avec max 50 caractères.
- UNIQUE → garantit que l'email est unique.

📌 ***Modifier une table (ALTER TABLE)*** :
```sql
ALTER TABLE users ADD COLUMN age INT;
```
*Modifier la table users en ajoutant une colonne age de type INT*

🛑 **Attention** :

La colonne age est ajoutée mais n’a aucune valeur par défaut,
donc toutes les lignes existantes auront NULL comme valeur.

Si tu veux une valeur par défaut, utilise :
```sql
ALTER TABLE users ADD COLUMN age INT DEFAULT 0;
```
Ici, tous les nouveaux utilisateurs auront age = 0 par défaut.

## 8. How to SELECT data from a table (Comment récupérer des données d'une table ?)

📌 ***Récupérer tous les utilisateurs*** :

```
SELECT * FROM users;
```

📌 ***Récupérer les noms et emails des utilisateurs*** :

```sql
SELECT first_name, email FROM users;
```

📌 ***Filtrer les utilisateurs par email*** :

```sql
SELECT * FROM users WHERE email = 'test@example.com';
```

💡 **Analogie** :
SELECT est comme un moteur de recherche qui filtre les données dans la base.

## 9. How to INSERT, UPDATE or DELETE data (Comment insérer, modifier ou supprimer des données ?)

📌 ***Ajouter un utilisateur (INSERT)*** :

```sql
INSERT INTO users (first_name, last_name, email) 
VALUES ('John', 'Doe', 'john@example.com');
```

📌 ***Mettre à jour un utilisateur (UPDATE)*** :

```sql
UPDATE users SET email = 'new_email@example.com' WHERE id = 1;
```

📌 ***Supprimer un utilisateur (DELETE)*** :

```sql
DELETE FROM users WHERE id = 1;
```

⚠️ **Attention** :
DELETE supprime définitivement les données ! 🔥

## 10. What are subqueries (Qu'est-ce qu'une sous-requête ?)

Une sous-requête est une requête SQL imbriquée dans une autre requête.

📌 **Exemple** : 

récupérer les utilisateurs ayant passé au moins une commande :

```sql
SELECT * FROM users 
WHERE id IN (SELECT user_id FROM orders);
```

- La sous-requête (SELECT user_id FROM orders) renvoie la liste des user_id ayant commandé.
- La requête principale récupère les utilisateurs correspondant.

💡 **Analogie** :
Une sous-requête est comme un post-it dans un carnet : elle fournit des infos supplémentaires pour répondre à une question.

## 11. How to use MySQL functions (Comment utiliser les fonctions MySQL ?)

MySQL propose de nombreuses fonctions utiles :

📌 ***Fonctions de calcul*** :

```sql
SELECT COUNT(*) FROM users;  -- Compte le nombre d'utilisateurs
SELECT AVG(price) FROM places;  -- Moyenne des prix
SELECT SUM(price) FROM places;  -- Somme des prix
```

📌 ***Fonctions sur les chaînes de caractères*** :

```sql
SELECT UPPER(first_name) FROM users;  -- Met en majuscules
SELECT LOWER(last_name) FROM users;  -- Met en minuscules
SELECT CONCAT(first_name, ' ', last_name) FROM users;  -- Concatène
```

📌 ***Fonctions de date*** :

```sql
SELECT NOW();  -- Date et heure actuelles
SELECT YEAR(NOW());  -- Année en cours
SELECT DATEDIFF('2025-01-01', '2024-03-03');  -- Différence en jours
```

💡 **Analogie** : Les fonctions MySQL sont comme des outils de cuisine 🍳 qui permettent de transformer et manipuler les données.

## What makes the big difference between a backtick and an apostrophe?

What is the reason that the following two queries give wildly different results?

```sql
SELECT COUNT(DISTINCT(`price`)) FROM `products`; --Good
```

| COUNT(DISTINCT(`price`)) |
|--------------------------|
|                     2059 |


```sql
SELECT COUNT(DISTINCT('price')) FROM `products`; --Bad
```

| COUNT(DISTINCT('price')) |
|--------------------------|
|                        1 |

- 'price' (apostrophes or quotes) is a string. It never changes, so the count is always 1.
- \`price` (backtics) refers to the column price. So it could be more than 1.


* A straight single quote (') is used for string literals (along with straight double quote (")).
* A backtick quote (`) is for quoting identifiers.


- Identifiers must be quoted if they match a reserved word, or if they contain special characters.
- Quoted identifiers also can specify lowercase in case-insensitive fields (which otherwise might be shown as uppercase).

📌 ***Conclusion***
- ✅ Une base de données est un moyen structuré de stocker des informations.
- ✅ SQL est le langage pour manipuler ces données.
- ✅ MySQL est un outil populaire pour gérer ces bases.
- ✅ DDL permet de définir la structure, DML permet de gérer les données.
- ✅ Les requêtes SELECT, INSERT, UPDATE, DELETE permettent d'interagir avec les données.
- ✅ Les sous-requêtes et fonctions SQL permettent d’optimiser les recherches.

😊
