# AP3-SIO2

[Réseau & VLANs](https://github.com/h3nr1-art/ap3-sio2/blob/main/R%C3%A9seau%20%26%20VLANs)  
[Contrôleur de domaine & DFS](https://github.com/h3nr1-art/ap3-sio2/blob/main/Contr%C3%B4leur%20de%20domaine%20%26%20DFS)  
[Cloud privé & DMZ](https://github.com/h3nr1-art/ap3-sio2/blob/main/Cloud%20priv%C3%A9%20%26%20DMZ)  
[Cluster WEB + load balancer](https://github.com/h3nr1-art/ap3-sio2/blob/main/Cluster%20WEB%20%2B%20load%20balancer)  

## Plan adressage ip

| Services                           | Adresse réseau   | Masque          | Broadcast     | Gateway       |
|------------------------------------|------------------|-----------------|---------------|---------------|
| Salles serveur VLAN                | 192.168.1.1/27   | 255.255.255.224 | 192.168.1.32  | 192.168.1.31  |
| Service informatique/dévellopement | 192.168.1.65/26  | 255.255.255.192 | 192.168.1.96  | 192.168.1.95  |
| Service commerciale                | 192.168.1.129/26 | 255.255.255.192 | 192.168.1.160 | 192.168.1.159 |
| Bureau d’étude                     | 192.168.1.33/27  | 255.255.255.224 | 192.168.1.192 | 192.168.1.191 |
| RH/Compta                          | 192.168.1.17/28  | 255.255.255.240 | 192.168.1.218 | 192.168.1.217 |
| Direction                          | 192.168.1.1/28   | 255.255.255.240 | 192.168.1.234 | 192.168.1.233 |
