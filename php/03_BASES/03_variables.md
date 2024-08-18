#### 2.1.2 Variables

Les variables en PHP sont utilisées pour stocker des données qui peuvent être manipulées et référencées ultérieurement dans le programme. Toutes les variables en PHP commencent par un signe dollar (`$`) suivi du nom de la variable. Les noms de variables sont sensibles à la casse.

Pour mieux comprendre, une variable est une boite dans laquelle vous pouvez stocker des informations. Vous pouvez ensuite utiliser cette boite pour stocker, modifier et récupérer ces informations.

Pour mieux définir une variable, il est recommandé de suivre ces règles :

- Le nom de la variable doit commencer par une lettre ou un tiret bas (`_`).

- Le nom de la variable ne doit pas contenir d'espaces ou de caractères spéciaux, à l'exception du tiret bas (`_`).

- Le nom de la variable ne doit pas commencer par un chiffre.

- Le nom de la variable doit être unique dans le script.

- Le nom de la variable doit être descriptif et significatif.

- Les noms de variables sont sensibles à la casse.

- **Déclaration d'une variable :**

Pour déclarer une variable en PHP, utilisez le signe dollar (`$`) suivi du nom de la variable et du signe égal (`=`) suivi de la valeur de la variable. Voici un exemple de déclaration de variable :

```php
<?php
$nom = "John";
?>
```

Dans cet exemple, nous avons déclaré une variable `$nom` et lui avons attribué la valeur `"John Doe"`.

Afficher la valeur d'une variable :

Pour afficher la valeur d'une variable en PHP, utilisez la fonction `echo` suivie du nom de la variable. Voici un exemple :

```php
<?php
$nom = "John";
echo $nom; // Affiche "John"
?>
```

### Conclusion 

Les variables sont un élément essentiel de la programmation en PHP. Elles permettent de stocker des données qui peuvent être manipulées et référencées ultérieurement dans le programme. Il est important de bien comprendre comment déclarer et utiliser des variables en PHP pour pouvoir écrire des scripts efficaces et fonctionnels.