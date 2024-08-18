## **Projet : Application Web PHP/MySQL**

### **1. Structure du projet**

Voici la structure de base du projet :

Voici la structure de base du projet :

```plaintext
/
|-- index.php
|-- register.php
|-- login.php
|-- logout.php
|-- create_post.php
|-- edit_post.php
|-- delete_post.php
|-- view_post.php
|-- config/
|   |-- database.php
|-- includes/
|   |-- header.php
|   |-- footer.php
|   |-- navbar.php
|   |-- functions.php
|-- css/
|   |-- styles.css
```

### **2. Création des fichiers**

#### **2.1 Configuration de la base de données**

**Fichier :** `config/database.php`

Ce fichier contient les informations de connexion à la base de données.

```php
<?php
$host = 'localhost';
$dbname = 'my_database';
$username = 'root';
$password = '';

$conn = new mysqli($host, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
```

#### **2.2 Fichiers d'inclusion (Header, Footer, Navbar)**

**Fichier :** `includes/header.php`

Ce fichier inclut les balises de début HTML et le lien vers la feuille de style.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My PHP/MySQL App</title>
    <link rel="stylesheet" href="/css/styles.css">
</head>
<body>
```

**Fichier :** `includes/footer.php`

Ce fichier contient les balises de fin du document HTML.

```html
</body>
</html>
```

**Fichier :** `includes/navbar.php`

Ce fichier contient la barre de navigation pour faciliter la navigation dans l'application.

```html
<nav>
    <ul>
        <li><a href="/index.php">Home</a></li>
        <li><a href="/register.php">Register</a></li>
        <li><a href="/login.php">Login</a></li>
        <li><a href="/create_post.php">Create Post</a></li>
        <li><a href="/logout.php">Logout</a></li>
    </ul>
</nav>
```

**Fichier :** `includes/functions.php`

Ce fichier contient les fonctions réutilisables dans l'application.

```php
<?php
function isLoggedIn() {
    return isset($_SESSION['user_id']);
}

function redirectIfNotLoggedIn() {
    if (!isLoggedIn()) {
        header('Location: /login.php');
        exit;
    }
}
```

#### **2.3 Pages principales**

**Fichier :** `index.php`

Page d'accueil qui affiche les derniers articles.

```php
<?php
include 'config/database.php';
include 'includes/header.php';
include 'includes/navbar.php';

$result = $conn->query("SELECT * FROM posts ORDER BY created_at DESC");

while ($row = $result->fetch_assoc()) {
    echo "<h2><a href='view_post.php?id=" . $row['id'] . "'>" . $row['title'] . "</a></h2>";
    echo "<p>" . substr($row['content'], 0, 100) . "...</p>";
}

include 'includes/footer.php';
```

**Fichier :** `register.php`

Page d'inscription des utilisateurs.

```php
<?php
include 'config/database.php';
include 'includes/header.php';
include 'includes/navbar.php';

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $username = htmlspecialchars(trim($_POST['username']));
    $email = filter_var($_POST['email'], FILTER_SANITIZE_EMAIL);
    $password = password_hash(trim($_POST['password']), PASSWORD_BCRYPT);

    $stmt = $conn->prepare("INSERT INTO users (username, email, password) VALUES (?, ?, ?)");
    $stmt->bind_param("sss", $username, $email, $password);
    if ($stmt->execute()) {
        echo "Registration successful!";
    } else {
        echo "Error: " . $conn->error;
    }
}
?>

<form action="register.php" method="post">
    <label for="username">Username:</label>
    <input type="text" id="username" name="username" required>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    <label for="password">Password:</label>
    <input type="password" id="password" name="password" required>
    <input type="submit" value="Register">
</form>

<?php include 'includes/footer.php'; ?>
```

**Fichier :** `login.php`

Page de connexion des utilisateurs.

```php
<?php
include 'config/database.php';
include 'includes/header.php';
include 'includes/navbar.php';
session_start();

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $email = filter_var($_POST['email'], FILTER_SANITIZE_EMAIL);
    $password = trim($_POST['password']);

    $stmt = $conn->prepare("SELECT id, password FROM users WHERE email = ?");
    $stmt->bind_param("s", $email);
    $stmt->execute();
    $stmt->store_result();

    if ($stmt->num_rows > 0) {
        $stmt->bind_result($user_id, $hashed_password);
        $stmt->fetch();
        if (password_verify($password, $hashed_password)) {
            $_SESSION['user_id'] = $user_id;
            header('Location: /index.php');
            exit;
        } else {
            echo "Invalid email or password.";
        }
    } else {
        echo "Invalid email or password.";
    }
}
?>

<form action="login.php" method="post">
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    <label for="password">Password:</label>
    <input type="password" id="password" name="password" required>
    <input type="submit" value="Login">
</form>

<?php include 'includes/footer.php'; ?>
```

**Fichier :** `logout.php`

Page pour déconnecter l'utilisateur.

```php
<?php
session_start();
session_destroy();
header('Location: /index.php');
exit;
```

**Fichier :** `create_post.php`

Page pour créer un nouvel article. Cette page est protégée, donc seule une personne connectée peut y accéder.

```php
<?php
include 'config/database.php';
include 'includes/header.php';
include 'includes/navbar.php';
include 'includes/functions.php';
session_start();

redirectIfNotLoggedIn();

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $title = htmlspecialchars(trim($_POST['title']));
    $content = htmlspecialchars(trim($_POST['content']));
    $user_id = $_SESSION['user_id'];

    $stmt = $conn->prepare("INSERT INTO posts (user_id, title, content) VALUES (?, ?, ?)");
    $stmt->bind_param("iss", $user_id, $title, $content);
    if ($stmt->execute()) {
        echo "Post created successfully!";
    } else {
        echo "Error: " . $conn->error;
    }
}
?>

<form action="create_post.php" method="post">
    <label for="title">Title:</label>
    <input type="text" id="title" name="title" required>
    <label for="content">Content:</label>
    <textarea id="content" name="content" required></textarea>
    <input type="submit" value="Create Post">
</form>

<?php include 'includes/footer.php'; ?>
```

**Fichier :** `edit_post.php`

Page pour modifier un article existant.

```php
<?php
include 'config/database.php';
include 'includes/header.php';
include 'includes/navbar.php';
include 'includes/functions.php';
session_start();

redirectIfNotLoggedIn();

$post_id = $_GET['id'];

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $title = htmlspecialchars(trim($_POST['title']));
    $content = htmlspecialchars(trim($_POST['content']));

    $stmt = $conn->prepare("UPDATE posts SET title=?, content=? WHERE id=? AND user_id=?");
    $stmt->bind_param("ssii", $title, $content, $post_id, $_SESSION['user_id']);
    if ($stmt->execute()) {
        echo "Post updated successfully!";
    } else {
        echo "Error: " . $conn->error;
    }
} else {
    $stmt = $conn->prepare("SELECT title, content FROM posts WHERE id=? AND user_id=?");
    $stmt->bind_param("ii", $post_id, $_SESSION['user_id']);
    $stmt->execute();
    $stmt->bind_result($title, $content);
    $stmt->fetch();
}
?>

<form action="edit_post.php?id=<?= $post_id ?>" method="post">
    <label for="title">Title:</label>
    <input type="text" id="title" name="title" value="<?= htmlspecialchars($title) ?>" required>
    <label for="content">Content:</label>
    <textarea id="content" name="content" required><?= htmlspecialchars($content) ?></textarea>
    <input type="submit" value="Update Post">
</form>

<?php include 'includes/footer.php'; ?>
```

**Fichier :** `delete_post.php`

Page pour supprimer un article.

```php
<?php
include 'config/database.php';
include 'includes/functions.php';
session_start();

redirectIfNotLoggedIn();

$post_id = $_GET['id'];

$stmt = $conn->prepare("DELETE FROM posts WHERE id=? AND user_id=?");
$stmt->bind_param("ii", $post_id, $_SESSION['user_id']);
if ($stmt->execute()) {
    echo "Post deleted successfully!";
} else {
    echo "Error: " . $conn->error;
}

header('Location: /index.php');
exit;
```

**Fichier :** `view_post.php`

Page pour afficher un article individuel.

```php
<?php
include 'config/database.php';
include 'includes/header.php';
include 'includes/navbar.php';

$post_id = $_GET['id'];

$stmt = $conn->prepare("SELECT title, content, created_at FROM posts WHERE id=?");
$stmt->bind_param("i", $post_id);
$stmt->execute();
$stmt->bind_result($title, $content, $created_at);
$stmt->fetch();
?>

<h1><?= htmlspecialchars($title) ?></h1>
<p><?= htmlspecialchars($content) ?></p>
<p><em>Posted on <?= $created_at ?></em></p>

<?php include 'includes/footer.php'; ?>
```

### **3. Feuille de style CSS**

**Fichier :** `css/styles.css`

Vous pouvez ajouter des styles CSS basiques pour la mise en page de votre application.

```css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
}

nav ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    background-color: #333;
}

nav ul li {
    display: inline;
    margin-right: 10px;
}

nav ul li a {
    color: white;
    text-decoration: none;
    padding: 10px;
}

nav ul li a:hover {
    background-color: #555;
}
```

### 4. Conclusion

Ce tutoriel vous a montré comment créer une application Web simple en PHP et MySQL. Vous pouvez personnaliser davantage l'application en ajoutant des fonctionnalités supplémentaires telles que la pagination, les commentaires, les likes, etc. N'hésitez pas à explorer davantage PHP et MySQL pour créer des applications Web plus avancées.    
