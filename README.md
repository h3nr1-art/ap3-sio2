# Projet DMH - Refonte du Système d'Information

## Présentation
Ce dépôt contient la documentation technique et les procédures de configuration réalisées dans le cadre de l'Atelier de Professionnalisation (AP3) pour l'entreprise DMH.

## Rôles de l'équipe
- **Admin Réseau** : VLANs, routage Linux, firewall.
- **Admin Windows** : AD, GPO, DFS.
- **Admin NAS/Cloud** : Cloud privé sur NAS, sauvegardes.
- **Admin Web (Mon rôle)** : Serveurs Apache, cluster web et load balancer Nginx.

## Avancement (Admin Web)
- [x] Configuration réseau de la VM Debian (WAN, LAN, DMZ, Host-Only).
- [x] Mise en place du pare-feu (iptables).
- [x] Installation et configuration d'Apache.
- [ ] Déploiement du 2ème backend.
- [ ] Configuration du Load Balancer Nginx.

## Structure du dépôt
- `/procedures` : Documentation pas à pas des installations.
- `/configs` : Fichiers de configuration (Apache, iptables, etc.).
- `/schemas` : Schémas réseau et logiques.
