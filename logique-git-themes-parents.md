# Logique Git / Thèmes parent

La préprod depuis laquelle dupliquer les sites se trouve ici : [https://childtheme.nanosite.tech/](https://childtheme.nanosite.tech/)&#x20;

Le thème parent se trouve ici  : [https://github.com/nicolaseverest/nanosite-theme-parent](https://github.com/nicolaseverest/nanosite-theme-parent)

Le thème enfant "par défaut" se trouve ici : [https://github.com/nicolaseverest/nanosite-theme-enfant](https://github.com/nicolaseverest/nanosite-theme-enfant)

Il est recommandé de créer un repo consacré au thème enfant du site qu'on développe. Par exemple, Sojade a son propre thème enfant : [https://github.com/AgenceEverest/sojade-child](https://github.com/AgenceEverest/sojade-child)





Pour avoir les accès aux Repos, demander à nicolas@scenarii.net

git remote set-url origin -> permet de changer l’url du remote enfant (par exemple)

**Pour cloner un thème enfant :**

On va d’abord aller sur Github, et créer un repo qui va devenir le nouveau dépôt pour notre thème enfant. Une fois notre dépôt créé, on récupère un lien git qui s’appelle quelque chose comme : git@github/nicolaseverest/mondepot.git

On va donc créer un nouveau site avec un thème enfant. Le mieux est de dupliquer le site à partir d’ici : https://childtheme.nanosite.tech/ Sur ce site, deux dossiers : nanosite-proefficace, relié à : git@github/nicolaseverest/nanosite-theme-parent.git nanosite-proefficace-child, relié à : git@github/nicolaseverest/nanosite-theme-enfant.git

L’idée est de changer l’adresse à laquelle est lié le dossier nanosite-proefficace-child.

**Attention à bien réécrire les lignes de commande à la main pour éviter les ratages lors de copier/coller !**

On installe le site en local avec MAMP, puis on se rend en ligne de commande dans le dossier nanosite-proefficace-child (cd.. pour reculer cd nomdudossier pour avancer, ls pour regarder autour de soi ce qu’il y a comme fichiers, tabulation pour faire de l’autocomplétion).

Une fois dans le dossier, on check la remote en faisant :&#x20;

* **git remote -v** : cela affiche à quelle remote est connectée le dossier. Normalement, il est relié à github.com/nicolaseverest/nanosite-theme-enfant&#x20;
* On va changer cette remote à l’aide de la commande git suivante : **git remote set-url origin git@github/nicolaseverest/mondepot.git**&#x20;
* Le dossier est maintenant lié à mon nouveau dépôt github. Il reste maintenant à créer un commit initial, pour cela je tape les commandes suivantes :&#x20;
* **git add -A** : permet d’ajouter tous les fichiers à mon commit&#x20;
* **git commit -m ‘initial commit’** : je crée un commit et je lui donne un nom&#x20;
* **git push --set-upstream origin master** : je pousse mon commit sur le nouveau repo. Le drapeau set-upstream permet de définir origin et master comme étant les branches de référence de mon dossier local.



Si on souhaite intégrer des mises à jours de la branche master sur une branche de travail :&#x20;

* On checkout sur notre branche de travail en cours
* On merge master avec notre branche de travail en cours (**git merge origin/master**)
* On push le nouveau commit créé par cette manip
