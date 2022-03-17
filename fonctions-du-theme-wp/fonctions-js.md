# Fonctions JS

## Barre de recherche du header

`function lancerRecherche()`

Vérifie que la barre de recherche du Nanosite n'est pas déjà ouverte et, dans le cas contraire, fait apparaître un masque gris, change le bouton de recherche en une croix, etc.

Permet également d'adapter la barre de recherche à la présence de la barre d'administration WordPress si l'utilisateur est connecté au back office.

## Chargement des iframes vidéos 

`function videosIframe()`

Fonction qui va d'abord récupérer toutes les vidéos sur la page (elles peuvent être retrouvées grâce à une classe commune), les stocker dans un tableau, puis itérer sur ce tableau pour vérifier s'il s'agit d'une vidéo YouTube ou Viméo.

En fonction de la nature de la vidéo, différents traitements vont être appliqués, mais dans les deux cas un iframe va être créé et des valeurs vont être récupérées sur la balise HTML récupérée initialement.

Ces valeurs sont liées à des attributs. Elles proviennent du backoffice de Wordpress. Par exemple, lorsque l'utilisateur entre le lien de la vidéo YouTube qu'il souhaite ajouter sur la page, ce lien va aller dans l'attribut de la balise HTML récupérée par le script JS, qui va s'en servir pour créer l'Iframe.

## Taille du logo dans le header

`function cssLogoHeader()`

Modifie la taille du logo dans le header en fonction de la taille de la fenêtre, mais aussi en fonction du scroll de l'utilisateur.

## Modification des flêches de navigation dans la pagination du blog

`function modifierFlechesNavigation()`

Tranforme les flèches par défaut en "Suivant >" et "Précédent <".

## Retour en haut + label Nanosite

`function retourEnHaut()`

Gère le bouton de retour tout en haut de la page + le label nanosite qui doit se trouver en bas à gauche. Ces deux boutons apparaissent et disparaissent au scroll, à partir d'un certain endroit (triggerPoint). La fonction gère aussi le bouton de retour en haut de la page.

## Suppression des paragraphes vides

`function supprimerParagraphesVides()`

Récupère toutes les balises `<p>` et, si elles sont vides, les supprime.

## Suppression des title sur les images

`function supprimerTitleDesImages()`

Récupère les balises img et supprimer les balises title au mouseover (la remet au mouseout). Le but est d'éviter la petite infobulle lorsque le curseur passe dessus, tout en gardant le title pour les lecteurs d'écran. 

## Faire apparaître le numéro de téléphone dans le Header

`function clickTelephone()`

Active avec un click event la div contenant le téléphone.

## Menu Burger

`function menuBurger()`

Fonction chargée lorsque la fenêtre est chargée. Gère l'ouverture et la fermeture du menu burger mobile ; gère également la présence d'une barre d'administration Wordpress.

## Redimensionnement d'une colonne de double largeur

`function resizeColonneDoubleLarge()`

Fonction chargée normalement, mais aussi lors de l'event "resize" (redimensionnement de la fenêtre). 
Redimensionne des div contenant certaines classes à la taille du content_width (classe principale pour avoir une taille correcte sur les éléments prenant toute la largeur de la fenêtre).

## Ajout de classes CSS

`function ajoutDeClasses()`

Ajoute des classes numérotées de 1 à 3 sur les extraits d'articles.

## Padding et margin corrigé

`function changeEntryContentCss()`

Met les padding et margin des premiers et derniers éléments de .entry-content (une catégorie de contenu Wordpress très utilisées) à 0.

## Bloc Questions / Réponses

`function blocQuestionReponse()`

Gère l'ouverture et la fermeture des blocs questions réponses, au clic.

## Label Nanosites

`function consommationCarbonne()`

Récupère la valeur du poids en carbone (qui est contenu dans la page) et l'affiche sur le logo Nanosite (en bas à gauche). Mais la valeur est visible seulement quand la souris se trouve sur le logo (ou l'écran touché, sur les écrans tactiles).

## Afficher le poids des images au survol de l'image nanosite

`function poidsImageHover()`

Affiche le poids de l'image lorsque le logo Nanosite est survolé (ou touché, sur les écrans tactiles).

## Remplacer l'espace devant certains caractères par un insécable

`function remplacerEspacesParInsecables()`

Remplace l'espace devant les éléments p, li, h1...h6 dans la div global_content (conteneur de tous le contenu de la page) par un espace insécable.

## Charger les images sur les extraits d'articles (Aside et Blog)

`function chargerLesImages()`

Modifie l'attribut "src" d'une image au clic sur un bouton, ce qui permet de charger dynamiquement une image (localisée dans les erxtraits d'articles).

## Menu principal responsive

`function menuPrincipalResponsiveScroll()`

Gère la largeur du menu, la largeur du contenu et la largeur du logo header selon un trigger point de 400px (au-dessus ou en dessous de ce trigger point).

La fonction gère le comportement au chargement, au resize, puis selon la trigger point.

La fonction est chargée quand toute la fenêtre est chargée, puis quand la fenêtre est rediensionnée.

## Redimensionnement des logos de certification du prefooter 

`function logoPreFooter()`

Redimensonne les balises entourant les logos de certification du prefooter en fonction de leur format (vertical ou horizontal).

