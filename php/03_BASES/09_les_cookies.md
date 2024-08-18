### **Cours sur les Cookies en PHP**

#### **1. Introduction aux cookies**

Les **cookies** sont de petits fichiers texte stockés sur l'ordinateur de l'utilisateur par le navigateur web. Ils sont souvent utilisés pour conserver des informations sur une session utilisateur, personnaliser l'expérience de navigation, ou suivre le comportement sur un site web. Les cookies sont envoyés au serveur avec chaque requête HTTP, ce qui permet au serveur de "se souvenir" des utilisateurs entre les différentes pages ou visites.

#### **2. Comment fonctionnent les cookies ?**

Lorsqu'un utilisateur visite un site web, le serveur peut envoyer un cookie au navigateur avec une commande HTTP. Le navigateur stocke ce cookie localement et l'envoie automatiquement au serveur à chaque fois que l'utilisateur visite à nouveau ce site.

Un cookie contient généralement :

- **Nom** : le nom du cookie, utilisé pour le référencer.
- **Valeur** : la donnée stockée, souvent sous forme de chaîne de caractères.
- **Durée de vie** : la date d'expiration du cookie, après laquelle il est supprimé.
- **Domaine et chemin** : indiquent à quel domaine ou chemin le cookie doit être renvoyé.
- **Sécurité** : indique si le cookie doit être transmis uniquement via HTTPS.

#### **3. Créer et lire un cookie en PHP**

##### **3.1 Créer un cookie**

Pour créer un cookie en PHP, on utilise la fonction `setcookie()`. Voici comment cela fonctionne :

```php
<?php
setcookie("nom_du_cookie", "valeur_du_cookie", time() + 3600, "/");
```

**Explications** :

- **"nom_du_cookie"** : le nom du cookie.
- **"valeur_du_cookie"** : la valeur du cookie.
- `time() + 3600` : la durée de vie du cookie en secondes (ici 1 heure). `time()` retourne l'heure actuelle en secondes, et on y ajoute 3600 secondes (soit 1 heure).
- **"/"** : le chemin pour lequel le cookie est valide (ici, le chemin racine du site).

**Exemple pratique** :

```php
<?php
setcookie("user", "John Doe", time() + 86400, "/"); // Crée un cookie qui expire dans 24 heures
```

##### **3.2 Lire un cookie**

Pour lire un cookie en PHP, on utilise la superglobale `$_COOKIE`, qui est un tableau associatif contenant tous les cookies reçus par le serveur.

```php
<?php
if(isset($_COOKIE["user"])) {
    echo "User is: " . $_COOKIE["user"];
} else {
    echo "User is not set";
}
```

**Explications** :

- `isset($_COOKIE["user"])` : vérifie si le cookie nommé "user" existe.
- `$_COOKIE["user"]` : récupère la valeur du cookie "user".

##### **3.3 Modifier un cookie**

Pour modifier un cookie, il suffit de recréer le cookie avec le même nom mais une nouvelle valeur ou une nouvelle date d'expiration.

```php
<?php
setcookie("user", "Jane Doe", time() + 86400, "/"); // Met à jour le cookie "user"
```

##### **3.4 Supprimer un cookie**

Pour supprimer un cookie, on le recrée avec une date d'expiration passée. Ainsi, le navigateur le supprimera automatiquement.

```php
<?php
setcookie("user", "", time() - 3600, "/"); // Supprime le cookie "user"
```

**Explications** :

- `time() - 3600` : on fixe la date d'expiration à une heure passée.

#### **4. Utilisations courantes des cookies**

Voici quelques exemples d'utilisation des cookies dans les applications web :

- **Mémoriser les préférences de l'utilisateur** : comme la langue, le thème (clair ou sombre), etc.
- **Gérer les sessions utilisateur** : identifier les utilisateurs entre différentes pages sans nécessiter de connexion à chaque fois.
- **Suivre les comportements** : par exemple, pour des statistiques ou de la publicité ciblée.

#### **5. Limites et sécurité des cookies**

##### **5.1 Limites**

- **Taille** : un cookie ne peut pas dépasser 4 Ko, donc il ne doit pas stocker de grandes quantités de données.
- **Nombre** : un domaine ne peut pas stocker plus de 20 cookies par navigateur.
- **Dépendance au client** : les cookies peuvent être désactivés par l'utilisateur dans son navigateur.

##### **5.2 Sécurité**

- **Vol de cookies** : si un cookie contient des informations sensibles (comme un identifiant de session), il peut être volé par un attaquant via des failles comme le XSS (Cross-Site Scripting).
- **Transmission sécurisée** : pour les données sensibles, assurez-vous que les cookies ne sont envoyés que via HTTPS en utilisant l'option `secure`.
- **Protection contre les accès non autorisés** : Utilisez l'option `HttpOnly` pour empêcher l'accès au cookie via du JavaScript malveillant.

```php
<?php
setcookie("secure_cookie", "valeur_sensible", time() + 86400, "/", "", true, true);
// Le dernier 'true' active l'option HttpOnly
```

**Explications** :

- `true` **après le chemin** : indique que le cookie doit être envoyé uniquement sur une connexion sécurisée HTTPS.
- `HttpOnly` : empêche le cookie d'être accessible par des scripts côté client (JavaScript).

#### **6. Conclusion**

Les cookies sont un outil puissant pour rendre les sites web interactifs et personnalisés. Cependant, il est essentiel de les utiliser de manière sécurisée et de prendre en compte la vie privée des utilisateurs. En PHP, la manipulation des cookies est simple grâce à des fonctions intégrées comme `setcookie()` et la superglobale `$_COOKIE`. En comprenant bien comment fonctionnent les cookies, vous pouvez améliorer significativement l'expérience utilisateur sur votre site tout en respectant les meilleures pratiques de sécurité.