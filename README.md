
# **Environnement de Développement PrestaShop**

Ce dépôt fournit une configuration complète pour un environnement de développement PrestaShop utilisant Docker. La configuration inclut plusieurs composants, notamment MySQL, PrestaShop, Loki, Promtail et Grafana pour l'analyse des journaux.
## Demo

[![Watch the video](https://img.youtube.com/vi/-I7AREvHALY/default.jpg)](https://youtu.be/-I7AREvHALY)

À la fin, lorsque tout est en fonctionnement, vous devriez obtenir ceci :
![alt text](19222828.png)

## Prérequis

- Assurez-vous d'avoir Docker et Docker Compose installés sur votre machine.  
- Téléchargez une version de PrestaShop et mettez à jour le fichier `Dockerfile.devel`.  
- Créez les dossiers nécessaires pour Grafana, Loki, etc.  

## Instructions d'installation

### Construction des conteneurs de base et de développement  

1. Clonez ce dépôt.  
2. Personnalisez le fichier `Dockerfile.devel` pour installer une version différente de PrestaShop ou d'autres dépendances si nécessaire.  
3. Construisez les images Docker en utilisant le script `docker.sh` fourni :


   ```sh
   ./docker.sh build
   ```

### Lancement de l'environnement de développement  

1. Démarrez l'environnement de développement :  

   ```sh
   ./docker.sh up
   ```

### Accès SSH au conteneur de base  

Le conteneur de base est configuré avec un serveur OpenSSH et permet un accès SSH en utilisant l'authentification par clé publique. Assurez-vous que votre clé publique est ajoutée au conteneur.  

## Détails de la configuration  

### Dockerfile.base  

Ce fichier Docker configure le conteneur de base avec toutes les dépendances et outils nécessaires, à l'exception de PrestaShop. Il inclut les configurations pour PHP, SSH et d'autres outils essentiels.  

### Dockerfile.devel  

Ce fichier Docker configure le conteneur de développement, ajoutant PrestaShop et les autres configurations nécessaires pour un environnement de développement.  

### docker-compose.yml  

Ce fichier définit les services et configurations pour Docker Compose, y compris le service PrestaShop, la base de données MySQL, Loki, Promtail et Grafana pour l'analyse des journaux.  

## Analyse des journaux avec Grafana et Loki  

Cette configuration inclut Grafana pour la visualisation des journaux et Loki comme système d'agrégation de journaux. Promtail est utilisé pour collecter les journaux à partir de différentes sources.  

### Services  

- **MySQL** : Service de base de données pour PrestaShop.  
- **PrestaShop** : Le service principal de l'application.  
- **Loki** : Système d'agrégation des journaux.  
- **Promtail** : Agent qui envoie le contenu des journaux à Loki.  
- **Grafana** : Plateforme de surveillance et d'observabilité.  

### Configuration de Grafana  

1. Grafana est accessible à l'adresse `http://localhost:3000`.  
2. L'authentification par défaut est désactivée et l'accès anonyme est activé avec un rôle Admin. Vous pouvez personnaliser ce paramètre dans le fichier `docker-compose.yml` si nécessaire.  
3. Les journaux d'Apache et de PrestaShop sont collectés et affichés dans les tableaux de bord de Grafana.  

### Fichiers de configuration  

- **loki-config.yaml** : Configuration pour Loki.  
- **promtail-config.yml** : Configuration pour Promtail, spécifiant quels journaux collecter et envoyer à Loki.  

### Démarrage de la pile d'analyse des journaux  

1. Lancez la pile à l'aide de Docker Compose :  

   ```sh
   docker-compose up -d
   ```  

2. Accédez à Grafana à l'adresse `http://localhost:3000` pour commencer à visualiser vos journaux.  

### Structure des répertoires  

- `config/` : Contient les fichiers de configuration pour MySQL et d'autres services.  
- `init-scripts/` : Scripts d'initialisation pour configurer l'environnement.  
- `logs/` : Répertoire pour stocker les journaux d'Apache et de PrestaShop.  
- `modules/` : Modules personnalisés de PrestaShop pour le développement.  
- `grafana/` : Stockage persistant pour les configurations et tableaux de bord de Grafana.  
- `provisioning/` : Configuration de provisionnement pour les sources de données et tableaux de bord Grafana.  

### Commandes d'exemple  

Pour construire et exécuter les conteneurs Docker :  

```sh
./docker.sh build
./docker.sh up
```

## Notes  

- Assurez-vous que votre clé SSH publique est correctement ajoutée à la configuration pour un accès SSH.  
- Ajustez les variables d'environnement si nécessaire dans le fichier `docker-compose.yml`.  

## Liens utiles  

- [Débogage à distance PHP avec VSCode](https://ramyhakam.medium.com/php-remote-debugging-with-vscode-a-comprehensive-guide-f20e67000b7d)  
- [Commandes console PrestaShop](https://github.com/nenes25/prestashop_console/blob/1.7/COMMANDS.md)  
- [Bootstrap pour module](https://github.com/friends-of-presta/demo-cqrs-hooks-usage-module)  
- [Logio](http://logio.org/)  
- [Création de commandes console dans PrestaShop 1.7](https://webkul.com/blog/create-your-own-console-command-in-prestashop-1-7/)  
