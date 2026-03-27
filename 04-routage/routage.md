# Routage Statique

## Principe

Le routage statique consiste à définir manuellement les chemins que doivent emprunter les paquets pour atteindre les réseaux distants.

**Règle générale :**
- Les réseaux **directement connectés** sont automatiquement connus du routeur (type C).
- Les réseaux **distants** doivent être ajoutés manuellement via `ip route` (type S).

---

## Table de routage — R1 (Paris)

| Type | Réseau destination | Masque | Interface sortie | Prochain saut |
|---|---|---|---|---|
| C | 192.168.0.0/23 | /23 | Fa0/0 (192.168.1.254) | — |
| C | 192.168.3.0/30 | /30 | Se2/0 (192.168.3.1) | — |
| C | 192.168.3.4/30 | /30 | Se3/0 (192.168.3.5) | — |
| C | 192.168.3.8/30 | /30 | Se6/0 (192.168.3.9) | — |
| S | 192.168.2.128/26 | /26 | Se2/0 | 192.168.3.2 (R2) |
| S | 192.168.2.192/26 | /26 | Se3/0 | 192.168.3.6 (R3) |
| S | 192.168.2.0/26 | /26 | Se6/0 | 192.168.3.10 (R4) |
| S | 192.168.2.64/26 | /26 | Se6/0 | 192.168.3.10 (R4) |
| S | 192.168.3.12/30 | /30 | Se6/0 | 192.168.3.10 (R4) |
| S | 192.168.3.16/30 | /30 | Se6/0 | 192.168.3.10 (R4) |

> Pour atteindre LAN5 (Toulouse) et LAN4 (Marseille), R1 passe par R4 qui se charge de la suite du chemin.

### Commandes R1

```cisco
R1(config)# ip route 192.168.2.128 255.255.255.192 192.168.3.2
R1(config)# ip route 192.168.2.192 255.255.255.192 192.168.3.6
R1(config)# ip route 192.168.2.0 255.255.255.192 192.168.3.10
R1(config)# ip route 192.168.2.64 255.255.255.192 192.168.3.10
R1# write memory
```
> Chaque interface des routeurs est configurée de cette manière.
> Table de routage + commandes

---

## Vérification

```cisco
! Afficher la table de routage complète
Router# show ip route
