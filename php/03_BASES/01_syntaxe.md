## Syntaxe de base

PHP utilise une syntaxe simple et intuitive qui permet d'intégrer du code directement dans un fichier HTML. Le code PHP est délimité par les balises `<?php` et `?>`. Tout ce qui est en dehors de ces balises est traité comme du HTML normal.

Une autre syntaxe, plus courte, consiste à utiliser les balises `<?` et `?>`. Cependant, cette syntaxe est moins courante et peut ne pas être prise en charge par tous les serveurs.

### Commentaires

Les commentaires sont des parties du code qui ne sont pas exécutées par l'interpréteur PHP. Ils servent à documenter le code pour le rendre plus lisible et compréhensible pour les autres développeurs (ou pour vous-même à une date ultérieure). PHP offre trois types de commentaires :

- **Commentaires sur une seule ligne :** Utilisez `//` ou `#` pour commenter une seule ligne.

```php
// Ceci est un commentaire sur une seule ligne
# Ceci est un autre commentaire sur une seule ligne
```

- **Commentaires sur plusieurs lignes :** Utilisez `/* */` pour commenter plusieurs lignes.

```php
/*
 * Ceci est un commentaire sur plusieurs lignes.
 * Il peut couvrir autant de lignes que nécessaire.
 */
```

- **Commentaires de documentation :** Utilisez `/** */` pour commenter une fonction ou une classe. Ces commentaires sont utilisés pour générer automatiquement de la documentation à partir du code.

```php
/**
 * Ceci est un commentaire de documentation.
 * Il est utilisé pour documenter une fonction ou une classe.
 */
```