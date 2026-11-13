# Configuration du Cluster Web et Load Balancing (Nginx)

## 1. Architecture
Le cluster web est composé de deux serveurs backend et d'un serveur frontal :
- **VM1 (192.168.20.50)** : Serveur Nginx (port 80) + Serveur Apache (port 8080).
- **VM2 (192.168.20.51)** : Serveur Apache (port 80).

Nginx agit comme un reverse proxy et répartit la charge (Round-Robin) entre les deux serveurs Apache.

## 2. Configuration de Nginx
Fichier `/etc/nginx/sites-available/default` :
```nginx
upstream backend_web {
    server 192.168.20.50:8080;
    server 192.168.20.51:80;
}

server {
    listen 80;
    server_name monsite.local;

    location / {
        proxy_pass http://backend_web;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
