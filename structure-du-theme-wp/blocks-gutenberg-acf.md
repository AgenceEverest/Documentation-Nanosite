# Blocks Gutenberg - ACF

**1 - Enregistrement du bloc**&#x20;

**2 - Faire apparaître le bloc**&#x20;

**3 - Lier le bloc à son template**&#x20;

Une douzaine de blocs ont été créés :&#x20;

* Bloc - 1 colonne flexible
* Bloc - ancres
* Bloc - 2 colonnes flexibles
* Bloc - 3 colonnes flexibles
* Bloc - Multicolonnes&#x20;
* Bloc - 2 colonnes texte/visuel
* Bloc 2 colonnes texte/visuel (large)
* Bloc - Liste de posts / filtre&#x20;
* Bloc - Séparateur&#x20;

#### 1 - Enregistrement du bloc&#x20;

Ces blocs sont déclarés dans my\_acf\_init(), dans `functions/acf-nanosite-register-blocks.php`, avec ce type de fonction :&#x20;

`acf_register_block(array( 'name' => 'nom-du-bloc', 'title' => __('Nom du bloc'), 'description' => __('description du bloc'), 'render_callback' => 'block_callback', 'category' => 'layout', 'icon' => 'nom de l’icône', 'mode' => 'edit', ));`

#### 2 - Faire apparaître le bloc&#x20;

Les blocs sont cachés par défaut. Pour faire apparaître un nouveau bloc, il faut ajouter son “name” dans la fonction “my\_plugin\_allowed\_block\_types” dans `acf-nanosite-register-blocks.php,` précédé de “acf/”.

Exemple :&#x20;

`function my_plugin_allowed_block_types($allowed_block_types, $post) {`

`return array('core/paragraph', 'acf/bloc', 'acf/un-autre-bloc');`

`}`

#### 3 - Lier le bloc à son template&#x20;

La fonction block\_callback() récupère chaque nom de bloc nouvellement déclaré et le lie à un template.

Les templates se trouvent dans `inc/blocks.`

Chaque template est relié à un groupe de champs ACF, spécialement créé pour cela. Chaque template de bloc doit donc démarrer avec ces lignes de PHP :&#x20;

`if (have_rows('nom_du_groupe_de_champ')) : the_row();`&#x20;

&#x20;   `$var = get_sub_field('un_autre_champ');`&#x20;

`endif;`

Dans le back office Wordpress, il faut donc créer un nouveau groupe de champ par bloc, et faire correspondre son “emplacement” à un bloc, qui est égal au “title” du bloc qu’on a déclaré précédemment dans functions.php

![](https://lh4.googleusercontent.com/Dotz9Ops6IOSJ-ryLgNcFBH0T00BZWuAc2C2kZ4H-0kmE5lSQ0FrZYA2hIQDBCeTKE3QRQyqJ8InzupzyhxvGQ8LFnnukA36RG-m3dTxgPsgbdzEaYVNbbGkWCkERxvxH150tAa0)

Dans ce groupe de champ, il ne reste plus qu’à créer des sous-champs, qui apparaîtront à la fois dans le bloc Gutenberg, et dont chaque variable pourra être récupérée par le template qu’on a associé à notre bloc dans functions.php.
