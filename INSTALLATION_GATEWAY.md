# Installer le serveur Gateway
## Ouverture des ports nécessaires au service
### Port 8080 - Nécessaire au transport des API
### Port 6379 - Nécessaire pour l'interface Redis
Attention, ici nous ajoutons l'ouverture à la Zone Public ( représente l’ensemble des réseaux publics ou non sécurisés. On ne fait pas confiance aux autres ordinateurs ou serveurs mais, on peut traiter les connexions entrantes au cas par cas à l’aide de règles. )

```{.copyWrapper}
sudo firewall-cmd --zone=public --add-port=8080/tcp
sudo firewall-cmd --zone=public --add-port=6379/tcp
```

### Set up YUM Repositories
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

#### STEP 6 : Installation de Redis et du Gateway
```{.copyWrapper}
sudo yum install -y redis tyk-gateway
```


#### STEP 7 : Configuration de Redis
##### Ouvrir le flux entrant à partir du Dashboard
```{.copyWrapper}
sudo vi /etc/redis.conf
```

Commenter la partie : bind tel que sur la capture d'écran ci-dessous

##### Vérifier/modifier les droits des répertoires Redis
sudo chmod 755 /var/lib/redis
sudo chmod 644 /var/lib/redis/dump.rdb
