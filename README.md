Installation et Configuration d'AdGuard Home sous Docker

Introduction

Ce projet vise à installer et configurer AdGuard Home dans un conteneur Docker, ainsi qu'à l'intégrer à un routeur pour filtrer les publicités et trackers sur tout le réseau.

1. Installation d'AdGuard Home sous Docker

1.1 Prérequis

Docker et Docker Compose installés sur une machine (VM ou serveur).

Une adresse IP statique configurée pour la machine hôte.

1.2 Lancement du conteneur

Démarrer AdGuard Home avec la commande :

docker-compose up -d

AdGuard Home sera accessible à l'adresse http://<IP_DE_TA_VM>:3000

2. Configuration du Routeur

2.1 Trouver l'IP de la machine hôte

Exécuter :

ip a

Exemple d'IP : 192.168.10.177

2.2 Configurer le serveur DNS sur le routeur

Accéder à l'interface web du routeur (http://192.168.10.1) et :

Aller dans Paramètres DHCP.

Renseigner 192.168.10.177 comme DNS primaire.

Ajouter un DNS secondaire (ex: 1.1.1.1 ou 8.8.8.8).

Sauvegarder et appliquer les modifications.

Redémarrer les appareils connectés au routeur pour qu'ils prennent en compte le nouveau DNS.

3. Accès à AdGuard Home

Ouvrir un navigateur et aller sur http://192.168.10.177:3000.

Suivre l'assistant de configuration :

Définir un mot de passe administrateur.

Configurer les DNS amont (ex: 1.1.1.1).

Activer les blocklists par défaut.

4. Ajout de la Liste OISD

4.1 Accéder aux filtres DNS

Aller dans Settings > Filters > DNS Blocklists.

Ajouter la liste OISD :

https://big.oisd.nl/

Cliquer sur Sauvegarder & Appliquer.

Attendre quelques minutes pour l'activation.

5. Vérification

5.1 Tester si AdGuard Home est bien utilisé

Exécuter sur un PC :

nslookup google.com

Résultat attendu : L'IP du serveur DNS doit être 192.168.10.177.

Aller dans AdGuard Home > Query Log et vérifier que les requêtes DNS apparaissent.

5.2 Tester le blocage des publicités

Aller sur un site de test :

🔗 ads-blocker.com/testing

🔗 d3ward.github.io/adblock.html

Vérifier que les publicités sont bien bloquées.

🎯 Conclusion

AdGuard Home est maintenant installé et configuré sous Docker.

Le routeur est paramétré pour utiliser AdGuard Home comme DNS principal.

La liste OISD est appliquée pour un blocage efficace des publicités et trackers.

🚀 Ton réseau est maintenant protégé contre les publicités !

