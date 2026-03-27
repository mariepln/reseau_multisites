# Infrastructure Réseau WAN Multi-Sites

> Simulation d'un réseau WAN d'entreprise multi-sites réalisée sur **Cisco Packet Tracer**.  
> Ce projet couvre la conception physique, le plan d'adressage, la configuration des équipements, le routage statique et les tests de connectivité.

---

## Objectifs du projet

Concevoir et configurer un réseau d’entreprise multi-sites comprenant :

- 6 routeurs (R1 → R6)
- 5 LAN (Paris, Nantes, Strasbourg, Marseille, Toulouse)
- Liaisons WAN en point-à-point (/30)
- Routage statique
- DHCP, SSH, tests de connectivité

---

## Topologie

```
                    [LAN2 - Nantes]
                          |
[LAN1 - Paris] ── R1 ── R2
                    |
                   R3 ── [LAN3 - Strasbourg]
                    |
                   R4 ── [LAN4 - Marseille]
                    |
                   R5         ← Routeur WAN intermédiaire
                    |
                   R6 ── [LAN5 - Toulouse]
```

> Voir le schéma complet : `01-reseau-physique_topologie.png`

---

## Technologies utilisées

- **Cisco Packet Tracer** — simulation réseau
- **Routeurs Cisco PT** — 6 routeurs
- **Câbles série** — liens WAN point à point
- **Câbles droits** — liens LAN (routeur ↔ switch ↔ PC)
- **Protocoles** — IP statique, DHCP, SSH, routage statique

---

## Structure du projet

| Dossier | Contenu |
|---|---|
| `01-reseau-physique/` | Topologie, équipements, câblage |
| `02-plan-adressage/` | Subnetting et plan IP complet |
| `03-config-terminaux/` | Configuration des PCs |
| `04-config-routeurs/` | Configurations R1 à R6|
| `05-routage-statique/` | Tables de routage statique |
| `06-tests-connectivite/` | Rapport de tests |
| `fichier-pt/` | Fichier Packet Tracer (.pkt) |

---

## Etapes de mise en place

- Réseau physique — topologie et câblage
- Plan d'adressage — attribution VLSM, WAN/30, passerelles
- Configuration équipements terminaux
- Configuration routeurs (interfaces + DHCP + SSH)
- Routage statique
- Tests de connectivité totale

---

## Compétences démontrées

- Conception d'un réseau WAN multi-sites
- Subnetting VLSM à partir d'une plage /21
- Configuration d'interfaces série et FastEthernet sur Cisco IOS
- Mise en place d'un serveur DHCP sur routeur Cisco
- Sécurisation des accès distants via SSH (RSA 2048 bits)
- Routage statique inter-sites
- Tests de connectivité et traçage de routes (ping / tracert)
