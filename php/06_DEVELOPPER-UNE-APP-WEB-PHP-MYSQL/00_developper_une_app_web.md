## **6. Développement d'une Application Web PHP/MySQL**

### 6.1 Création d'une base de données

#### **Conception de la base de données**

1. **Analyse des besoins** :

   - Définir quelles données seront stockées dans votre application (par exemple, utilisateurs, articles, commentaires).
   - Identifier les entités principales et leurs relations.

2. **Modélisation** :

   - Utiliser un outil de modélisation (comme MySQL Workbench) pour créer un modèle de la base de données.

   - Définir les tables pour chaque entité identifiée, par exemple :

     - **users** : `id`, `username`, `email`, `password`, `created_at`.
     - **posts** : `id`, `user_id`, `title`, `content`, `created_at`, `updated_at`.
     - **comments** : `id`, `post_id`, `user_id`, `comment`, `created_at`.

   - Définir les relations :

     - Relation un-à-plusieurs entre `users` et `posts`.
     - Relation un-à-plusieurs entre `posts` et `comments`.

     3. **Création des tables** :

   4. Utiliser le SQL pour créer des tables :

      ```sql
      CREATE TABLE users (
          id INT AUTO_INCREMENT PRIMARY KEY,
          username VARCHAR(50) NOT NULL,
          email VARCHAR(100) NOT NULL,
          password VARCHAR(255) NOT NULL,
          created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
      );
        
      CREATE TABLE posts (
          id INT AUTO_INCREMENT PRIMARY KEY,
          user_id INT NOT NULL,
          title VARCHAR(100) NOT NULL,
          content TEXT NOT NULL,
          created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
          updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
          FOREIGN KEY (user_id) REFERENCES users(id)
      );
        
      CREATE TABLE comments (
          id INT AUTO_INCREMENT PRIMARY KEY,
          post_id INT NOT NULL,
          user_id INT NOT NULL,
          comment TEXT NOT NULL,
          created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
          FOREIGN KEY (post_id) REFERENCES posts(id),
          FOREIGN KEY (user_id) REFERENCES users(id)
      );
      ```

### **6.2 Utilisation de phpMyAdmin ou ligne de commande MySQL**

1. **phpMyAdmin** :

   - Accéder à phpMyAdmin via un navigateur.
   - Créer une nouvelle base de données.
   - Importer un fichier SQL pour configurer les tables si nécessaire.

2. **Ligne de commande MySQL** :

- Se connecter à MySQL :

  ```bash
  mysql -u root -p
  ```

- Créer une base de données :

  ```sql
  CREATE DATABASE nom_de_la_base;
  ```

- Importer une base de données à partir d'un fichier SQL :

  ```sql
  USE nom_de_la_base; -- Sélectionner la base de données
  mysql -u username -p my_database < my_database.sql -- Importer le fichier SQL
  ```

### 6.3 Formulaires PHP et gestion des données

#### **Création de formulaires HTML**

1. **Formulaires GET et POST** :

- Formulaire d'inscription avec méthode POST :

  ```html
  <form action="register.php" method="post">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username">
        <label for="email">Email:</label>
        <input type="email" id="email" name="email">
        <label for="password">Password:</label>
        <input type="password" id="password" name="password">
        <input type="submit" value="Register">
  </form>
  ```

- Sécurisation du formulaire en utilisant des techniques telles que :

  - Utilisation de `htmlspecialchars()` pour éviter les injections XSS.
  - Vérification de la validité des données côté serveur.

### **6.4 Traitement des données de formulaire avec PHP**

1. **Validation et nettoyage des données** :

- Nettoyer et valider les entrées :

  ```php
  <?php
  $username = htmlspecialchars(trim($_POST['username']));
  $email = filter_var($_POST['email'], FILTER_SANITIZE_EMAIL);
  $password = htmlspecialchars(trim($_POST['password']));
  ```

Expliquons ce code end détail :

- `htmlspecialchars()` : Convertit les caractères spéciaux en entités HTML pour éviter les attaques XSS (Cross-Site Scripting).
- `trim()` : Supprime les espaces en début et fin de chaîne.
- `filter_var()` : Valide et filtre une variable avec un filtre spécifique, ici `FILTER_SANITIZE_EMAIL`.
- `$_POST['username']` : Récupère la valeur du champ `username` envoyée via la méthode POST.
- `$_POST['email']` : Récupère la valeur du champ `email` envoyée via la méthode POST.
- `$_POST['password']` : Récupère la valeur du champ `password` envoyée via la méthode POST.

Ces fonctions permettent de nettoyer et valider les données avant de les insérer dans la base de données. Ce processus est essentiel pour garantir la sécurité et l'intégrité des données.

2. **Insertion dans la base** :

- Préparer une requête pour insérer les données :

  ```php
  <?php
  $stmt = $conn->prepare("INSERT INTO users (username, email, password) VALUES (?, ?, ?)");
  $stmt->bind_param("sss", $username, $email, $hashed_password);
  $stmt->execute();
  ```

Expliquons ce code en détail :

- `$conn->prepare()` : Prépare une requête SQL pour l'exécution.
- `$stmt->bind_param()` : Lie les variables aux paramètres de la requête préparée.
- `$stmt->execute()` : Exécute la requête préparée.
- `?` : Marqueur de paramètre pour les valeurs à insérer. Les types de données sont définis par les lettres `s` (string), `i` (integer), `d` (double), `b` (blob).

### **6.5 Authentification utilisateur**

#### **Système de login et de gestion de sessions**

1. **Gestion des sessions** :

   - Démarrer une session pour suivre l'état de l'utilisateur :

     ```php
     <?php
     session_start();
     $_SESSION['user_id'] = $user_id;
     ```
     
Ce code démarre une session PHP et stocke l'ID de l'utilisateur dans la variable `$_SESSION`. Cela permet de suivre l'état de l'utilisateur tout au long de sa session.

**Vérification des identifiants** :

- Comparer les identifiants fournis avec ceux stockés dans la base de données :

  ```php
  <?php
  $stmt = $conn->prepare("SELECT id, password FROM users WHERE email = ?");
  $stmt->bind_param("s", $email);
  $stmt->execute();
  $stmt->store_result();
  if ($stmt->num_rows > 0) 
      $stmt->bind_result($user_id, $hashed_password);
      $stmt->fetch();
      if (password_verify($password, $hashed_password)) {
          $_SESSION['user_id'] = $user_id;
      }
  }
  ```
  
Ce code vérifie si l'email fourni correspond à un utilisateur dans la base de données. Si c'est le cas, il vérifie si le mot de passe fourni correspond au mot de passe hashé stocké dans la base de données. Si la vérification réussit, l'ID de l'utilisateur est stocké dans la session.

#### **Sécurisation des mots de passe**

1. **Hashage des mots de passe** :

   - Utiliser `password_hash()` pour sécuriser les mots de passe :

     ```php
     <?php
     $hashed_password = password_hash($password, PASSWORD_BCRYPT);
     ```
Pour hashage des mots de passe, nous utilisons l'algorithme de hachage bcrypt par défaut. Cela garantit que les mots de passe sont stockés de manière sécurisée dans la base de données. Il existe plusieurs options pour personnaliser le processus de hachage, telles que l'ajout de coûts pour ralentir les attaques par force brute.

Vérification lors de la connexion :

```php
<?php
if (password_verify($password, $hashed_password)) {
    // Connexion réussie
}
```

### 6.6 CRUD complet (Create, Read, Update, Delete)

#### **Création d'une interface de gestion de contenu**

1. **Affichage des données** :

- Utiliser une requête SELECT pour récupérer et afficher les données :

  ```php
  <?php
  $result = $conn->query("SELECT * FROM posts");
  while ($row = $result->fetch_assoc()) {
      echo "<h2>" . $row['title'] . "</h2>";
      echo "<p>" . $row['content'] . "</p>";
  }
  ```

2. **Création et modification** :

- Formulaire pour créer un nouveau post :

  ```html
  <form action="create_post.php" method="post">
      <input type="text" name="title" placeholder="Title">
      <textarea name="content" placeholder="Content"></textarea>
      <input type="submit" value="Create Post">
  </form>
  ```

- Mettre à jour un post :

    ```php
    <?php
    $stmt = $conn->prepare("UPDATE posts SET title=?, content=? WHERE id=?");
    $stmt->bind_param("ssi", $title, $content, $post_id);
    $stmt->execute();
    ```

**Suppression de données** :

- Supprimer un post avec une requête DELETE :

  ```php
  <php
  $stmt = $conn->prepare("DELETE FROM posts WHERE id=?");
  $stmt->bind_param("i", $post_id);
  $stmt->execute();
  ```

