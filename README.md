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

#### Installation des packages nécessaires
##### Python
```{.copyWrapper}
sudo yum install python34
```

##### Set up YUM Repositories
###### STEP 1 : we need to install some software that allows us to use signed packages:
```{.copyWrapper}
sudo yum install pygpgme yum-utils wget
```

###### STEP 2 : we need to configure repository configurations for Tyk Dashboard
```{.copyWrapper}
sudo vi /etc/yum.repos.d/tyk_tyk-dashboard.repo
```

###### STEP 3 : Copier la configuration suivante dans le fichier
```{.copyWrapper}
[tyk_tyk-dashboard]
name=tyk_tyk-dashboard
baseurl=https://packagecloud.io/tyk/tyk-dashboard/el/7/$basearch
repo_gpgcheck=1
gpgcheck=1
enabled=1
gpgkey=http://keyserver.tyk.io/tyk.io.rpm.signing.key
       https://packagecloud.io/tyk/tyk-dashboard/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
```

> **Rappels Vim** 
>
> * Pour passer en mode Edition, appuyer sur i. 
> * Pour passer en mode commande, appuyer sur échappement. 
> * Pour sauvegarder et quitter le fichier, mode commande : ***wq!*** 

###### STEP 4 : we need to configure repository configurations for MongoDB
```{.copyWrapper}
sudo vi /etc/yum.repos.d/mongodb-org-3.0.repo
```

###### STEP 5 : Copier la configuration suivante dans le fichier
```{.copyWrapper}
[mongodb-org-3.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.0/x86_64/
gpgcheck=0
enabled=1
```

###### FINAL STEP : Raffraichir le cache local
```{.copyWrapper}
sudo yum -q makecache -y --disablerepo='*' --enablerepo='tyk_tyk-dashboard'
```




### Installer le serveur Gateway




