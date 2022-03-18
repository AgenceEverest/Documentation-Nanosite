---
description: Gestion des contenus
---

# Blocks Gutenberg - ACF

**A - Les blocs Gutenberg**&#x20;

* 1 - Enregistrement du bloc&#x20;
* 2 - Faire apparaître le bloc&#x20;
* 3 - Lier le bloc à son template&#x20;

**B - JavaScript et CSS**&#x20;

* 1 - Injection d’un script pour modifier le bloc Gutenberg “Multicolonnes”&#x20;
* 2 - Ajout de CSS

### A - Les blocs Gutenberg&#x20;

Une douzaine de blocs ont été créés :&#x20;

* Bloc séparateur&#x20;
* Call-to-action 2 colonnes textes&#x20;
* 2 colonnes texte / visuel&#x20;
* 2 colonnes texte / visuel (large)&#x20;
* Image(s)&#x20;
* bloc multicolonnes&#x20;
* bloc iframe (vidéos, autre)&#x20;
* bloc grand slider bloc témoignage&#x20;
* bloc questions réponses&#x20;
* bloc une colonne large&#x20;

#### 1 - Enregistrement du bloc&#x20;

Ces blocs sont déclarés dans my\_acf\_init(), dans `functions/acf-nanosite-register-blocks.php`, avec ce type de fonction :&#x20;

`acf_register_block(array( 'name' => 'nom-du-bloc', 'title' => __('Nom du bloc'), 'description' => __('description du bloc'), 'render_callback' => 'block_callback', 'category' => 'layout', 'icon' => 'nom de l’icône', 'mode' => 'edit', ));`

#### 2 - Faire apparaître le bloc&#x20;

Les blocs sont cachés par défaut. Pour faire apparaître un nouveau bloc, il faut ajouter son “name” dans la fonction “my\_plugin\_allowed\_block\_types” dans `acf-nanosite-register-blocks.php,` précédé de “acf/”.

Exemple :&#x20;

function my\_plugin\_allowed\_block\_types($allowed\_block\_types, $post) {

```
return array('core/paragraph', ‘acf/bloc’, ‘acf/un-autre-bloc’);
```

}&#x20;

3 - Lier le bloc à son template&#x20;

La fonction block\_callback() récupère chaque nom de bloc nouvellement déclaré et le lie à un template.

Les templates se trouvent dans welligo/inc/blocks.

Chaque template est relié à un groupe de champs ACF, spécialement créé pour cela. Chaque template de bloc doit donc démarrer avec ces lignes de PHP : if (have\_rows('nom\_du\_groupe\_de\_champ')) : the\_row(); $var = get\_sub\_field('un\_autre\_champ'); endif;

Dans le back office Wordpress, il faut donc créer un nouveau groupe de champ par bloc, et faire correspondre son “emplacement” à un bloc, qui est égal au “title” du bloc qu’on a déclaré précédement dans functions.php :

Dans ce groupe de champ, il ne reste plus qu’à créer des sous-champs, qui apparaîtront à la fois dans le bloc Gutenberg, et dont chaque variable pourra être récupérée par le template qu’on a associé à notre bloc dans functions.php.

B - JavaScript et CSS 1 - Injection d’un script pour modifier le bloc Gutenberg “Multicolonnes” Un script se trouvant dans welligo/js/gutenberg\_custom.js est injecté via la fonction gutenberg\_custom() dans functions.php.

```
Pour que ce script fonctionne, l’ID “gutenbergMulticolonne” doit avoir été indiqué au niveau des attributs du conteneur du sous-champ “Grille (nombre de colonnes par rangée)” dans le groupe de champ “Bloc - multi-colonnes”.

Il faut aussi que dans la partie “choix” la clé indique combien de colonnes on aura (exemple : “rangee_de_2”, car le script récupère le dernier caractère de cette valeur). 
```

(Idée d’amélioration pour ce script : créer un sous champs qui indiquera combien de colonnes on veut afficher dans notre bloc, et qu’on récupérera via le script ?)

2 - Ajout de CSS Modification mineure dans welligo/css/admin.css pour modifier le bloc Gutenberg Multicolonne
