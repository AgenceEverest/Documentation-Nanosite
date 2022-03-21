# Fonctions PHP

### Charger des SVG de façon sécurisée

**Fichier : base-inline-svg.php**

`load_inline_svg($filename)`

Cette fonction a pour but de charger des SVG de façon sécurisée. Il suffit de créer un dossier SVG à la racine du thème, d'y placer ses SVG puis de les charger à l'endroit où on le souhaite dans ses templates à l'aide de la fonction `<?= apply_filters('add_svg', 'nom_du_svg') ?>.` &#x9;

La variable svg\_path, qui retrouve le chemin vers le SVG, peut avoir besoin de subir des modifications selon le contexte. 							&#x9;

### Calculer le poids des images

**Fichier : base-inline-svg.php**

`return_weight_of_img($fileUrl)`

Fonction qui calcule le poids de l'image grâce à son URL et ses en-têtes et renvoie une string contenant le poids de l'image en kilobytes. Dans un template, il faut utiliser ce filter :&#x20;

apply\_filters('get\_weight\_of\_img', $url-de-l'image);

La façon de récupérer l'URL de l'image peut varier. Parfois il s'agit d'un champ ACF, d'autres cas sont sont plus complexes, comme lorsqu'il s'agit d'extraits d'articles (ici pour les offres) :&#x20;

```
<?php $image_alt = get_post_meta(get_post_thumbnail_id($post->ID), '_wp_attachment_image_alt', TRUE); ?>
<?php $image_weight = apply_filters('get_weight_of_img', $thumbnail['0']); ?>
```

### ACF-contact-form-prefill.php

Permet de pré-remplir le formulaire de contact.

### ACF-nanosite-options.php

Active la page d'options "Customisation du thème" dans le backoffice Wordpress.

### ACF-nanosite.php

Liste les les différents champs ACF au format PHP (peuvent être chargés en back office).

### admin-editor-styles.php

Ajoute une feuille de style à l'éditeur de texte du backoffice. Rajoute également des boutons à l'éditeur de texte.

### admin-nanosite-notice.php

### admin-register-menus.php

Enregistre les différents menus du nanosite (menu principal, menu mobile, menu footer).

### base-clean-wp.php

Nettoie l'installation Wordpress : supprime de nombreux script inutiles, le flux RSS, des ressources inutiles du header, désactive les emojis... Désactive aussi des feuilles de style inutiles (par exemple celles des blocs Gutenberg, mais aussi les commentaires.&#x20;

### base-enqueue-scripts.php

Installe jQuery sur les seules pages nécessaires (page de formulaire de contact).

### base-featured-images.php

### base-enqueue-styles.php

Ajoute les 2 feuilles de style nécessaires au site.

### base-image-custom-size.php

Ajoute les filtres permettant d'avoir les images de tailles customisées du thème.

### base-title-404.php

Modification du texte par défaut de la page 404.

### clean-antispam.php

Ajout du shortcode contre le spam dans le contact mail.

### customizer-scss.php

Fonction permettant à des utilisateurs de facilement customiser le CSS du Nanosite.

### ninja-forms-permissions.php

### yoast-meta-description.php







