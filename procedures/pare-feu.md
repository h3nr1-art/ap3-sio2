# Configuration du Pare-feu (iptables)

## 1. Objectif
Mettre en place une politique de sécurité stricte sur le routeur Debian pour protéger le réseau interne (LAN) et la zone démilitarisée (DMZ).

## 2. Script `/etc/firewall.sh`
Le script est appliqué automatiquement au démarrage de l'interface WAN via la directive `post-up` dans `/etc/network/interfaces`.

### Principes de sécurité appliqués :
- **Politique par défaut** : `DROP` sur les chaînes `INPUT` et `FORWARD` (tout ce qui n'est pas explicitement autorisé est bloqué).
- **Connexions établies** : Autorisation des paquets `ESTABLISHED,RELATED` pour permettre le retour du trafic (essentiel pour ne pas couper le SSH).
- **Services exposés** :
  - Autorisation du port `22` (SSH) en entrée pour l'administration.
  - Autorisation du port `80` (HTTP) en entrée pour le serveur web.
- **Routage (NAT)** : Activation du `MASQUERADE` sur l'interface WAN (`ens33`) pour permettre aux machines du LAN de sortir vers Internet.

## 3. Vérification de l'application
La commande `iptables -L INPUT -n --line-numbers` permet de vérifier l'ordre des règles. La règle d'acceptation du SSH doit impérativement se trouver **avant** le `DROP` par défaut.
