# Installer le serveur Gateway
## Ouverture des ports nécessaires au service
#### _Port 8080 - Transport des API_
#### _Port 6379 - Interface Redis_
Attention, ici nous ajoutons l'ouverture à la Zone Public ( représente l’ensemble des réseaux publics ou non sécurisés. On ne fait pas confiance aux autres ordinateurs ou serveurs mais, on peut traiter les connexions entrantes au cas par cas à l’aide de règles. )

```{.copyWrapper}
sudo firewall-cmd --zone=public --add-port=8080/tcp
sudo firewall-cmd --zone=public --add-port=6379/tcp
```
## Besoin de gérer les DNS localement en éditant le fichier /etc/hosts
Afin de pouvoir respecter les bonnes pratiques, il vaut mieux utiliser les DNS que les adresses IP. 
Pour ce faire, sur l'environnement de développement , nous allons donc mapper les deux serveurs localement, avec une DNS dans le fichier /etc/hosts

```{.copyWrapper}
sudo vi /etc/hosts
```
Ajouter les lignes mappant IPs et DNS, soit ici : 
```{.copyWrapper}
51.75.196.202   tyk-dashboard
51.77.108.198   tyk-gateway
```

Voici un exemple du fichier hosts configuré pour l'exemple.
![Hosts file](2019-03-22_13h45_37.png)


## Set up YUM Repositories
#### STEP 1 : we need to install some software that allows us to use signed packages:
```{.copyWrapper}
sudo yum install pygpgme yum-utils wget
```

#### STEP 2 : we need to configure repository configurations for Tyk Dashboard
```{.copyWrapper}
sudo vi /etc/yum.repos.d/tyk_tyk-gateway.repo
```

#### STEP 3 : Copier la configuration suivante dans le fichier 
```{.copyWrapper}
[tyk_tyk-gateway]
name=tyk_tyk-gateway
baseurl=https://packagecloud.io/tyk/tyk-gateway/el/7/$basearch
repo_gpgcheck=1
gpgcheck=1
enabled=1
gpgkey=http://keyserver.tyk.io/tyk.io.rpm.signing.key
       https://packagecloud.io/tyk/tyk-gateway/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
```

#### STEP 4 : Installer EPEL pour enrichir les repositories 
```{.copyWrapper}
sudo yum install -y epel-release
sudo yum update
```

#### STEP 5 : Mettre le cache a jour
```{.copyWrapper}
sudo yum -q makecache -y --disablerepo='*' --enablerepo='tyk_tyk-gateway' --enablerepo=epel
```

## Installation des différents éléments
#### STEP 1 : Installation de Redis et du Gateway
```{.copyWrapper}
sudo yum install -y redis tyk-gateway
```

#### STEP 2 : Configuration de Redis
##### Ouvrir le flux entrant à partir du Dashboard
```{.copyWrapper}
sudo vi /etc/redis.conf
```

Commenter la partie : bind tel que sur la capture d'écran ci-dessous

##### Vérifier/modifier les droits des répertoires Redis
```{.copyWrapper}
sudo chmod 755 /var/lib/redis
sudo chmod 644 /var/lib/redis/dump.rdb
```
