# Gestion et compilation du SCSS

### **Organisation**

Le style du nanosite est géré à l'aide du langage Sass.&#x20;

Un style de base se trouve dans le dossier nanosite-proefficace/sass, dans le thème parent.

Pour toute personnalisation d'un site, il faut travailler dans le dossier Sass du thème enfant (nanosite-proefficace-child/scss).

Ce code Sass est compilé dans le dossier /css/, que ce soit dans le thème parent ou dans le thème enfant.&#x20;

Le thème charge deux fichier CSS compilé : main.css, pour le thème parent, et mainchild.css pour le thème enfant. Dans le thème parent, d'autres fichiers CSS sont chargés (admin.css, variables.css, login.css...).

### Variables SASS

Les variables SASS de l'ensemble du thème se trouvent dans le thème enfant. Une copie de sauvegarde se trouve dans le thème parent. Quand le code du site est compilé, ce sont les variables présentes dans le dossier du thème enfant qui sont utilisées pour le code SASS du thème parent.

On peut modifier la valeur de ces variables, mais il ne faut pas les supprimer ni modifier leur nom.

Il est par contre possible d'en créer de nouvelles, pour les besoins du thème enfant.

### Compilation du code SASS

Il est possible de compiler le code SASS de deux façon. En étant connecté à l'admin, une barre apparaît en bas du site en front, pour compiler avec ou sans sourcemapping.

![](<.gitbook/assets/Capture d’écran 2022-07-29 à 15.39.00.png>)

Pour activer cette barre, il faut aller dans le back office -> Customisation -> développement et activer "Afficher les infos du responsive"&#x20;

![](<.gitbook/assets/Capture d’écran 2022-07-29 à 15.50.41.png>)

Il est aussi possible de compiler le code SASS en allant dans la page d'accueil du backoffice

![](<.gitbook/assets/Capture d’écran 2022-07-29 à 15.49.21.png>)

Le code SASS est compilé à l'aide de la librairie SCSSPHP, dans le fichier nanosite-proefficace/functions/customizer.scss.php

* Cette fonction compile le CSS du thème parent et du thème enfant. Elle utilise la librairie PHP "SCSSPHP" qui se trouve dans functions/scssphp. La doc de cette librairie se trouve ici : https://scssphp.github.io/scssphp/
* Cette fonction est lancée au clic sur les formulaires qui se trouve dans inc/css-compil-footer.php
* Elle lance la compilation du css via css\_compil avec (true) ou sans (false) sourcemapping du code SASS
* Dans cette fonction, on compile d'abord le code du thème parent, puis celui du thème enfant
* La compilation à proprement parler se trouve dans la fonction compil() avec tous ses arguments (le compiler, le fichier CSS à compiler, la cible, le sourcemappping)
* Cette fonction est un try / catch. Le catch permet de renvoyer les erreurs de compilation Sass en alert JS dans le navigateur.
* La minification du CSS est désactivée si l'on compile avec le sourcemapping, et elle est réactivée si on compile sans sourcemapping.
