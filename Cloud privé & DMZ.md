Installation de nextcloud :

# Documentation Only Office Nextcloud
# Only Office
```bash
nextcloud-onlyoffice	
172.16.101.41
root
u6)W/8rR]//=Yu5+j4"?U*TDr7[f6{%q
```
acces admin a nextcloud:
```
admin
ygdugeduig$^pmùç)
```
https://nextcloud.soluris.fr/login?direct=1


### Documentation utilisée

Site web du projet: https://github.com/ONLYOFFICE
Doc : https://github.com/ONLYOFFICE/docker-onlyoffice-nextcloud
Docker : https://docs.docker.com/engine/install/
https://helpcenter.onlyoffice.com/fr/integration/nextcloud.aspx

### Prérequis
- Docker (version 20.10 ou ultérieure)
- Docker Compose (version 2.0 ou ultérieure)

### Installation de docker/docker compose
```bash
# docker 
# Add Docker's official GPG key:
apt update
apt install ca-certificates curl
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
apt update

# Installation du paquet docker
apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Vérification du status de docker 
systemctl status docker
# Si docker n'est pas actif 
systemctl start docker
```
### Installation de git
```bash
apt install git
```

### Installation de onlyoffice
```bash
git clone https://github.com/ONLYOFFICE/docker-onlyoffice-nextcloud
cd docker-onlyoffice-nextcloud

nano docker-compose.yml

```

```bash
version: '3'

services:

  nextcloud:
    image: nextcloud:latest
    container_name: nextcloud
    restart: always
    ports:
      - "80:80"
    depends_on:
      - db
    environment:
      - MYSQL_HOST=db
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_PASSWORD=MotDePasseIci
      - NEXTCLOUD_ADMIN_USER=admin
      - NEXTCLOUD_ADMIN_PASSWORD=AdminMotDePasse
    volumes:
      - nextcloud_data:/var/www/html

  db:
    image: mariadb:10.11
    container_name: nextcloud_db
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=RootMotDePasseIci
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_PASSWORD=MotDePasseIci
    volumes:
      - db_data:/var/lib/mysql

volumes:
  nextcloud_data:
  db_data:

```

### Installation de Mariadb
```bash
apt install mariadb-server -y


systemctl start mariadb
systemctl enable mariadb


systemctl status mariadb
```

### Créer la base de données
```bash

mysql -u root -p

CREATE DATABASE nextcloud CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
CREATE USER 'nextcloud'@'%' IDENTIFIED BY 'MotDePasseIci';
GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextcloud'@'%';
FLUSH PRIVILEGES;
SHOW DATABASES;
SELECT User, Host FROM mysql.user;

EXIT;
```

### Configurer Mariadb
```bash
nano /etc/mysql/mariadb.conf.d/50-server.cnf

#ctrl + f
127.0.0.1 #pour trouver la ligne 
bind-address = 127.0.0.1
#et remplacer par:
bind-address = 0.0.0.0
```
```bash
systemctl restart mariadb
```

### Configurer l'OIDC

Se rendre dans nextcloud avec un compte administrateur aller dans :
**paramètres d'administration** -> **openid connect** -> entrer sa configuration (keycloak) dans notre cas

![](https://notes.soluris.fr/uploads/9b19b9ad-c42b-4983-b489-613c64e69f87.png)


### Configurer ONLYOFFICE 

**Paramètres -> Administration -> ONLYOFFICE**
![](https://notes.soluris.fr/uploads/55248d5c-142e-47ef-a07f-df687bade313.png)

puis un nouveau menu apparait en-dessous : 

![](https://notes.soluris.fr/uploads/d53b977c-953f-4551-8224-37e712dab844.png)


