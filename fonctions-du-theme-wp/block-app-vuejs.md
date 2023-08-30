# Block app / VueJS

`Fonctionne avec Vite.`

`npm i => installer le projet`

`npm run serve => lance un serveur local`

`npm run build => compile l'application`

`L'application est compilée dans son dossier dist, et le block ACF block-app.php bien récupérer le contenu du dist grâce à ces deux lignes :`&#x20;

```php
wp_enqueue_script('vue-app-js', get_stylesheet_directory_uri() . '/vue-app/dist/assets/index.js');
wp_enqueue_style('vue-app-css', get_stylesheet_directory_uri() . '/vue-app/dist/assets/index.css');
```

Le bloc App / VueJS a été crée dans le but d'avoir une alternative plus moderne et légère (en tout cas pour l'utilisateur) à un bloc conçu en PHP qui permettrait d'afficher et de filtrer les posts.

L'approche en PHP était complexe et alambiquée, et mélangeait du JS, du PHP, de l'Ajax... Désormais, une application unique se trouve dans le thème enfant, à ce chemin : nanosite-proefficace-child/vue-app

Plusieurs sites installés au cours de l'année 2022 / 2023 utilisent cette application :&#x20;

* reseaugrabuge.com
* isfec-bretagne.org
* naviso.fr&#x20;
* petitbilly.com
* lebeurrebordier.com

Le thème enfant de chacun de ces sites étant unique, le code de l'app VueJS l'est aussi, car il s'adapte aux contextes de ces sites, les custom post types concernés par le filtre et l'affichage, mais aussi, les filtres (à plusieurs étages, en mode multi-select, ou bien avec une input de recherche).&#x20;

Cependant, l'architecture globale est ressemblante : le composant showCpt.vue centralise beaucoup de logique : il récupère les custom post type grâce à l'API Rest de WordPress, les transforme au besoin, puis les stocks dans ses data.&#x20;

Idée d'évolution : créer une application unique pour tous les nanosites, qui serait un submodule du thème enfant. Eventuellement baser a logique sur les computed properties et les v-model plutôt que sur v-show.

## **CSS du block-app**

Dans un soucis de cohérence, le CSS du block-app est géré comme tous le reste du CSS du site : dans le dossier nanosite-proefficace-child/scss, plutôt que dans les composants Vue.

Il existe du CSS au sein des composants Vue, mais je recommande de ne pas l'utiliser et de le commenter s'il ne l'est pas déjà. Cependant, le CSS des composants Vue peut-être utile en cas de débuggage ou d'ajout de fonctionnalités de l'application : lorsqu'on lance la commande NPM run serve, on lance un serveur local et l'application, et le CSS qui est lu est celui des composants, pas celui du site. Il peut donc être utile de le décommenter dans ce cas de figure.