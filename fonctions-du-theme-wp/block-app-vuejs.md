# Block app / VueJS

**Résumé :**&#x20;

`Le code de l'app se trouve dans nanosite-proefficace-child/vue-app`

`Le code du block qui le gère est nanosite-proefficace-child/inc/blocks/block-app.php`

`Chaque thème enfant a son app, donc chaque app est différente, mais un travail dans le sens d'une uniformisation des app est en cours`

`Fonctionne avec Vite.`

`npm i => installer le projet`

`npm run serve => lance un serveur local`

`npm run build => compile l'application`

`L'application est compilée dans son dossier dist, et le block ACF block-app.php vient récupérer le contenu du dist grâce à ces deux lignes :`&#x20;

```php
wp_enqueue_script('vue-app-js', get_stylesheet_directory_uri() . '/vue-app/dist/assets/index.js');
wp_enqueue_style('vue-app-css', get_stylesheet_directory_uri() . '/vue-app/dist/assets/index.css');
```

Le bloc App / VueJS a été crée dans le but d'avoir une alternative plus moderne et légère à un bloc conçu en PHP qui permettrait d'afficher et de filtrer les posts.

L'approche en PHP était complexe et alambiquée, et mélangeait du JS, du PHP, de l'Ajax... Désormais, une application unique se trouve dans le thème enfant, à ce chemin : nanosite-proefficace-child/vue-app

Plusieurs sites installés au cours de l'année 2022 / 2023 utilisent cette application :&#x20;

* reseaugrabuge.com
* isfec-bretagne.org
* naviso.fr&#x20;
* petitbilly.com
* maisonbordier.com
* useweb.fr

Le thème enfant de chacun de ces sites étant unique, le code de l'app VueJS l'est aussi, car il s'adapte aux contextes de ces sites, les custom post types concernés par le filtre et l'affichage, mais aussi, les filtres (à plusieurs étages, en mode multi-select, ou bien avec une input de recherche).&#x20;

Cependant, l'architecture globale est ressemblante : le composant showCpt.vue centralise beaucoup de logique : il récupère les custom post type grâce à l'API Rest de WordPress, les transforme au besoin, puis les stocks dans ses data.&#x20;

Idée d'évolution : créer une application unique pour tous les nanosites, qui serait un submodule du thème enfant. Eventuellement baser a logique sur les computed properties et les v-model plutôt que sur v-show.

## Endpoint custom :&#x20;

Un endpoint custom a été mis en place pour cette app, il s'appelle :

<pre class="language-php"><code class="lang-php"><strong>custom_taxonomy_terms_by_post_type_endpoint
</strong></code></pre>

Ce endpoint récupère toutes les taxonomies, les terms associés à ces taxonomies, et en fait un fichier JSON unique.

## Bordier&#x20;

Pour le site maisonbordier.com, le endpoint custom sur les taxonomies a été transformé pour permettre de répondre au problème causé par l'ajout de Polylang sur le site. La fonction qui crée le endpoint s'appelle&#x20;

## **CSS du block-app**

Dans un soucis de cohérence, le CSS du block-app est géré comme tous le reste du CSS du site : dans le dossier nanosite-proefficace-child/scss, plutôt que dans les composants Vue.

Il existe du CSS au sein des composants Vue, mais je recommande de ne pas l'utiliser et de le commenter s'il ne l'est pas déjà. Cependant, le CSS des composants Vue peut-être utile en cas de débuggage ou d'ajout de fonctionnalités de l'application : lorsqu'on lance la commande NPM run serve, on lance un serveur local et l'application, et le CSS qui est lu est celui des composants, pas celui du site. Il peut donc être utile de le décommenter dans ce cas de figure.

## **Pour l'adapter à un nouveau site**

Pour tester l'app en local, il est possible d'utiliser la commande `npm run dev` pour afficher l'application et la recharger à la volée. Cependant il y a quelques fichiers à modifier pour qu'elle fonctionne correctement : &#x20;

* Tout d'abord, l'application en état de dév utilise le fichier vue-app/index.html, qui contient le code html généré par un bloc PHP. C'est à dire qu'il faut créer le bloc PHP qui contient l'app, récupérer le code JSON généré par le bloc, et le coller à la place de celui présent dans index.html, pour simuler la présence d'un bloc Gutenberg dans index.html. L'application va ainsi utiliser ces données pour générer le code.
* Ensuite, il faut modifier l'adresse du host dans le fichier vue-app/src/helpers/cleanUrl.js. Il y a une condition qui vérifie si on se trouve en localhost. Si c'est le cas, alors il faut renseigner le bon "pathname".&#x20;
* Il faut ensuite faire la requête fetch sur le bon endpoint. A vérifier si dans la version de l'app que vous avez entre les mains, il n'y a pas un custom endpoint qui est fetché. Un endpoint par défaut pour les publications est mon-site.fr/wp-json/wp/v2/mon-type-de-publication
