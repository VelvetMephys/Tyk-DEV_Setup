# Documentation d'installation d'un Middleware Tyk sur 2 machines

## Description de l'environnement
- Tyk\-Dashboard
- Tyk\-Gateway
- Tyk\-Pump
- Redis
- MongoDb

## Description de l'architecture :
- Dashboard : Dashboard + MongoDB + Pump
- Gateway : Gateway + Redis

## Documentation Officielle :
- https://tyk.io/docs/get-started/with-tyk-on-premise/installation/redhat-rhel-centos/

## Installation et configuration des serveurs
1. Installer le serveur Dashboard
  1. Configurer le serveur
    1. Ouverture des ports
      * Ouverture du port 3000
      ```firewall-cmd --zone=public --add-port=2888/tcp ```
    
    2. Installation des repository Tyk pour installation
    


2. Installer le serveur Gateway




