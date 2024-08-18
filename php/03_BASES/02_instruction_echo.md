#### 2.1.2 Instructions

Les instructions sont des commandes qui sont exécutées par l'interpréteur PHP. Chaque instruction doit se terminer par un point-virgule `;`. Voici un exemple d'instruction simple :

```php
echo "Hello, World!";
```

Dans cet exemple, `echo` est une instruction qui affiche le texte `Hello, World!` à l'écran. Notez que les instructions PHP sont sensibles à la casse, c'est-à-dire que `echo` et `Echo` sont deux instructions différentes.

Les instructions peuvent être combinées sur une seule ligne en les séparant par des points-virgules :

```php
echo "Hello, ";
echo "World!";
```

Cependant, il est plus courant de les combiner sur une seule ligne en les séparant par des points-virgules :

```php
echo "Hello, "; echo "World!";
```

Il est également possible la syntaxe alternative pour les instructions PHP, qui consiste à utiliser les balises `<?` et `?>` :

```php
<? "Hello, World!" ?>
```

Cette syntaxe est moins courante et peut ne pas être prise en charge par tous les serveurs. Elle est l'équivalent de la syntaxe standard `<?php echo "Hello, World!"; ?>`.