# Bandeau de cookies

Le bandeau de cookies est géré grâce à plusieurs fichiers :&#x20;

* bandeau\_cookies.js
* footer.php
* header.php

La logique est la suivante :&#x20;

0/ Les cookies sont des lignes de code écrites en back office, qui sont chargées dans header.php. Par défaut elles sont bloquées par une condition PHP, qui peut être débloquée par l'utilisateur en acceptant les cookies.

1/ L'administrateur remplit en back office les cookies qu'il souhaite ajouter au site internet (Pixel Facebook, Google Ads, Google Analytics). Il définit aussi la durée de validité des cookies, le nom des cookies, etc.

2/ Les variables sont récupérées en PHP dans footer.php et transformées en variable JS. Le fichier bandeau\_cookies.js est chargé et les variables sont récupérées.

3/ Le fichier bandeau\_cookies (fonctionnement détaillé ci-dessous) crée les cookies et gère la bannière.

4/ Lorsque l'utilisateur accepte les cookies, la page est rechargée et les cookies, s'ils sont acceptés, vont donc être écrit en début de page (voir étape 0).

### Bandeau\_cookies.js

Cette classe permet de gérer le bandeau. Ce fichier est chargé dans wp\_footer(). Les variables en argument (cookieName, durationAccepted, durationRefused) sont créées juste avant le wp\_footer() dans le fichier **footer.php.** Elles contiennent des variables PHP dont le contenu est écrit en backoffice.

Voici les méthodes de cette classe :&#x20;

* initialiseCookieBanner : initialise le bandeau de cookies si des cookies ont été activés en back office du site. Vérifie aussi que les cookies n'ont pas déjà été acceptés (si c'est le cas, la bannière, est cachée).
* checkCookie(name) : vérifie si le cookie est déjà présent dans le navigateur de l'utilisateur
* displayBanner : afficher le bandeau de cookies
* displayChoseCookies : affiche le menu de choix des cookies
* closeBanner : ferme l'accueil du bandeau
* closeChoseCookies : ferme la fenêtre de choix des cookies
* createCookie(name, value, duration) : crée le cookie et l'écrit dans le navigateur de l'utilisateur ; les valeurs des arguments sont précisées dans le back office du site.
* acceptAll : valide la création de tous les cookies possibles
* refuse : lance la méthode "createCookies" et génère des cookies avec la valeur "false", ce qui permet au rechargement de la page de ne pas charger de nouveau la bannière.&#x20;
* handleSwitch : gère les switch du panneau avec les choix des différents cookies
* acceptCookies : accepte les cookies validés par les switchs
* back : gestion du bouton de retour en arrière du panneau de choix des cookies au panneau principal&#x20;

