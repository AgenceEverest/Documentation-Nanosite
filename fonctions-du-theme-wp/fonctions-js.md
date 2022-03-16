# Fonctions JS

## Barre de recherche du header

`function lancerRecherche()`

Vérifie que la barre de recherche du Nanosite n'est pas déjà ouvert et, dans le cas contraire, fait apparaître un masque gris, change le bouton de recherche en une croix, etc.

Permet également d'adapter la barre de recherche à la présence de la barre d'administration WordPress si l'utilisateur est connecté au back office.


## Chargement des iframes vidéos 

`function videosIframe()`

Function qui va d'abord récupérer toutes les vidéos sur la page (elles peuvent être retrouvées grâce à une classe commune), les stocker dans un tableau, puis itérer sur ce tableau pour vérifier s'il s'agit d'une vidéo YouTube ou Viméo.

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

Récupère toutes les balises <p> et, si elles sont vides, les supprime.


## Suppression des title sur les images

`function supprimerTitleDesImages()`

Récupère les balises img et supprime les attributs title de celles-ci.

## Changer la taille du logo header
function changerTailleLogoHeader() {
    let triggerPoint = 400;
    let logoHeaderOnScroll = document.getElementById('logo_header_img_scroll');
    let logoHeaderAuDebut = document.getElementById('logo_header_img');
    let headerElt = document.getElementById('header');
    let comportementEnDessous = () => {
        logoHeaderOnScroll.style.display = "block";
        logoHeaderAuDebut.style.display = "none";
        headerElt.classList.add('header_scroll');
    }
    let comportementAuDessus = () => {
        logoHeaderOnScroll.style.display = "none";
        logoHeaderAuDebut.style.display = "block";
        headerElt.classList.remove('header_scroll');
    }
    scrollTrigger(triggerPoint, comportementEnDessous, comportementAuDessus);
}
changerTailleLogoHeader();


// faire apparaître le numéro de téléphone dans le Header
function clickTelephone() {
    var element = document.querySelector('.cta_btn_phone');
    if (typeof (element) != 'undefined' && element != null) {
        let buttonPhone = document.querySelector('.cta_btn_phone');
        let phoneOffElt = document.querySelector('.cta_btn_phone_off');
        let phoneOnElt = document.querySelector('.cta_btn_phone_on');
        buttonPhone.addEventListener('click', () => {
            phoneOffElt.style.opacity = '0';
            phoneOnElt.style.display = 'inline-block';
        })
    }
}
clickTelephone();



// Menu Burger
function menuBurger() {
    let menuMobileButton = document.getElementById('menu_mobile_trigger');
    let menuElt = document.getElementById('menu');
    let menuMaskElt = document.getElementById('menu_mask');
    let burgerButton = document.getElementById('burger');
    let htmlElement = document.getElementsByTagName('html')[0];
    let contentHideElts = Array.from(document.getElementsByClassName('content_hide_menu'));
    var testAdminbar = document.getElementById("wpadminbar");
    menuMobileButton.addEventListener('click', () => {
        if (burgerButton.classList.contains('open')) { // si le menu est déjà ouvert
            burgerButton.classList.remove('open');
            menuElt.style.marginRight = "0";
            menuMaskElt.style.display = "none";
            menuElt.style.marginLeft = '0px';
            menuElt.style.opacity = '0';
            htmlElement.style.overflowY = 'auto';
            contentHideElts.forEach(element => {
                element.style.opacity = '1';
                element.style.pointerEvents = 'auto';
            })
        } else { // si le menu est fermé
            let headerElt = document.getElementById('header');
            let headerHeight = headerElt.offsetHeight;
            let viewPortHeight = window.innerHeight;
            menuElt.style.marginRight = "0"; 
            menuMaskElt.style.display = "block";
            menuMaskElt.style.top = '0';
            menuElt.style.marginLeft = `-${menuElt.offsetWidth}px`;
            menuElt.style.opacity = '1'; 
            burgerButton.classList.add('open');
            htmlElement.style.overflowY = 'hidden';
            contentHideElts.forEach(element => {
                element.style.opacity = '0.2';
                element.style.pointerEvents = 'none';
            })
            if (testAdminbar) { //si la barre admin est présente
                let wpAdminbar = document.querySelector('#wpadminbar');
                let wpAdminbarHeight = wpAdminbar.offsetHeight;
                let headerAdminHeight = headerHeight + wpAdminbarHeight;
                menuElt.style.top = `${headerAdminHeight.toString()}px`; 
                menuElt.style.height = `${viewPortHeight-headerAdminHeight}px`;
            } else { //si la barre admin n'est pas présente
                menuElt.style.top = `${headerHeight.toString()}px`; 
                menuElt.style.height = `${viewPortHeight-headerHeight}px`;
            }
        }
    })
}
window.addEventListener('load', () => {
    menuBurger();
})


// Colonne double large, dimmensionnement
function resizeColonneDoubleLarge() {
    let contentWidth = document.getElementsByClassName('content_width');
    contentWidth = contentWidth[0].offsetWidth;
    let colToResize = document.querySelectorAll('.col_right_wide_imgleft_wrapper, .col_left_wide_imgright_wrapper, .col_left_wide_imgleft_img_texte, .col_right_wide_imgright_img_texte');
    colToResize.forEach(col => {
        col.style.width = `${contentWidth * 0.5 + 16}` + `px`; 
    })
}
resizeColonneDoubleLarge();
window.addEventListener('resize', () => {
    resizeColonneDoubleLarge();
})


// ajout de classes CSS
function ajoutDeClasses() {
    // sideBar Actualité
    let nombreArticles = 3;
    let articleExtrait = document.querySelectorAll('#aside_actualites_wrapper .article_extrait');
    for (i = 0; i < nombreArticles; i++) {
        if (articleExtrait[i] != undefined) {
            articleExtrait[i].classList.add(`article_extrait_${i + 1}`);
        }
    }
}
ajoutDeClasses();


// met les padding et margin des premiers et derniers éléments de .entry-content à 0
function changeEntryContentCss() {
    let elementsEntryContent = document.querySelectorAll('.page_defaut .entry-content, .onepage .entry-content, .article_blog .entry-content');
    elementsEntryContent.forEach(element => {
        if (element.firstElementChild) {
            element.firstElementChild.style.paddingTop = '0';
            element.firstElementChild.style.marginTop = '0';
        }
        if (element.lastElementChild) {
            element.lastElementChild.style.paddingBottom = '0';
            element.lastElementChild.style.marginBottom = '0';
        }
    })
    let listedesOffres = document.querySelectorAll('.page_defaut .liste_des_offres .content_width');
    if (listedesOffres) {
        listedesOffres.forEach(liste => {
            liste.firstElementChild.style.marginTop = "0px";
        })
    }
}
changeEntryContentCss();


// Bloc Questions / Réponses
function blocQuestionReponse() {
    let questionReponseTitles = document.querySelectorAll('.question_reponse_title');
    questionReponseTitles.forEach(questionReponseTitle => {
        questionReponseTitle.addEventListener('click', (e) => {
            let plus = questionReponseTitle.querySelector('.question_reponse_title_icone_plus');
            let moins = questionReponseTitle.querySelector('.question_reponse_title_icone_moins');
            let reponse = questionReponseTitle.closest('.question_reponse_item');
            reponse = reponse.querySelector('.question_reponse_wysiwyg');
            if (questionReponseTitle.classList.contains('active')) { // est déjà actif
                questionReponseTitle.classList.remove('active');
                plus.style.display = "block";
                moins.style.display = "none";
                reponse.style.display = "none";
            } else { // est inactif
                questionReponseTitle.classList.add('active');
                plus.style.display = "none";
                moins.style.display = "block";
                reponse.style.display = "block";
            }
        })
    })
}
blocQuestionReponse();


// Label Nanosites
consommationCarbonne();
function consommationCarbonne() {
    window.addEventListener('load', () => {
        var consoCarbone = document.getElementById('wcb_g');
        var consoCarboneText = consoCarbone.innerText || consoCarbone.textContent;
        var valeurCarbone = consoCarboneText.split(" ")[0];
        var valeurCarboneNumber = parseFloat(valeurCarbone);
        if(isNaN(valeurCarboneNumber)){
            var nanositeCalculEnCours = document.getElementById('nanosite_calcul_encours');
            nanositeCalculEnCours.style.display = "block";
        }else{
            var nanositeCalculOk = document.getElementById('nanosite_calcul_ok');
            nanositeCalculOk.style.display = "block";
            var insertValeurCarbone = document.getElementById('nanosite_calcul_ok_value');
            var content = document.createTextNode(""+ valeurCarboneNumber + "");
            insertValeurCarbone.appendChild(content);
        }
    })
}

let nanositeLabel = document.getElementById('nanosite_label');
let nanositeLabelOn = document.getElementById('nanosite_label_on');
let nanositeLabelContainer = document.getElementById('nanosite_label_container');

nanositeLabel.addEventListener('mouseover', function() {
   nanositeLabelOn.style.display = "block";
   nanositeLabelContainer.style.display = "block";
});
nanositeLabel.addEventListener('mouseout', function() {
   nanositeLabelOn.style.display = "none";
   nanositeLabelContainer.style.display = "none";
});
nanositeLabel.addEventListener("touchstart", function(){
    nanositeLabelOn.style.display = "block";
    nanositeLabelContainer.style.display = "block";
});
nanositeLabel.addEventListener('touchmove', function() {
   nanositeLabelOn.style.display = "none";
   nanositeLabelContainer.style.display = "none";
});



//Afficher le poids des images au survol de la feuille
function poidsImageHover() {
    let poidsImages = document.querySelectorAll('.poids-image');
    poidsImages.forEach(poidsImage => {
        let poidsImageIcone = poidsImage.querySelector('.poids-image-icone');
        let poidsImageData = poidsImage.querySelector('.poids-image-data');
            poidsImage.addEventListener('mouseover', function() {
               poidsImageData.style.display = "inline-block";
            });
            poidsImage.addEventListener('mouseout', function() {
                poidsImageData.style.display = "none";
            });
            poidsImage.addEventListener('touchstart', function() {
                poidsImageData.style.display = "inline";
            });
            poidsImage.addEventListener('touchmove', function() {
                poidsImageData.style.display = "none";
            });
    });
}
poidsImageHover();


// remplace l'espace devant certains caractères par un insécable
function remplacerEspacesParInsecables() {
    let parags = document.querySelectorAll('#global_content p, #global_content li, #global_content h1, #global_content h2, #global_content h3, #global_content h4, #global_content h5, #global_content h6');
    parags.forEach(parag => {
        let string = parag.innerHTML;
        string = string.replace(/ !/g, '\u00a0!');
        string = string.replace(/ :/g, '\u00a0:');
        string = string.replace(/ \?/g, '\u00a0?');
        string = string.replace(/ ;/g, '\u00a0;');
        parag.innerHTML = string;
    });
}
remplacerEspacesParInsecables();


// charger les images sur les extraits d'articles (Aside et Blog)
function chargerLesImages() {
    var element = document.querySelector('#charger_les_images');
    if (typeof (element) != 'undefined' && element != null) {
        let chargerLesImages = document.getElementById('charger_les_images');
        let chargerLesImagesBouton = document.getElementById('charger_les_images_switch_label');
        let articlesWrapperBlog = document.getElementById('articles_wrapper_blog');
        let articlesWrapperAside = document.getElementById('aside_actualites_wrapper');
        if(typeof (articlesWrapperBlog) != 'undefined' && articlesWrapperBlog != null){ //Blog
            var articlesExtraits = articlesWrapperBlog.querySelectorAll('.article_extrait');
        }
        if(typeof (articlesWrapperAside) != 'undefined' && articlesWrapperAside != null){ //Aside
            var articlesExtraits = articlesWrapperAside.querySelectorAll('.article_extrait');
        }
        chargerLesImagesBouton.addEventListener('click', (event) => {
            articlesExtraits.forEach(articleExtrait => {
                let articleExtraitThumbnail = articleExtrait.querySelector('.article_extrait_thumbnail');
                let articleExtraitThumbnailImg = articleExtraitThumbnail.querySelector('img'); // l'élément que l'on veut charger
                articleExtraitThumbnail.style.display = "block"; // on affiche le bloc qui contient l'image
                let articleExtraitThumbnailImgData = articleExtraitThumbnailImg.getAttribute("data-src"); // on récupère l'attribut data-src
                articleExtraitThumbnailImg.setAttribute("src", articleExtraitThumbnailImgData); // on ajoute l'attribut data-src à l'attribut src
                
                // une fois que les images sont chargées
                chargerLesImagesBouton.style.pointerEvents = "none";
                    setTimeout(function() {
                        chargerLesImagesBouton.style.opacity = '0.3';
                        chargerLesImages.style.opacity = '0.3';
                    }, 500);
            });
        })
        
    }

}
chargerLesImages();


// menu principal responsive
function menuPrincipalResponsiveScroll() {
    let triggerPoint = 400;
    let headerElt = document.getElementById('header');
    
    let menuHeader = document.getElementById('menu_header');
    let menuHeaderWidth = menuHeader.offsetWidth;
    let menuHeaderWrapper = document.getElementById('menu_header_wrapper');
    let contentNavHeader = document.getElementById('content_nav_header');
        contentNavHeader = contentNavHeader.offsetWidth;
    
    let logoHeaderImg = document.getElementById('logo_header_img');
        logoHeaderImg = logoHeaderImg.offsetWidth;
    let logoHeaderImgScroll = document.getElementById('logo_header_img_scroll');
        logoHeaderImgScroll = logoHeaderImgScroll.offsetWidth;

    let headerPhone = document.getElementById('header_phone');
        if (typeof (headerPhone) != 'undefined' && headerPhone != null) {
           headerPhone = headerPhone.offsetWidth;
        } else {
           headerPhone = 0; 
        }
    
    let headerContact = document.getElementById('header_contact');
        if (typeof (headerContact) != 'undefined' && headerContact != null) {
           headerContact = headerContact.offsetWidth;
        } else {
           headerContact = 0; 
        }

    let elementsHeader;
    let placeDispoHeader;

    // comportement au chargement ou au resize
    if ( headerElt.classList.contains('header_scroll')  ){
        elementsHeader = logoHeaderImgScroll + headerPhone + headerContact + 60;
        placeDispoHeader = contentNavHeader - elementsHeader;
        if (placeDispoHeader > menuHeaderWidth){
            menuHeader.style.position = 'relative';
            menuHeader.style.top = '50%';
        } 
        if (placeDispoHeader < menuHeaderWidth){
            menuHeader.style.position = 'absolute';
            menuHeader.style.top = '-9999px';
        }
    } else{
        elementsHeader = logoHeaderImg + headerPhone + headerContact + 60;
        placeDispoHeader = contentNavHeader - elementsHeader;
        if (placeDispoHeader > menuHeaderWidth){
            menuHeader.style.position = 'relative';
            menuHeader.style.top = '50%';
        } 
        if (placeDispoHeader < menuHeaderWidth){
            menuHeader.style.position = 'absolute';
            menuHeader.style.top = '-9999px';
        }
    }
    // comportement quand on scrolle sous les 400px
    let comportementEnDessous = () => {
        elementsHeader = logoHeaderImgScroll + headerPhone + headerContact + 60;
        placeDispoHeader = contentNavHeader - elementsHeader;
        if (placeDispoHeader > menuHeaderWidth){
            menuHeader.style.position = 'relative';
            menuHeader.style.top = '50%';
        } 
        if (placeDispoHeader < menuHeaderWidth){
            menuHeader.style.position = 'absolute';
            menuHeader.style.top = '-9999px';
        }      
    }
    // comportement quand on scrolle au dessus des 400px
    let comportementAuDessus = () => {
        elementsHeader = logoHeaderImg + headerPhone + headerContact + 60;
        placeDispoHeader = contentNavHeader - elementsHeader;
        if (placeDispoHeader > menuHeaderWidth){
            menuHeader.style.position = 'relative';
            menuHeader.style.top = '50%';
        } 
        if (placeDispoHeader < menuHeaderWidth){
            menuHeader.style.position = 'absolute';
            menuHeader.style.top = '-9999px';
        }
    }
    scrollTrigger(triggerPoint, comportementEnDessous, comportementAuDessus);
}
window.addEventListener('load', () => {
        menuPrincipalResponsiveScroll();
    })
window.addEventListener('resize', () => {
        menuPrincipalResponsiveScroll();
    })
    menuPrincipalResponsiveScroll();
 
