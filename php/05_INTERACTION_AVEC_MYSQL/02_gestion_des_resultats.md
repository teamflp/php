## Gestion des résultats

### 1. **Récupération des résultats des requêtes SQL**

Lorsqu'une requête SQL est exécutée dans un script PHP, les résultats sont généralement renvoyés sous forme de ressources que vous pouvez ensuite parcourir pour accéder aux données individuelles. PHP offre plusieurs méthodes pour extraire ces résultats, chacune ayant ses propres particularités et cas d'utilisation.

#### a. **Utilisation de** `fetch_assoc()`

La méthode `fetch_assoc()` est utilisée pour récupérer une ligne de résultats sous la forme d'un tableau associatif. Dans ce tableau, les clés sont les noms des colonnes de la base de données, et les valeurs sont les données correspondantes. Cette méthode est idéale lorsque vous souhaitez manipuler les résultats sous forme de paires clé-valeur.

**Exemple d'utilisation :**

```php
<?php
$result = $mysqli->query("SELECT id, nom, email FROM utilisateurs");

while ($row = $result->fetch_assoc()) {
    echo "ID: " . $row["id"] . " - Nom: " . $row["nom"] . " - Email: " . $row["email"] . "<br>";
}
```

#### b. **Utilisation de** `fetch_object()`

La méthode `fetch_object()` permet de récupérer une ligne de résultats sous la forme d'un objet. Les propriétés de cet objet correspondent aux colonnes de la base de données. Cette approche est particulièrement utile si vous préférez travailler avec des objets plutôt qu'avec des tableaux.

**Exemple d'utilisation :**

```php
<?php
$result = $mysqli->query("SELECT id, nom, email FROM utilisateurs");

while ($row = $result->fetch_object()) {
    echo "ID: " . $row->id . " - Nom: " . $row->nom . " - Email: " . $row->email . "<br>";
}
```

#### c. **Utilisation de** `fetchAll()`

La méthode `fetchAll()` est disponible avec PDO (PHP Data Objects) et permet de récupérer toutes les lignes du résultat d'une requête dans un tableau multidimensionnel. Par défaut, chaque ligne est retournée sous forme d'un tableau associatif, mais il est possible de spécifier un mode de récupération différent.

**Exemple d'utilisation :**

```php
<?php
$stmt = $pdo->query("SELECT id, nom, email FROM utilisateurs");
$rows = $stmt->fetchAll(PDO::FETCH_ASSOC);

foreach ($rows as $row) {
    echo "ID: " . $row['id'] . " - Nom: " . $row['nom'] . " - Email: " . $row['email'] . "<br>";
}
```

### 2. **Affichage des résultats dans une page web**

Une fois que vous avez récupéré les résultats de votre requête SQL, il est courant de les afficher dans une page web. Pour cela, vous pouvez utiliser des boucles pour itérer sur chaque ligne de résultats et générer dynamiquement du code HTML. PHP s'intègre parfaitement avec HTML, ce qui facilite ce processus.

#### a. **Affichage de résultats sous forme de liste**

L'une des méthodes les plus simples pour afficher des résultats consiste à les présenter sous forme de liste non ordonnée.

**Exemple d'utilisation :**

```php
<?php
$result = $mysqli->query("SELECT nom FROM utilisateurs");

echo "<ul>";
while ($row = $result->fetch_assoc()) {
    echo "<li>" . htmlspecialchars($row["nom"]) . "</li>";
}
echo "</ul>";
```

#### b. **Affichage de résultats sous forme de tableau HTML**

Pour des données tabulaires, il est souvent plus approprié d'utiliser un tableau HTML. Vous pouvez générer ce tableau dynamiquement en parcourant les résultats de la requête.

**Exemple d'utilisation :**

```php
<?php
$result = $mysqli->query("SELECT id, nom, email FROM utilisateurs");

echo "<table border='1'>";
echo "<tr><th>ID</th><th>Nom</th><th>Email</th></tr>";

while ($row = $result->fetch_assoc()) {
    echo "<tr>";
    echo "<td>" . htmlspecialchars($row["id"]) . "</td>";
    echo "<td>" . htmlspecialchars($row["nom"]) . "</td>";
    echo "<td>" . htmlspecialchars($row["email"]) . "</td>";
    echo "</tr>";
}

echo "</table>";
```

#### c. **Utilisation des boucles pour un affichage plus complexe**

En combinant les boucles PHP avec du HTML, vous pouvez créer des interfaces utilisateur plus sophistiquées. Par exemple, vous pourriez imbriquer plusieurs boucles pour afficher des données hiérarchiques ou utiliser des conditions pour afficher différentes mises en forme en fonction des valeurs des données.

**Exemple d'utilisation avec des conditions :**

```php
<?php
$result = $mysqli->query("SELECT id, nom, email, statut FROM utilisateurs");

echo "<table border='1'>";
echo "<tr><th>ID</th><th>Nom</th><th>Email</th><th>Statut</th></tr>";

while ($row = $result->fetch_assoc()) {
    echo "<tr>";
    echo "<td>" . htmlspecialchars($row["id"]) . "</td>";
    echo "<td>" . htmlspecialchars($row["nom"]) . "</td>";
    echo "<td>" . htmlspecialchars($row["email"]) . "</td>";
    
    // Affichage conditionnel du statut
    $statut = $row["statut"] == 1 ? "Actif" : "Inactif";
    echo "<td>" . htmlspecialchars($statut) . "</td>";
    
    echo "</tr>";
}

echo "</table>";
```

### Conclusion

La gestion des résultats des requêtes SQL est une étape essentielle dans le développement d'applications web PHP. En utilisant les méthodes appropriées pour extraire et afficher les données, vous pouvez créer des interfaces utilisateur dynamiques et interactives. N'hésitez pas à expérimenter avec les différentes approches présentées ici pour trouver celle qui convient le mieux à vos besoins spécifiques.