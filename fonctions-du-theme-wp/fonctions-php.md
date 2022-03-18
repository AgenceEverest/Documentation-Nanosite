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

### ACF-nanosite-options.php

### ACF-nanosite.php

### admin-editor-styles.php

### admin-nanosite-notice.php

### admin-register-menus.php

### base-clean-wp.php

### base-enqueue-scripts.php

### base-featured-images.php

### base-enqueue-styles.php

### base-image-custom-size.php

### base-title-404.php

### clean-antispam.php

### customizer-scss.php

### ninja-forms-permissions.php

### yoast-meta-description.php







