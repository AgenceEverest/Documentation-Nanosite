# Gestion des champs ACF et des Blocks Gutenberg

**TL;DR : quand on customise dans le thème enfant un bloc Gutenberg présent dans le thème parent, il faut faire attention à ne pas mettre à jour le groupe de champs ACF associé à ce bloc.**

**Cette partie du Nanosite est en chantier, versionner les champs ACF est l'un des objectifs de développement du Nanosite**

La gestion des champs ACF et des blocs Gutenberg pose quelques problèmes avec le versionning. Pour l'instant la logique est la suivante :&#x20;

* Un nouveau Nanosite (donc créé à partir de childtheme.nanosite.tech) dispose d'un ensemble de blocs de base qui sont les suivants :&#x20;
  * Bloc - 1 colonne flexible
  * Bloc - ancres
  * Bloc - 2 colonnes flexibles
  * Bloc - 3 colonnes flexibles
  * Bloc - Multicolonnes&#x20;
  * Bloc - 2 colonnes texte/visuel
  * Bloc 2 colonnes texte/visuel (large)
  * Bloc - Liste de posts / filtre&#x20;
  * Bloc - Séparateur&#x20;

<mark style="color:orange;">**Nota bene :**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">un groupe de champs, appelé "Colonne flexible clonable", est la base des blocs comportant des colonnes flexible. Modifier ce groupe de champs revient à modifier tous les blocs contenant une colonne flexible.</mark>

Lorsqu'on développe un Nanosite, il est possible de mettre à jour le thème parent du site, et donc les fichiers servant à afficher ces blocs. Mais si l'on met à jour les fichiers PHP, il faut aussi mettre à jour les champs ACF du site.

Il est tout à fait possible de modifier les blocs d'origine dans le thème enfant, **mais il faudra faire bien attention à "figer" les champs ACF de ce bloc customisé, et à ne pas les mettre à jour, sous peine de perdre la customisation du bloc.**

Enfin, il est possible de déclarer de nouveaux blocs dans le thème enfant du site et de créer des groupes de champs ACF associés.



