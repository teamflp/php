## Propriétés et Méthodes

### Définition des propriétés

Les **propriétés** d'une classe sont des variables qui appartiennent à une classe et peuvent être utilisées pour stocker des informations sur les objets créés à partir de cette classe. Les propriétés sont définies dans la classe à l'aide des mots-clés de visibilité `public`, `private` ou `protected`.

- **public** : La propriété est accessible de n'importe où, c'est-à-dire à la fois à l'intérieur de la classe, à partir des sous-classes et depuis l'extérieur de la classe.
- **private** : La propriété est accessible uniquement à l'intérieur de la classe où elle est définie.
- **protected** : La propriété est accessible à l'intérieur de la classe où elle est définie et dans les sous-classes héritées, mais pas depuis l'extérieur de ces classes.

Exemple de définition de propriétés :

```php
<?php
class Voiture {
    public $marque;    // Propriété publique
    private $modele;   // Propriété privée
    protected $couleur; // Propriété protégée
}
?>
```

### Utilisation des propriétés

Pour accéder à une propriété d'un objet, on utilise l'opérateur `->`.

```php
<?php
$maVoiture->marque = "Toyota";
echo $maVoiture->marque; // Affiche "Toyota"
?>
```

Cependant, les propriétés privées et protégées ne peuvent pas être directement accessibles de l'extérieur de la classe, ce qui garantit l'encapsulation.

### Définition des méthodes

Les **méthodes** sont des fonctions qui sont définies au sein d'une classe et qui permettent d'exécuter des actions sur les objets. Comme pour les propriétés, les méthodes peuvent être publiques, privées ou protégées.

Exemple de méthode dans une classe :

```php
<?php
class Voiture {
    public $marque;

    // Méthode publique
    public function demarrer() {
        echo "La voiture démarre";
    }
}
?>
```

### Utilisation des méthodes

Pour appeler une méthode d'un objet, on utilise l'opérateur `->`.

```php
<?php
$maVoiture->demarrer(); // Affiche "La voiture démarre"
?>
```

Si la méthode est privée ou protégée, elle ne peut être appelée que depuis l'intérieur de la classe ou par les classes qui en héritent.

### Conclusion

La POO en PHP est un puissant outil pour structurer vos programmes de manière claire et efficace. En utilisant des classes pour définir des objets avec des propriétés et des méthodes, vous pouvez créer des systèmes modulaires, réutilisables et plus faciles à maintenir. La maîtrise des concepts de base tels que les classes, les objets, les propriétés et les méthodes est essentielle pour tirer pleinement parti des capacités de la POO en PHP.