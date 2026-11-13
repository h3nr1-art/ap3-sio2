# Configuration Réseau de la VM Debian (Routeur/Pare-feu)

## 1. Architecture des interfaces
La VM Debian possède 4 interfaces réseau, configurées dans `/etc/network/interfaces` :

| Interface | Rôle | Type de réseau | Adresse IP |
|---|---|---|---|
| `ens33` | WAN (Internet) | NAT (VMnet8) | DHCP (ex: 172.16.x.x) |
| `ens37` | LAN | LAN Segment | 192.168.10.254/24 |
| `ens38` | DMZ | LAN Segment | 192.168.100.254/24 |
| `ens39` | Administration | Host-Only (VMnet1) | 192.168.20.50/24 |

## 2. Problématique rencontrée (Conflit d'adressage)
Lors de la configuration initiale, l'interface Host-Only (`ens39`) avait été configurée sur le réseau `192.168.188.0/24`. Cependant, l'interface `vmnet1` de la machine hôte (Linux) était sur le réseau `192.168.20.0/24`. 

**Conséquence :** Impossible de faire un `ping` ou un `ssh` entre l'hôte et la VM (erreur `Connection timed out`).

**Solution :** Modification de l'IP de l'interface `ens39` de la VM pour l'aligner sur le sous-réseau de l'hôte (`192.168.20.50`). La connectivité a été rétablie.

## 3. Fichier de configuration
Le fichier `/etc/network/interfaces` contient la configuration statique (hors WAN en DHCP).
