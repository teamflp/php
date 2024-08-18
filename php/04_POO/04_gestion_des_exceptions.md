## Gestion des exceptions en PHP

La gestion des exceptions en PHP permet de traiter les erreurs de manière plus structurée et flexible par rapport aux méthodes traditionnelles de gestion d'erreurs, telles que l'utilisation des codes d'erreur ou des messages d'erreur directs. Avec les exceptions, vous pouvez gérer les erreurs dans un bloc de code spécifique, en séparant la logique d'erreur de la logique normale de votre programme.

### **Concepts de base**

- **Exception** : Une exception est un événement qui se produit lors de l'exécution d'un programme et qui interrompt le flux normal du programme. En PHP, une exception est un objet qui est généré (lancé) lorsqu'une erreur survient.

- **Try** : Le bloc `try` contient le code susceptible de générer une exception. Si une exception est lancée dans ce bloc, elle sera capturée par le bloc `catch` correspondant.

- **Catch** : Le bloc `catch` est utilisé pour capturer et gérer les exceptions lancées dans le bloc `try`. Vous pouvez définir plusieurs blocs `catch` pour traiter différents types d'exceptions.

- **Throw** : Le mot-clé `throw` est utilisé pour lancer une exception manuellement. Lorsque le mot-clé `throw` est rencontré, l'exécution du programme est immédiatement transférée au premier bloc `catch` qui peut gérer ce type d'exception.

### **Utilisation des blocs** `try`**,** `catch`**, et** `throw`

Syntaxe de base pour la gestion des exceptions en PHP :

```php
<?php
try {
    // Code susceptible de générer une exception
} catch (Exception $e) {
    // Gestion de l'exception
}
?>
```

Voici un exemple simple illustrant l'utilisation des blocs `try`, `catch`, et `throw` en PHP :

```php
<?php
function division($dividende, $diviseur) {
    if ($diviseur == 0) {
        // Lancer une exception si le diviseur est égal à zéro
        throw new Exception("Division par zéro.");
    }
    return $dividende / $diviseur;
}

try {
    // Essayer de diviser 10 par 0, ce qui générera une exception
    echo division(10, 0);
} catch (Exception $e) {
    // Gérer l'exception et afficher le message d'erreur
    echo "Erreur : " . $e->getMessage();
}
?>
```

Dans cet exemple :

1. `throw new Exception("Division par zéro.");` : Si le diviseur est égal à zéro, une exception est lancée avec le message "Division par zéro".

2. `try` : Le bloc `try` contient le code qui tente de diviser deux nombres. Si une exception est lancée, l'exécution saute immédiatement au bloc `catch`.

3. `catch (Exception $e)` : Ce bloc capture l'exception de type `Exception` et gère l'erreur en affichant un message.

#### **3.3.3 Hiérarchie des exceptions**

En PHP, toutes les exceptions doivent être des instances de la classe `Exception` ou d'une classe qui hérite de `Exception`. Cela signifie que vous pouvez créer vos propres classes d'exception personnalisées en les étendant de la classe de base `Exception`.

Par exemple :

```php
<?php
<?php
class MonExceptionPersonnalisee extends Exception {}

try {
    throw new MonExceptionPersonnalisee("Ceci est une exception personnalisée.");
} catch (MonExceptionPersonnalisee $e) {
    echo "Erreur personnalisée : " . $e->getMessage();
} catch (Exception $e) {
    echo "Erreur générale : " . $e->getMessage();
}
?>
?>
```

Dans cet exemple :

1. `MonExceptionPersonnalisee` : Une nouvelle classe d'exception personnalisée est créée en étendant la classe de base `Exception`.

2. `throw new MonExceptionPersonnalisee("Ceci est une exception personnalisée.");` : Une exception de type `MonExceptionPersonnalisee` est lancée.

3. **Gestion de l'exception personnalisée** : Le premier bloc `catch` capture les exceptions de type `MonExceptionPersonnalisee`, tandis que le second bloc capture toutes les autres exceptions de type `Exception`.

#### **3.3.4 Exceptions multiples et propagation**

Il est possible de capturer différentes exceptions dans différents blocs `catch`. L'ordre des blocs `catch` est important : PHP commence par vérifier la première exception et, s'il y a correspondance, exécute ce bloc `catch`. Si aucune correspondance n'est trouvée, il passe au bloc `catch` suivant.

Par exemple

```php
<?php
class ErreurDivision extends Exception {}
class ErreurInconnue extends Exception {}

function verifierNombre($nombre) {
    if ($nombre == 0) {
        throw new ErreurDivision("Division par zéro détectée.");
    } elseif ($nombre < 0) {
        throw new ErreurInconnue("Nombre négatif détecté.");
    }
    return true;
}

try {
    verifierNombre(-1);
} catch (ErreurDivision $e) {
    echo "Erreur de division : " . $e->getMessage();
} catch (ErreurInconnue $e) {
    echo "Erreur inconnue : " . $e->getMessage();
} catch (Exception $e) {
    echo "Erreur générale : " . $e->getMessage();
}
?>
```

Ici, le programme traite les différentes exceptions en fonction de leur type.

- **Propagation des exceptions** : Si une exception n'est pas capturée dans un bloc `try...catch`, elle se propage au niveau supérieur jusqu'à ce qu'elle soit capturée ou jusqu'à ce que le script s'arrête.

#### **3.3.5 Avantages de l'utilisation des exceptions**

- **Séparation de la logique d'erreur** : Les exceptions permettent de séparer clairement le code qui traite les erreurs du code qui effectue les opérations normales, rendant le code plus lisible et plus maintenable.

- **Gestion centralisée des erreurs** : Vous pouvez gérer toutes les erreurs dans un seul endroit, par exemple en utilisant un seul bloc `catch` ou en configurant un gestionnaire d'exceptions global.

- **Flexibilité et extensibilité** : En créant des exceptions personnalisées, vous pouvez gérer des situations d'erreur spécifiques de manière plus détaillée.

### Conclusion

La gestion des exceptions en PHP est un mécanisme puissant pour gérer les erreurs de manière élégante et efficace. Elle permet d'améliorer la robustesse et la maintenabilité de votre code en séparant clairement les préoccupations liées à la logique métier et à la gestion des erreurs. En utilisant correctement les blocs `try`, `catch`, et `throw`, ainsi que les exceptions personnalisées, vous pouvez créer des applications PHP plus résilientes et mieux structurées.