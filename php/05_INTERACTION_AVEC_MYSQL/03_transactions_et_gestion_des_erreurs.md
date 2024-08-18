## Transactions et gestion des erreurs

### Transactions MySQL

Les transactions sont une caractéristique essentielle dans les bases de données qui permettent de regrouper une série d'opérations SQL en une seule unité de travail. Ces opérations sont traitées comme un tout indivisible : soit toutes les opérations réussissent, soit aucune ne doit être appliquée. Les transactions sont particulièrement utiles pour assurer la cohérence des données lors de modifications complexes.

#### Utilisation de `BEGIN`, `COMMIT`, et `ROLLBACK`

1. **BEGIN** :

   - `BEGIN` (ou `START TRANSACTION`) marque le début d'une transaction. Dès que vous exécutez cette commande, toutes les opérations SQL suivantes seront traitées comme une seule transaction jusqu'à ce qu'un `COMMIT` ou un `ROLLBACK` soit exécuté.
   - Exemple :

2. **COMMIT** :

- `COMMIT` permet de valider toutes les opérations effectuées dans la transaction. Une fois le `COMMIT` exécuté, toutes les modifications de la transaction sont définitivement appliquées à la base de données.
- Exemple :

3. **ROLLBACK** :

- `ROLLBACK` annule toutes les opérations effectuées depuis le début de la transaction. Cette commande est utilisée pour revenir à l'état initial si une erreur se produit ou si certaines conditions ne sont pas remplies.
- Exemple :

```sql
<?php
$pdo->rollBack();
```

#### Exemple pratique

Voici un exemple de code illustrant l'utilisation des transactions en PHP avec PDO :

```php
<?php
try {
    // Démarrer la transaction
    $pdo->beginTransaction();

    // Première opération SQL
    $stmt = $pdo->prepare("INSERT INTO comptes (nom, solde) VALUES (:nom, :solde)");
    $stmt->execute([':nom' => 'John Doe', ':solde' => 500]);

    // Deuxième opération SQL
    $stmt = $pdo->prepare("UPDATE comptes SET solde = solde - 100 WHERE nom = :nom");
    $stmt->execute([':nom' => 'John Doe']);

    // Validation de la transaction
    $pdo->commit();

    echo "Transaction réussie!";
} catch (Exception $e) {
    // En cas d'erreur, annuler la transaction
    $pdo->rollBack();
    echo "Erreur lors de la transaction : " . $e->getMessage();
}
```

Dans cet exemple, si une des opérations échoue (par exemple, une exception est levée), le `ROLLBACK` annule toutes les modifications effectuées dans cette transaction, garantissant ainsi que la base de données reste cohérente.

### Gestion des erreurs et débogage

La gestion des erreurs est cruciale pour écrire du code robuste et maintenir la stabilité de l'application, surtout lorsqu'il s'agit d'opérations de base de données. PHP offre un mécanisme de gestion des erreurs via les blocs `try-catch`.

#### Utilisation de `try-catch` pour gérer les erreurs de base de données

- **try-catch** :
  - Le bloc `try-catch` permet de capturer les exceptions qui peuvent se produire lors de l'exécution d'un code à risque (comme les requêtes SQL). Si une exception est levée dans le bloc `try`, elle est capturée par le bloc `catch`, où vous pouvez traiter l'erreur de manière appropriée (comme annuler une transaction ou afficher un message d'erreur à l'utilisateur).
  - Exemple de structure :

```php
<?php
try {
    // Code susceptible de provoquer une exception
    $stmt = $pdo->query("SELECT * FROM comptes WHERE id = 1");
} catch (PDOException $e) {
    // Gérer l'exception
    echo "Erreur SQL : " . $e->getMessage();
}
```

### Débogage des erreurs SQL

- **Affichage des erreurs** :

  - Pour déboguer les erreurs SQL, il est souvent utile d'afficher les messages d'erreur détaillés. Cependant, en production, il est conseillé de les enregistrer dans un fichier de log plutôt que de les afficher directement, afin d'éviter de divulguer des informations sensibles.

  - Exemple :

```php
<?php
$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```

### **Journaux d'erreurs** :

- Enregistrez les erreurs dans un fichier de journalisation pour faciliter le débogage sans affecter l'expérience utilisateur. Vous pouvez utiliser des outils comme `error_log()` pour écrire dans des fichiers de log personnalisés.

En combinant transactions et gestion des erreurs, vous pouvez créer des applications PHP qui sont non seulement performantes, mais aussi sûres et résilientes face aux erreurs. Il est essentiel de toujours envisager les différents cas d'erreurs possibles et de les gérer de manière appropriée pour éviter toute corruption de données ou interruptions de service.