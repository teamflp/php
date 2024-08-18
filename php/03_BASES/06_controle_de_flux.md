## Structures conditionnelles

Les structures conditionnelles sont un élément fondamental de la programmation, permettant aux développeurs de contrôler le flux d'exécution du code en fonction de conditions spécifiques. En PHP, comme dans la plupart des langages de programmation, les structures conditionnelles sont utilisées pour exécuter des blocs de code seulement si certaines conditions sont remplies.

### La structure `if`

L'instruction `if` est la structure conditionnelle de base en PHP. Elle permet d'exécuter un bloc de code si une condition donnée est vraie. Voici la syntaxe générale :

```php
<?php
$age = 18;

if (condition) {
    // Code à exécuter si la condition est vraie
}
?>
```

Exemple :

```php
<?php
$age = 18;

if ($age >= 18) {
    echo "Vous êtes majeur.";
}
?>
```

### La structure `else`

L'instruction `else` s'utilise en complément de `if` pour exécuter un bloc de code alternatif si la condition de `if` est fausse.

```php
<?php
if (condition) {
    // Code à exécuter si la condition est vraie
} else {
    // Code à exécuter si la condition est fausse
}
?>
```

Exemple :

```php
<?php
$age = 17;

if ($age >= 18) {
    echo "Vous êtes majeur.";
} else {
    echo "Vous êtes mineur.";
}
?>
```

### La structure `elseif`

Parfois, vous avez besoin de tester plusieurs conditions. L'instruction `elseif` permet d'ajouter des conditions supplémentaires après un `if`. Elle peut être utilisée en combinaison avec `else`.

Syntaxe :

```php
<?php
if (condition1) {
    // Code à exécuter si la condition1 est vraie
} elseif (condition2) {
    // Code à exécuter si la condition2 est vraie
} else {
    // Code à exécuter si aucune condition n'est vraie
}
?>
```

Exemple :

```php
<?php
$age = 17;

if ($age >= 18) {
    echo "Vous êtes majeur.";
} elseif ($age >= 16) {
    echo "Vous êtes presque majeur.";
} else {
    echo "Vous êtes mineur.";
}
?>
```

### La structure `Le switch-case`

Lorsque vous avez plusieurs conditions à tester qui sont basées sur la même variable, l'instruction switch peut être une alternative plus lisible à une série de `elseif`.

Syntaxe :

```php
<?php
switch (variable) {
    case valeur1:
        // Code à exécuter si variable est égale à valeur1
        break;
    case valeur2:
        // Code à exécuter si variable est égale à valeur2
        break;
    // ...
    default:
        // Code à exécuter si aucune des valeurs ne correspond
}
?>
```

```php
<?php
$jour = "mardi";

switch ($jour) {
    case "lundi":
        echo "Aujourd'hui c'est lundi.";
        break;
    case "mardi":
        echo "Aujourd'hui c'est mardi.";
        break;
    case "mercredi":
        echo "Aujourd'hui c'est mercredi.";
        break;
    default:
        echo "Jour non reconnu.";
}
?>
```

Dans cet exemple, le code affiche "Aujourd'hui c'est mardi." car la variable `$jour` est égale à "mardi".

### La structure ternaire

L'opérateur ternaire est une version concise de l'instruction if...else. Il est utilisé pour affecter une valeur à une variable en fonction d'une condition.

Syntaxe :

```php
<?php
$variable = (condition) ? valeur_si_vrai : valeur_si_faux;
?>
```

Exemple :

```php
<?php
$age = 18;

echo ($age >= 18) ? "Vous êtes majeur." : "Vous êtes mineur.";
?>
```

Dans cet exemple, si la condition est vraie, le premier bloc de code est exécuté, sinon le second bloc de code est exécuté.

### L'opérateur `null coalescing`

L'opérateur `null coalescing` permet de simplifier l'écriture d'un test sur une variable.

```php
<?php
$nom = $_GET['nom'] ?? "Inconnu";

echo "Bonjour $nom";
?>
```

Dans cet exemple, si la variable `$_GET['nom']` est définie, elle est utilisée, sinon la valeur par défaut "Inconnu" est utilisée.

### L'opérateur `null coalescing` avec `isset`

L'opérateur `null coalescing` peut être combiné avec la fonction `isset` pour tester si une variable est définie.

```php
<?php
$nom = $_GET['nom'] ?? "Inconnu";

echo "Bonjour $nom";
?>
```

Dans cet exemple, si la variable `$_GET['nom']` est définie, elle est utilisée, sinon la valeur par défaut "Inconnu" est utilisée.

### Conclusion

Les structures conditionnelles permettent de tester des conditions et d'exécuter du code en fonction du résultat. Il est possible de tester une condition simple avec `if`, `else`, et `elseif`, ou de tester plusieurs valeurs avec `switch`. La structure ternaire permet de simplifier l'écriture d'un `if`/`else`, et l'opérateur `null coalescing` permet de simplifier la gestion des variables non définies.