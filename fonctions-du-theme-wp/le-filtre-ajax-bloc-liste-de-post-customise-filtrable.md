# Le filtre ajax (bloc "liste de post customisé filtrable")

_**Note :**_ _**Ce bloc, trop complexe à mettre en place et à maintenir, est en cours de remplacement par un bloc contenant une app VueJS, appelé "Block-app"**_

Lorsqu’on veut créer un filtre Ajax avec plusieurs taxonomies sur le Nanosite, il suffit de rajouter créer un bloc Gutenberg “Bloc listant les articles customisés filtrables”.

Ce bloc fait plusieurs choses : Il peut lister un certain type de publication Il peut lister une taxonomie (liée à la publication) Il peut lister un term

Lorsqu’on choisit de filtrer un type de publication, on peut choisir d’afficher un filtre, qui permettra de filtrer selon une taxonomie liée à la publication, puis on peut choisir d’afficher un deuxième étage au filtre, qui filtrera une deuxième taxonomie liée à la publication.

Enfin, il existe la possibilité de choisir quel type d’extrait on souhaite utiliser pour afficher nos extraits dans le filtre.

Les fichiers permettant de faire fonctionner ce bloc sont les suivants :

Des fichiers PHP :

inc/blocks/block-cpt-list-filterable.php : il contient le code du bloc Gutenberg, qui affiche la liste des publications, les filtres… functions/filter/ajax-call-without-filters.php : il contient le code PHP qui va être utilisé lors d’une requête AJAX sans filtres (essentiellement pour charger de nouveaux éléments) functions/filter/ajax-call.php : contient le code PHP permettant de filtrer les éléments et d’en charger davantage

Un fichier JS : js/ark\_filter.js : il contient le code permettant de gérer l’interface du filtre et d’effectuer les requête AJAX en JavaScript
