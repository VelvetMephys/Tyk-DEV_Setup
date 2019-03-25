# Procédure d'installation de Tyk sur 2 machines

## Description de l'environnement
- Tyk\-Dashboard
- Tyk\-Gateway
- Tyk\-Pump
- Redis
- MongoDb

## Description de l'architecture :
- [Serveur_Dashboard] : Dashboard + MongoDB + Pump
- [Serveur_Gateway] : Gateway + Redis

## Adresse IP et DNS :
Environnement | IP | DNS
----------| -----------|----------------
Dashboard | 51.75.196.202 | tyk-dashboard 
Gateway | 51.77.108.198  | tyk-gateway 

## Documentation Officielle :
- https://tyk.io/docs/get-started/with-tyk-on-premise/installation/redhat-rhel-centos/

[serveur_Dashboard]: https://github.com/VelvetMephys/documentation/blob/master/INSTALLATION.md "guide d'installation du serveur Dashboard"
[serveur_Gateway]: https://github.com/VelvetMephys/documentation/blob/master/INSTALLATION.md "Guide d'installation du serveur Gateway"
