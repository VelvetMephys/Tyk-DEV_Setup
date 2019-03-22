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
### Installer le serveur Dashboard
#### Configurer le serveur
##### Ouverture du port 3000 - Nécessaire à l'accès au serveur Web
Attention, ici nous ajoutons l'ouverture à la Zone Public ( représente l’ensemble des réseaux publics ou non sécurisés. On ne fait pas confiance aux autres ordinateurs ou serveurs mais, on peut traiter les connexions entrantes au cas par cas à l’aide de règles. )

```{.copyWrapper}
firewall-cmd --zone=public --add-port=3000/tcp 
```

##### Installation des packages nécessaires
```{.copyWrapper}
sudo yum install python34
```

#### Installer le serveur Gateway




