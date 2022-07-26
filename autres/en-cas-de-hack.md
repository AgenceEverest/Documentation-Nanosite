# En cas de hack

En cas de hack, il faut d'abord trouver sur le FTP la date de l’injection de fichier qui a causé le hack. Il faut ensuite retourner à un backup antérieur à ce hack (voir sur les différents hosters) et corriger les failles :&#x20;

* Mise à jour des extensions&#x20;
* Changement de tous les mots de passe : sur l’hébergement, FTP, et la BDD

Avec Secupress : on peut faire un scan des fichiers malicieux : on réinstalle le backup puis on fait tourner cette fonction de Secupress.

Pour les non-Wordpress : il y a un Waf dessus (qui s'appelle stackpath, voir dans Safeincloud les accès à Stackpath).

Backup de Planethoster : dans le Cpanel : "R1 Soft Restore Backup" permet de restaurer une BDD à une date fixe. **Attention : ça télécharge tous les fichiers de tous les sites. Donc il faut rentrer dans le compte d’hébergement et faire une archive uniquement du site concerné.**
