
# **AdGuard Home Configuration sous Docker**

Bienvenue dans le projet **AdGuard Home**. Ce guide détaille l’installation et la configuration d’AdGuard Home dans un conteneur Docker, avec l’intégration à un routeur pour filtrer les publicités et trackers à l’échelle du réseau.

---

## **Table des Matières**

- [Introduction](#introduction)
- [Prérequis](#prérequis)
- [Installation](#installation)
- [Configuration du Routeur](#configuration-du-routeur)
- [Ajout de la Liste OISD](#ajout-de-la-liste-oisd)
- [Vérification](#vérification)
- [Auteur](#auteur)

---

## **Introduction**

AdGuard Home est un outil puissant permettant de bloquer les publicités et les trackers à l’échelle d’un réseau. Ce projet explique comment le configurer rapidement à l’aide de Docker et l’intégrer au routeur pour protéger tous les appareils connectés.

---

## **Prérequis**

Avant de commencer, assurez-vous d’avoir :
- Une machine ou VM avec **Docker** et **Docker Compose** installés.
- Une adresse IP statique assignée à la machine hôte.
- Un accès à l’interface de configuration de votre routeur.

---

## **Installation**

1. **Lancer le conteneur Docker**
   - Placez-vous dans le répertoire du projet contenant le fichier `docker-compose.yml` et exécutez :
     ```bash
     docker-compose up -d
     ```
   - Une fois lancé, l’interface web d’AdGuard Home est accessible à l’adresse suivante :  
     **http://<IP_DE_LA_VM>:3000**

---

## **Configuration du Routeur**

1. **Trouver l’adresse IP de la machine hôte** :
   - Exécutez la commande suivante :
     ```bash
     ip a
     ```
   - Notez l’adresse IP (ex. **192.168.1.177**).

2. **Configurer le serveur DNS du routeur** :
   - Accédez à l’interface web du routeur (ex. **http://192.168.1.1**).
   - Renseignez :
     - **DNS primaire** : `192.168.1.177` (IP de la machine hôte).
     - **DNS secondaire** : `1.1.1.1` (Cloudflare) ou `8.8.8.8` (Google DNS).
   - Appliquez les modifications et redémarrez les appareils connectés pour qu’ils prennent en compte le nouveau DNS.

---

## **Ajout de la Liste OISD**

Pour améliorer le blocage des publicités et trackers, ajoutez la liste **OISD** à AdGuard Home :

1. Accédez à **Settings > Filters > DNS Blocklists** dans l’interface web d’AdGuard Home.
2. Ajoutez la liste :
   ```
   https://big.oisd.nl/
   ```
3. Cliquez sur **Sauvegarder & Appliquer**.
4. Attendez quelques minutes pour l’activation complète des règles.

---

## **Vérification**

1. **Tester si AdGuard Home est actif** :
   - Exécutez :
     ```cmd
     nslookup google.com
     ```
     - **Résultat attendu** : Le serveur DNS doit être **192.168.1.177**.

2. **Vérifier les requêtes DNS** :
   - Dans l’interface d’AdGuard Home, allez dans **Query Log** et vérifiez que les requêtes apparaissent.

3. **Tester le blocage des publicités** :

