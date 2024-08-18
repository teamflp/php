#### Classes et Objets

##### Déclaration de classes

Une **classe** est une sorte de plan (ou de modèle) qui définit les propriétés et les comportements d'un type particulier d'objet. En PHP, une classe est définie en utilisant le mot-clé `class`, suivi du nom de la classe, et le corps de la classe est délimité par des accolades `{}`.

Voici un exemple de déclaration d'une classe simple en PHP :

```php
<?php
class Voiture {
    // Propriétés de la classe
    public $marque;
    public $modele;
    public $couleur;

    // Méthode de la classe
    public function demarrer() {
        echo "La voiture démarre";
    }
}
?>
```

Dans cet exemple, `Voiture` est le nom de la classe, et elle contient trois **propriétés** (ou attributs) : `$marque`, `$modele`, et `$couleur`. Elle possède également une méthode `demarrer()`, qui définit un comportement que les objets de cette classe pourront exécuter.

##### Instanciation d'objets

Une fois qu'une classe est définie, vous pouvez créer des **objets** basés sur cette classe. En PHP, un objet est une instance d'une classe. Pour créer un objet, on utilise le mot-clé `new` suivi du nom de la classe.

Voici comment instancier un objet à partir de la classe `Voiture` :
    
```php
<?php
// Instanciation d'un objet de la classe Voiture
$maVoiture = new Voiture();

// Accès aux propriétés de l'objet
$maVoiture->marque = "Renault";
$maVoiture->modele = "Clio";

// Appel de la méthode de l'objet
$maVoiture->demarrer();
?>
```

Dans cet exemple, `$maVoiture` est un objet de la classe `Voiture`. On peut accéder aux propriétés de l'objet en utilisant l'opérateur `->`, et appeler la méthode `demarrer()` de l'objet.

##### Visibilité des propriétés et méthodes