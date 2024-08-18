### Opérateurs et expressions : Opérateurs arithmétiques et de comparaison, de comparaison, et logiques.

Les opérateurs en PHP sont utilisés pour effectuer des opérations sur des variables et des valeurs. Ils sont divisés en plusieurs catégories :

- **Opérateurs arithmétiques :** Ils permettent de réaliser des opérations mathématiques.

  - Addition (`+`) : `$a + $b`
  - Soustraction (`-`) : `$a - $b`
  - Multiplication (`*`) : `$a * $b`
  - Division (`/`) : `$a / $b`
  - Modulo (`%`) : `$a % $b` (reste de la division de `$a` par `$b`)

Exemple :

```php
<?php
$a = 10;
$b = 3;
$somme = $a + $b; // $somme vaut 13
$diff = $a - $b; // $diff vaut 7
$prod = $a * $b; // $prod vaut 30
$quot = $a / $b; // $quot vaut 3.3333333333333
$reste = $a % $b; // $reste vaut 1
?>
```

Dans cet exemple, les opérateurs arithmétiques sont utilisés pour effectuer des opérations mathématiques sur les variables `$a` et `$b`.

### **Opérateurs de comparaison :** Ils sont utilisés pour comparer deux valeurs.

#### **Les opérateurs de comparaison**

Dans les structures conditionnelles, les opérateurs de comparaison sont utilisés pour évaluer les conditions. Voici quelques opérateurs couramment utilisés en PHP :

- `==` : égal à
- `!=` : différent de
- `>` : supérieur à
- `<` : inférieur à
- `>=` : supérieur ou égal à
- `<=` : inférieur ou égal à
- `===` : strictement égal (comparaison de la valeur et du type)
- `!==` : strictement différent

Exemple :

```php
<?php
<?php
$a = 10; 
$b = 5;

var_dump($a == $b); // false : $a et $b ne sont pas égaux en valeur.
var_dump($a === $b); // false : $a et $b ne sont ni égaux en valeur ni en type (bien qu'ils soient tous les deux des entiers, ils ont des valeurs différentes).
var_dump($a != $b); // true : $a et $b sont différents en valeur.
var_dump($a > $b); // true : $a est supérieur à $b.
var_dump($a !== $b); // true : $a et $b sont différents en valeur et en type (ici, c'est surtout la différence de valeur qui compte car ils sont du même type).
var_dump($a < $b); // false : $a n'est pas inférieur à $b.
var_dump($a > $b); // true : $a est supérieur à $b (répétition de la ligne précédente).
var_dump($a <= $b); // false : $a n'est ni inférieur ni égal à $b.
var_dump($a >= $b); // true : $a est supérieur ou égal à $b.
?>
```

Dans cet exemple, les opérateurs de comparaison sont utilisés pour comparer les valeurs des variables `$a` et `$b`.

### Explication des résultats :

1. `$a == $b` : Compare uniquement les valeurs de `$a` et `$b`. Ici, 10 n'est pas égal à 5, donc le résultat est `false`.
2. `$a === $b` : Compare à la fois les valeurs et les types de `$a` et `$b`. Puisque 10 n'est pas égal à 5 (malgré le fait qu'ils sont tous deux de type `int`), le résultat est `false`.
3. `$a != $b` : Vérifie si les valeurs de `$a` et `$b` sont différentes. 10 est différent de 5, donc le résultat est `true`.
4. `$a > $b` : Vérifie si `$a` est supérieur à `$b`. 10 est effectivement supérieur à 5, donc le résultat est `true`.
5. `$a !== $b` : Vérifie si `$a` et `$b` sont différents en valeur ou en type. Comme 10 et 5 sont différents en valeur, le résultat est `true`.
6. `$a < $b` : Vérifie si `$a` est inférieur à `$b`. 10 n'est pas inférieur à 5, donc le résultat est `false`.
7. `$a > $b` (répétée) : Comme précédemment, cette comparaison montre que 10 est supérieur à 5, donc le résultat est encore `true`.
8. `$a <= $b` : Vérifie si `$a` est inférieur ou égal à `$b`. 10 n'est ni inférieur ni égal à 5, donc le résultat est `false`.
9. `$a >= $b` : Vérifie si `$a` est supérieur ou égal à `$b`. 10 est supérieur à 5, donc le résultat est `true`.

### Les opérateurs logiques

**Opérateurs logiques :** Ils permettent de combiner plusieurs conditions.

- ET (`&&`) : Retourne `true` si les deux opérandes sont vrais.
- OU (`||`) : Retourne `true` si au moins un des opérandes est vrai.
- NON (`!`) : Inverse la valeur logique d'une expression.

Exemple 1 : Opérateur `&&` (ET)

```php
<?php
$age = 25;
$sexe = 'F';

if ($age >= 18 && $sexe == 'F') {
    echo 'Vous êtes une femme majeure.'; // Affiche : Vous êtes une femme majeure.
}
?>
```

Dans cet exemple, la condition est vraie si l'âge est supérieur ou égal à 18 et si le sexe est féminin.

Exemple 2 : Opérateur `||` (OU)

```php
<?php
$age = 15;
$sexe = 'M';

if ($age < 18 || $sexe == 'F') {
    echo 'Vous êtes mineur ou de sexe féminin.'; // Affiche : Vous êtes mineur ou de sexe féminin.
}
?>
```

Dans cet exemple, la condition est vraie si l'âge est inférieur à 18 ou si le sexe est féminin.

Exemple 3 : Opérateur `!` (NON)

```php
<?php
$age = 25;

if (!($age < 18)) {
    echo 'Vous êtes majeur.'; // Affiche : Vous êtes majeur.
}
?>
```

Dans cet exemple, la condition est vraie si l'âge n'est pas inférieur à 18.

### Exercices

1. Créez une variable `$note` initialisée à 12. Écrivez une condition qui affiche "Note valide" si la note est comprise entre 0 et 20.
2. Créez une variable `$genre` initialisée à 'M'. Écrivez une condition qui affiche "Homme" si le genre est 'M', et "Femme" si le genre est 'F'.
3. Créez une variable `$age` initialisée à 25. Écrivez une condition qui affiche "Majeur" si l'âge est supérieur ou égal à 18, et "Mineur" sinon.
4. Créez une variable `$note` initialisée à 12. Écrivez une condition qui affiche "Note valide" si la note est comprise entre 0 et 20, et "Note invalide" sinon.

Les opérateurs logiques permettent de combiner plusieurs conditions pour réaliser des tests plus complexes. Ils sont souvent utilisés dans les structures conditionnelles pour prendre des décisions en fonction de plusieurs critères.

### Conclusion

Les structures conditionnelles sont essentielles pour créer des scripts PHP dynamiques et réactifs. Elles permettent aux développeurs de gérer la logique de leurs programmes de manière flexible, en répondant à différentes conditions. Maîtriser ces structures vous permettra de concevoir des applications PHP robustes et efficaces.