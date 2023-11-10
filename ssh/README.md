# Quelques raccourcis SSH...

Pour pouvoir pull/push, il faut installer une clé SSH sur sa machine et sur le repo de l'agence.&#x20;

Il est possible de naviguer sur le serveur contenant certaines préprods avec des commandes. Pour celui contenant Sojade, Camping Portland, Childtheme, il existe des commandes pour aller directement dans les dossiers concernés :&#x20;

sp : sojade parent

sc : sojade child

ctp : childtheme parent

ctc childtheme child

cpp : camping portland parent

cpc : camping portland child

rajouter "g" à ces raccourcis pour git pull sur ces dossiers

gpall : git pull sur les tous les parents et enfants ci-dessus

gppall : git pull sur tous les thèmes parents



ssh-keygen -t ecdsa -b 521 -C [your\_email@example.com](mailto:your\_email@example.com)  => la commande pour relier git à un serveur de façon sécurisé



