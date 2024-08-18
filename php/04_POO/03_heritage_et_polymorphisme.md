## Héritage et Polymorphisme

L'héritage et le polymorphisme sont deux concepts fondamentaux de la programmation orientée objet (POO) qui permettent de structurer et réutiliser efficacement du code dans vos applications PHP. Ils facilitent la modularité, la maintenance et l'extensibilité du code, rendant ainsi vos applications plus robustes et plus faciles à faire évoluer.

### Héritage Simple et Multiple

L'héritage permet à une classe d'hériter des propriétés et des méthodes d'une autre classe, ce qui évite de réécrire du code redondant. En PHP, l'héritage se fait par l'utilisation du mot-clé `extends`.

#### Héritage Simple

L'héritage simple consiste en une classe enfant (ou dérivée) qui hérite des caractéristiques d'une seule classe parent (ou base). Par exemple :

```php
<?php
class ParentClass {
    public $property = 'valeur par défaut';

    public function method() {
        echo 'Méthode de la classe parent';
    }
}

class ChildClass extends ParentClass {
    public function displayProperty() {
        echo $this->property;
    }
}

$child = new ChildClass();
$child->displayProperty(); // Affiche 'valeur par défaut'
?>
```

Dans cet exemple, `ChildClass` hérite de la propriété `$property` et de la méthode `method()` de `ParentClass`. La classe enfant peut également redéfinir ou surcharger les méthodes de la classe parent si nécessaire.

#### Héritage Multiple

Contrairement à certains autres langages orientés objet, PHP ne supporte pas directement l'héritage multiple (c'est-à-dire hériter de plusieurs classes à la fois). Cependant, PHP propose une solution élégante via les *traits*. Un *trait* est un mécanisme de réutilisation du code dans une classe qui permet d'inclure des méthodes dans différentes classes.

```php
<?php
trait TraitA {
    public function methodA() {
        echo 'Méthode A du TraitA';
    }
}

trait TraitB {
    public function methodB() {
        echo 'Méthode B du TraitB';
    }
}

class MyClass {
    use TraitA, TraitB;
}

$object = new MyClass();
$object->methodA(); // Affiche: Méthode A du TraitA
$object->methodB(); // Affiche: Méthode B du TraitB
?>
```

Avec les *traits*, vous pouvez simuler un héritage multiple en combinant les fonctionnalités de plusieurs traits dans une seule classe.

### Encapsulation et Abstraction

L'encapsulation et l'abstraction sont deux autres concepts clés de la POO qui visent à protéger et à organiser les données de vos classes.

#### Encapsulation

L'encapsulation consiste à restreindre l'accès direct aux propriétés et méthodes d'une classe, en les rendant privées ou protégées, et à exposer uniquement ce qui est nécessaire à l'extérieur de la classe. En PHP, cela est réalisé par les modificateurs d'accès : `public`, `protected` et `private`.

- `public` : accessible depuis n'importe où (de l'intérieur comme de l'extérieur de la classe).
- `protected` : accessible uniquement depuis l'intérieur de la classe elle-même et de ses sous-classes.
- `private` : accessible uniquement depuis l'intérieur de la classe elle-même.

```php
<?php
class MyClass {
    public $publicProperty = 'public';
    protected $protectedProperty = 'protected';
    private $privateProperty = 'private';

    public function getPrivateProperty() {
        return $this->privateProperty;
    }
}

$object = new MyClass();
echo $object->publicProperty; // OK
// echo $object->protectedProperty; // Erreur
// echo $object->privateProperty; // Erreur
echo $object->getPrivateProperty(); // OK, via méthode publique
?>
```

### Abstraction

L'abstraction consiste à définir des classes qui ne peuvent pas être instanciées directement, mais qui servent de modèles pour d'autres classes. En PHP, cela se fait à travers les classes abstraites et les interfaces.

#### Classes Abstraites

Une classe abstraite est une classe qui ne peut pas être instanciée et qui peut contenir des méthodes abstraites. Une méthode abstraite est une méthode déclarée mais non définie, c'est-à-dire sans corps. Les sous-classes qui héritent de la classe abstraite doivent implémenter les méthodes abstraites.

```php
<?php
abstract class AbstractClass {
    abstract protected function abstractMethod();

    public function concreteMethod() {
        echo 'Méthode concrète de la classe abstraite';
    }
}

class ConcreteClass extends AbstractClass {
    protected function abstractMethod() {
        echo 'Implémentation de la méthode abstraite';
    }
}

$object = new ConcreteClass();
$object->abstractMethod(); // Affiche: Implémentation de la méthode abstraite
$object->concreteMethod(); // Affiche: Méthode concrète de la classe abstraite
?>
```

### Interfaces

Une interface est semblable à une classe abstraite, mais elle ne peut contenir que des méthodes abstraites (sans implémentation) et des constantes. Les classes qui implémentent une interface doivent définir toutes les méthodes de l'interface. Une classe peut implémenter plusieurs interfaces, ce qui permet de contourner la limitation de l'héritage simple en PHP.

```php
<?php
interface InterfaceA {
    public function methodA();
}

interface InterfaceB {
    public function methodB();
}

class MyClass implements InterfaceA, InterfaceB {
    public function methodA() {
        echo 'Méthode A implémentée';
    }

    public function methodB() {
        echo 'Méthode B implémentée';
    }
}

$object = new MyClass();
$object->methodA(); // Affiche: Méthode A implémentée
$object->methodB(); // Affiche: Méthode B implémentée
?>
```

L'utilisation des interfaces encourage une architecture flexible et modulaire, permettant aux développeurs de créer des systèmes qui respectent le principe de séparation des responsabilités.

#### 3.2.3 Polymorphisme

Le polymorphisme permet à une classe d’être utilisée comme une autre classe, généralement en se basant sur des interfaces ou des classes parent. Cela permet à des objets de différentes classes d’être traités de manière uniforme tout en réagissant de manière spécifique à leur propre implémentation.

```php
<?php
interface Animal {
    public function makeSound();
}

class Dog implements Animal {
    public function makeSound() {
        echo 'Woof!';
    }
}

class Cat implements Animal {
    public function makeSound() {
        echo 'Meow!';
    }
}

function animalSound(Animal $animal) {
    $animal->makeSound();
}

animalSound(new Dog()); // Affiche: Woof!
animalSound(new Cat()); // Affiche: Meow!
?>
```

Dans cet exemple, la fonction `animalSound()` peut accepter n'importe quel objet implémentant l'interface `Animal`, et appeler la méthode `makeSound()` appropriée, même si chaque implémentation est spécifique à une classe.

### Conclusion

L'héritage et le polymorphisme, combinés avec l'encapsulation et l'abstraction, sont des concepts puissants en PHP pour organiser et réutiliser le code de manière efficace. Ils permettent non seulement de réduire la duplication du code, mais aussi de rendre le code plus flexible et plus facile à maintenir. En maîtrisant ces concepts, vous serez capable de concevoir des systèmes orientés objet robustes et modulaires.