## Exécution des Requêtes SQL en PHP

La gestion des bases de données est une composante essentielle de la plupart des applications web modernes. En PHP, les interactions avec une base de données se font généralement via des requêtes SQL. Voici une exploration détaillée des différentes façons d'exécuter ces requêtes en toute sécurité.

#### 1. Requêtes de base (SELECT, INSERT, UPDATE, DELETE)

Ces quatre types de requêtes SQL représentent les opérations CRUD (Create, Read, Update, Delete) qui sont à la base de la gestion des données.

- **SELECT :** Utilisé pour lire ou extraire des données d'une table. Par exemple, pour récupérer tous les utilisateurs d'une table `users` :

```php
<?php
$query = "SELECT * FROM users";
$result = mysqli_query($connection, $query);

while ($row = mysqli_fetch_assoc($result)) {
    echo $row['username'];
}
```

- **INSERT :** Utilisé pour ajouter de nouvelles données dans une table. Par exemple, pour insérer un nouvel utilisateur dans la table `users` :

```php
<?php
$query = "INSERT INTO users (username, email) VALUES ('john_doe', 'john@example.com')";
$result = mysqli_query($connection, $query);

if ($result) {
    echo "Nouvel utilisateur ajouté avec succès!";
} else {
    echo "Erreur lors de l'ajout de l'utilisateur : " . mysqli_error($connection);
}
```

- **UPDATE :** Utilisé pour modifier des données existantes dans une table. Par exemple, pour mettre à jour l'email d'un utilisateur :

```php
<?php
$query = "UPDATE users SET email='john_new@example.com' WHERE username='john_doe'";
$result = mysqli_query($connection, $query);

if ($result) {
    echo "Utilisateur mis à jour avec succès!";
} else {
    echo "Erreur lors de la mise à jour : " . mysqli_error($connection);
}
```

**DELETE :** Utilisé pour supprimer des données d'une table. Par exemple, pour supprimer un utilisateur de la table `users` :

```php
<?php
$query = "DELETE FROM users WHERE username='john_doe'";
$result = mysqli_query($connection, $query);

if ($result) {
    echo "Utilisateur supprimé avec succès!";
} else {
    echo "Erreur lors de la suppression : " . mysqli_error($connection);
}
```

#### 2. Préparation et Exécution des Requêtes Sécurisées

L'une des principales préoccupations en matière de sécurité lors de l'exécution de requêtes SQL est la prévention des **injections SQL**, une technique d'attaque qui permet à un utilisateur malveillant d'exécuter des requêtes SQL non autorisées sur la base de données. Pour éviter cela, il est fortement recommandé d'utiliser des **requêtes préparées**.

- **Utilisation des requêtes préparées :**

  Les requêtes préparées permettent de séparer le code SQL de la donnée, ce qui empêche l'injection de code SQL malveillant. En PHP, les requêtes préparées peuvent être utilisées avec l'extension `mysqli` ou `PDO`.

  - **Exemple avec** `mysqli`**:**

```php
<?php
// Préparation de la requête
$stmt = $connection->prepare("SELECT * FROM users WHERE username = ?");

// Liaison des paramètres
$stmt->bind_param("s", $username);

// Affectation de la valeur du paramètre
$username = "john_doe";

// Exécution de la requête
$stmt->execute();

// Récupération des résultats
$result = $stmt->get_result();
while ($row = $result->fetch_assoc()) {
    echo $row['email'];
}

// Fermeture de la requête préparée
$stmt->close();
```

- **Exemple avec** `PDO`** :**

```php
<?php
// Préparation de la requête
$stmt = $pdo->prepare("SELECT * FROM users WHERE username = :username");

// Exécution de la requête avec les paramètres
$stmt->execute(['username' => 'john_doe']);

// Récupération des résultats
$users = $stmt->fetchAll();
foreach ($users as $user) {
    echo $user['email'];
}
```

- **Avantages des requêtes préparées :**

  - **Sécurité accrue :** Les requêtes préparées empêchent les injections SQL, car les données et le code SQL sont séparés.
  - **Performance :** Les requêtes préparées peuvent être exécutées plusieurs fois avec des valeurs différentes, ce qui peut être plus efficace pour des exécutions répétées de la même requête.
  - **Lisibilité et Maintenance :** Le code est plus clair et plus facile à maintenir, car les paramètres sont explicitement définis et passés à la requête.

### Conclusion

L'exécution de requêtes SQL en PHP est une tâche courante mais critique. L'utilisation correcte des requêtes basiques (SELECT, INSERT, UPDATE, DELETE) est essentielle pour manipuler les données dans la base de données. Cependant, pour assurer la sécurité de l'application, il est impératif de toujours utiliser des requêtes préparées. Non seulement cela protège contre les attaques par injection SQL, mais cela améliore également la lisibilité et la performance du code.