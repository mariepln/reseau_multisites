# 📦 Réseau Physique — Équipements et Câblage

## Équipements réseau

### Routeurs

| Nom | Modèle | Site | Rôle | Nb interfaces |
|---|---|---|---|---|
| R1 | Cisco PT Router | Paris | Siège — nœud central | 4 |
| R2 | Cisco PT Router | Nantes | Agence Ouest | 2 |
| R3 | Cisco PT Router | Strasbourg | Agence Est | 2 |
| R4 | Cisco PT Router | Marseille | Agence Sud | 3 |
| R5 | Cisco PT Router | WAN | Routeur intermédiaire | 2 |
| R6 | Cisco PT Router | Toulouse | Agence Sud-Ouest | 2 |

> ⚠️ Les routeurs PT nécessitent l'ajout du module **WIC-2T** pour les interfaces série (liens WAN).

### Switches

| Nom | Modèle | Site |
|---|---|---|
| S1 | Cisco 2960 | Paris |
| S2 | Cisco 2960 | Nantes |
| S3 | Cisco 2960 | Strasbourg |
| S4 | Cisco 2960 | Marseille |
| S6 | Cisco 2960 | Toulouse |

> ℹ️ R5 n'a pas de switch ni de LAN associé — rôle de routeur WAN intermédiaire uniquement.

### Équipements terminaux

| Nom | Site | LAN |
|---|---|---|
| PC1 | Paris | LAN1 — 192.168.0.0/23 |
| PC2 | Nantes | LAN2 — 192.168.2.128/26 |
| PC3 | Strasbourg | LAN3 — 192.168.2.192/26 |
| PC4 | Marseille | LAN4 — 192.168.2.0/26 |
| PC5 | Toulouse | LAN5 — 192.168.2.64/26 |

> ℹ️ Chaque LAN est représenté par 1 PC en simulation. Le plan d'adressage est dimensionné pour le nombre réel d'équipements en production.

---

## Câblage

### Liens WAN — Câbles série (DCE/DTE)

| De | Interface | Vers | Interface | Clock Rate |
|---|---|---|---|---|
| R1 | Se2/0 | R2 | Se2/0 | 64000 (DCE côté R1) |
| R1 | Se3/0 | R3 | Se2/0 | 64000 (DCE côté R1) |
| R1 | Se6/0 | R4 | Se2/0 | 64000 (DCE côté R1) |
| R4 | Se3/0 | R5 | Se2/0 | 64000 (DCE côté R4) |
| R5 | Se3/0 | R6 | Se2/0 | 64000 (DCE côté R5) |

> ℹ️ Sur un lien série, le côté **DCE** fournit l'horloge avec la commande `clock rate`. Le côté DTE ne nécessite pas cette commande.

### Liens LAN — Câbles droits

| De | Interface | Vers | Interface |
|---|---|---|---|
| R1 | Fa0/0 | S1 | Fa0/1 |
| R2 | Fa0/0 | S2 | Fa0/1 |
| R3 | Fa0/0 | S3 | Fa0/1 |
| R4 | Fa0/0 | S4 | Fa0/1 |
| R6 | Fa0/0 | S6 | Fa0/1 |
| S1 | Fa0/2 | PC1 | Fa0 |
| S2 | Fa0/2 | PC2 | Fa0 |
| S3 | Fa0/2 | PC3 | Fa0 |
| S4 | Fa0/2 | PC4 | Fa0 |
| S6 | Fa0/2 | PC5 | Fa0 |
