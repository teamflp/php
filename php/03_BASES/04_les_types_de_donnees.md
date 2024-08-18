## Les types de données

PHP est un langage faiblement typé, ce qui signifie que vous n'avez pas besoin de déclarer explicitement le type d'une variable ; PHP le déduit automatiquement en fonction de la valeur assignée. Voici les principaux types de données en PHP :

- **Integer (int) :** Représente un nombre entier, par exemple `42`, `-3`.

```php
<?php
$nombre = 42;
echo $nombre; // Affiche 42
?>
```

- **Float (float) :** Représente un nombre à virgule flottante, par exemple `3.14`, `-0.5`.

```php
<?php
$pi = 3.14;
echo $pi; // Affiche 3.14
?>
```

- **String :** Représente une chaîne de caractères, par exemple `'Hello, World!'`, `"Bonjour"`.

```php
<?php
$nom = 'Alice';
echo $nom; // Affiche Alice
?>
```

- **Boolean (bool) :** Représente une valeur booléenne, `true` ou `false`.

```php
<?php
$estVrai = true;
echo $estVrai; // Affiche 1
?>
```

- **Array :** Représente une collection de valeurs, par exemple `[1, 2, 3]`, `['rouge', 'vert', 'bleu']`.

```php
<?php
$couleurs = ['rouge', 'vert', 'bleu'];
echo $couleurs[0]; // Affiche rouge
?>
```

- **Object :** Représente une instance d'une classe.

```php
<?php
class Personne {
    public $nom;
    public $age;
}

$alice = new Personne();
$alice->nom = 'Alice';
$alice->age = 30;
echo $alice->nom; // Affiche Alice
?>
```

- **NULL :** Représente une variable sans valeur.

```php
<?php
$indefini = NULL;
echo $indefini; // Affiche rien
?>
```

### Conclusion

Les types de données en PHP sont similaires à ceux des autres langages de programmation. Il est important de comprendre ces types pour manipuler correctement les données dans vos scripts PHP.