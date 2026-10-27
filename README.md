# Operació Nord Tec (Raúl Cebreros Ruiz , ASIX1B)
## Índex
* ***1.- Estat del projecte***
* ***2.- Arquitectura de xarxa***
* ***3.- Configuracions***
* ***4.- Incidencies i solucions***
* ***5.- Estat del projecte***
* ***6.- Arquitectura de xarxa***
* ***7.- Configuracions***
* ***8.- Incidències i solucions***
* ***9.- Missatge d'error exacte***
* ***10.- Quan: fase i context***
* ***11.- Causa: perquè passava***
* ***12.- Solució: què vam fer***
* ***13.- Detectada per: @usuari***
* ***14.- Decisions tècnices***
* ***15.- Reflexions tècniques***
## Estat del projecte
Els primers equips han arribat a l'oficina i necesiten estar connectats a la xarxa i pugin sortir a internet. Volen una configuració ben ordenada i documentada.
## Arquitectura de xarxa
maquina firewall:
#!/bin/bash

#netejem taules
iptables -F
iptables -t nat -F
iptables -X

#política per defecte
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT

#sortir a internet
iptables -t nat -A POSTROUTING -s 192.168.10.0/24 -o enp1s0 -j MASQUERADE  
iptables -t nat -A POSTROUTING -s 192.168.20.0/24 -o enp1s0 -j MASQUERADE
iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -o enp1s0 -j MASQUERADE

#publicar el servidor web
#DNAT
iptables -t nat -A PREROUTING -i enp3s0 -p tcp --dport 80 -j DNAT --to-destination 192.168.10.10
iptables -t nat -A PREROUTING -i enp3s0 -p tcp -d 10.0.0.1 --dport 80 -j DNAT --to-destination 192.168.10.10

## Configuracions
* ubuntu.desk: Configurem la ip amb 192.168.20.10/24 i l'enllaçem amb la ip de la firewall (192.168.20.1)
* ubuntu.server: Configurem la ip amb 192.168.10.10/24 i l'enllaçem amb la ip de la firewall (192.168.10.1)
## Incidències i solucions
## Missatge d'error exacte
## Quan: fase i context
## Causa: perquè passava
## Solució: què vam fer
## Detectada per: @usuari
## Decisions tècnices
## Reflexions tècniques