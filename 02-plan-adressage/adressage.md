# Plan d'adressage

## Plage IP globale

| Paramètre | Valeur |
|---|---|
| Réseau de base | 192.168.0.0/21 |
| Plage totale | 192.168.0.0 → 192.168.7.255 |
| Nombre d'adresses | 2048 |
| Méthode | VLSM (Variable Length Subnet Mask) |

> Le VLSM permet d'allouer des sous-réseaux de taille adaptée à chaque besoin, évitant le gaspillage d'adresses IP.

---

## Subnetting — Tableau complet

Les sous-réseaux sont alloués du plus grand au plus petit (bonne pratique VLSM).

| Sous-réseau | Site | Équipements | Masque | @IP réseau | @IP diffusion | Plage hôtes |
|---|---|---|---|---|---|---|
| LAN1 | Paris | 500 | /23 | 192.168.0.0 | 192.168.1.255 | 192.168.0.1 → 192.168.1.254 |
| LAN4 | Marseille | 50 | /26 | 192.168.2.0 | 192.168.2.63 | 192.168.2.1 → 192.168.2.62 |
| LAN5 | Toulouse | 40 | /26 | 192.168.2.64 | 192.168.2.127 | 192.168.2.65 → 192.168.2.126 |
| LAN2 | Nantes | 30 | /26 | 192.168.2.128 | 192.168.2.191 | 192.168.2.129 → 192.168.2.190 |
| LAN3 | Strasbourg | 30 | /26 | 192.168.2.192 | 192.168.2.255 | 192.168.2.193 → 192.168.2.254 |
| R1–R2 | WAN | 2 | /30 | 192.168.3.0 | 192.168.3.3 | 192.168.3.1 → 192.168.3.2 |
| R1–R3 | WAN | 2 | /30 | 192.168.3.4 | 192.168.3.7 | 192.168.3.5 → 192.168.3.6 |
| R1–R4 | WAN | 2 | /30 | 192.168.3.8 | 192.168.3.11 | 192.168.3.9 → 192.168.3.10 |
| R4–R5 | WAN | 2 | /30 | 192.168.3.12 | 192.168.3.15 | 192.168.3.13 → 192.168.3.14 |
| R5–R6 | WAN | 2 | /30 | 192.168.3.16 | 192.168.3.19 | 192.168.3.17 → 192.168.3.18 |

> Les liens point à point WAN utilisent des /30 : seulement 2 adresses hôtes nécessaires, évite tout gaspillage.

---

## Interfaces par routeur

### R1 — Paris (Siège)

| Interface | Type | IP | Masque | Connecté à |
|---|---|---|---|---|
| Fa0/0 | LAN | 192.168.1.254 | /23 | Switch S0 (LAN Paris) |
| Se2/0 | WAN | 192.168.3.1 | /30 | R2 (Nantes) |
| Se3/0 | WAN | 192.168.3.5 | /30 | R3 (Strasbourg) |
| Se6/0 | WAN | 192.168.3.9 | /30 | R4 (Marseille) |

### R2 — Nantes

| Interface | Type | IP | Masque | Connecté à |
|---|---|---|---|---|
| Fa0/0 | LAN | 192.168.2.190 | /26 | Switch S1 (LAN Nantes) |
| Se2/0 | WAN | 192.168.3.2 | /30 | R1 (Paris) |

### R3 — Strasbourg

| Interface | Type | IP | Masque | Connecté à |
|---|---|---|---|---|
| Fa0/0 | LAN | 192.168.2.254 | /26 | Switch S2 (LAN Strasbourg) |
| Se2/0 | WAN | 192.168.3.6 | /30 | R1 (Paris) |

### R4 — Marseille

| Interface | Type | IP | Masque | Connecté à |
|---|---|---|---|---|
| Fa0/0 | LAN | 192.168.2.62 | /26 | Switch S3 (LAN Marseille) |
| Se2/0 | WAN | 192.168.3.10 | /30 | R1 (Paris) |
| Se3/0 | WAN | 192.168.3.13 | /30 | R5 (WAN) |

### R5 — Routeur WAN intermédiaire

| Interface | Type | IP | Masque | Connecté à |
|---|---|---|---|---|
| Se2/0 | WAN | 192.168.3.14 | /30 | R4 (Marseille) |
| Se3/0 | WAN | 192.168.3.17 | /30 | R6 (Toulouse) |

### R6 — Toulouse

| Interface | Type | IP | Masque | Connecté à |
|---|---|---|---|---|
| Fa0/0 | LAN | 192.168.2.126 | /26 | Switch S4 (LAN Toulouse) |
| Se2/0 | WAN | 192.168.3.18 | /30 | R5 (WAN) |

---

## Configuration des PCs

| PC | Site | IP | Masque | Passerelle |
|---|---|---|---|---|
| PC0-1 | Paris | DHCP | /23 | 192.168.1.254 |
| PC2 | Nantes | 192.168.2.129 | /26 | 192.168.2.190 |
| PC3 | Strasbourg | 192.168.2.193 | /26 | 192.168.2.254 |
| PC4 | Marseille | 192.168.2.1 | /26 | 192.168.2.62 |
| PC5 | Toulouse | 192.168.2.65 | /26 | 192.168.2.126 |

> PC0 et PC1 (Paris) reçoivent IP automatiquement via le serveur DHCP configuré sur R1. Les autres PCs sont configurés en IP statique.
