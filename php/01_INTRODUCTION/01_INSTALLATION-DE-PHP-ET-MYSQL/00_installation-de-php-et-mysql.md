### 1.2 Installation de PHP et MySQL

#### Installation de PHP sur différents environnements (Windows, Mac, Linux)

Pour développer des applications web en PHP, il est essentiel d'installer PHP sur votre machine. Le processus d'installation varie en fonction du système d'exploitation que vous utilisez.

##### 

##### Installation de PHP sur Linux

1. **Installation via le gestionnaire de packages** :

   - Sur Linux, la méthode la plus simple pour installer PHP est d'utiliser le gestionnaire de packages de votre distribution.

     - **Ubuntu/Debian** :

       ```
       
       ```

       Copier le code

       `sudo apt update sudo apt install php libapache2-mod-php`

     - **CentOS/RHEL** :

       ```
       bash
       ```

       Copier le code

       `sudo yum install php php-mysql`

   - Après l'installation, redémarrez Apache ou Nginx pour appliquer les changements.

2. **Installation manuelle** :

   - Pour une installation plus personnalisée, vous pouvez compiler PHP à partir des sources. Téléchargez le code source depuis le site officiel de PHP, extrayez les fichiers, et exécutez les commandes de compilation. Cela permet une installation de PHP sur mesure, bien que cela soit plus complexe et nécessite plus de configuration.

#### Installation et configuration de MySQL

MySQL est un système de gestion de bases de données relationnelles open source, largement utilisé avec PHP pour développer des applications web dynamiques.

##### Télécharger et installer MySQL

1. **Téléchargement de MySQL** :

   - Rendez-vous sur le site officiel de MySQL et téléchargez la version appropriée pour votre système d'exploitation (Windows, macOS, ou Linux).

2. **Installation sur Windows** :

   - Exécutez l'installateur téléchargé et suivez les instructions à l'écran. Vous pouvez opter pour une installation personnalisée ou utiliser les paramètres par défaut. Pendant l'installation, vous serez invité à configurer le mot de passe root et d'autres options de sécurité.

3. **Installation sur macOS** :

   - Vous pouvez installer MySQL via un package DMG téléchargé depuis le site officiel de MySQL ou utiliser Homebrew avec la commande suivante :

     ```
     bash
     ```

     Copier le code

     `brew install mysql`

   - Après l'installation, démarrez MySQL avec la commande :

     ```bash
     sudo apt update
     sudo apt install php libapache2-mod-php
     ```

     Copier le code

     `brew services start mysql`

4. **Installation sur Linux** :

   - Sur Ubuntu/Debian, installez MySQL avec les commandes suivantes :

     ```
     bash
     ```

     Copier le code

     `sudo apt update sudo apt install mysql-server`

   - Pour CentOS/RHEL :

     ```
     bash
     ```

     Copier le code

     `sudo yum install mysql-server`

   - Une fois installé, démarrez le service MySQL et configurez-le en utilisant `mysql_secure_installation`.

##### Configuration de base via le terminal ou un client MySQL tel que phpMyAdmin

1. **Configuration via le terminal** :

   - Après l'installation, vous pouvez configurer MySQL en utilisant le terminal. Connectez-vous à MySQL en utilisant la commande suivante :

     ```
     bash
     ```

     Copier le code

     `mysql -u root -p`

   - Vous pouvez ensuite exécuter des commandes SQL pour créer des bases de données, des utilisateurs, et gérer les permissions.

2. **Utilisation de phpMyAdmin** :

   - **phpMyAdmin** est une interface web pour MySQL qui facilite la gestion de vos bases de données. Pour l'utiliser, vous devez d'abord installer et configurer phpMyAdmin. Une fois installé, vous pouvez accéder à phpMyAdmin via votre navigateur et utiliser son interface graphique pour créer et gérer des bases de données, des utilisateurs, et d'autres configurations MySQL.

L'installation et la configuration de PHP et MySQL sont des étapes cruciales pour tout développeur web. Ces outils forment la base de nombreuses applications web dynamiques, et leur installation correcte est la première étape vers la création d'un environnement de développement fonctionnel.