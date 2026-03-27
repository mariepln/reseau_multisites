# Configuration des Routeurs

> Accès initial via **câble console** (PC → port console du routeur) pour la première configuration.  
> Accès distant sécurisé via **SSH** pour LAN1 une fois la configuration réseau en place.

---

## R1 — Paris (Siège central)

### Interfaces

```cisco
Router> enable
Router# configure terminal

! Nommage du routeur
Router(config)# hostname R1

! Interface LAN — Paris
R1(config)# interface fa0/0
R1(config-if)# ip address 192.168.1.254 255.255.254.0
R1(config-if)# no shutdown
R1(config-if)# exit

! Interface WAN — vers R2 (Nantes)
R1(config)# interface se2/0
R1(config-if)# ip address 192.168.3.1 255.255.255.252
R1(config-if)# clock rate 64000
R1(config-if)# no shutdown
R1(config-if)# exit

! Interface WAN — vers R3 (Strasbourg)
R1(config)# interface se3/0
R1(config-if)# ip address 192.168.3.5 255.255.255.252
R1(config-if)# clock rate 64000
R1(config-if)# no shutdown
R1(config-if)# exit

! Interface WAN — vers R4 (Marseille)
R1(config)# interface se6/0
R1(config-if)# ip address 192.168.3.9 255.255.255.252
R1(config-if)# clock rate 64000
R1(config-if)# no shutdown
R1(config-if)# exit

> **configuration de chaque interface des routeurs dans la même logique.**

```

### DHCP — LAN1 Paris (500 équipements)

```cisco

! Pool DHCP pour le LAN1 Paris
R1(config)# ip dhcp pool lan1-Paris
R1(dhcp-config)# network 192.168.0.0 255.255.254.0
R1(dhcp-config)# default-router 192.168.1.254
R1(dhcp-config)# dns-server 8.8.8.8
R1(dhcp-config)# exit

! Exclusion des adresses réservées (passerelle + équipements fixes)
R1(config)# ip dhcp excluded-address 192.168.1.250 192.168.1.254
```

> Les adresses 192.168.1.250 à 192.168.1.254 sont réservées aux équipements réseau (routeur, switches, serveurs) et exclues du pool DHCP.

### SSH — Accès distant sécurisé

```cisco
! Nom de domaine requis pour la génération de clé RSA
R1(config)# ip domain-name lan1-Paris

! Génération de la clé RSA 2048 bits
R1(config)# crypto key generate rsa
! Choisir 2048 bits à l'invite

! Forcer SSH version 2 (plus sécurisé que v1)
R1(config)# ip ssh version 2

! Création du compte administrateur local
R1(config)# username cisco secret cisco

! Mot de passe enable
R1(config)# enable secret cisco

! Configuration des lignes VTY (accès distant)
R1(config)# line vty 0 4
R1(config-line)# transport input ssh
R1(config-line)# login local
R1(config-line)# exit

R1# write memory

```

> ⚠️ En environnement de production, utiliser des mots de passe complexes et différents pour `username` et `enable secret`.
> Tous les équipements réseau (routeurs + switchs) sont administrables via SSH pour garantir un accès sécurisé distant”

---

## Vérification des interfaces

Après configuration, vérification sur chaque routeur :

```cisco
Router# show ip interface brief
```

Toutes les interfaces configurées doivent afficher le statut `up/up`.
