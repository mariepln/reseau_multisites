# Tests de Connectivité

## Méthodologie

Les tests sont effectués depuis chaque PC vers tous les autres PCs du réseau afin de valider la connectivité totale inter-sites. Deux outils sont utilisés :

- **ping** — vérifie que la destination est joignable
- **tracert** — affiche le chemin emprunté par les paquets (utile pour valider le routage)

---

## Test détaillé — PC5 (Toulouse) vers PC4 (Marseille)

### Ping

```
C:\> ping 192.168.2.1

Pinging 192.168.2.1 with 32 bytes of data:

Reply from 192.168.2.1: bytes=32 time=40ms TTL=125
Reply from 192.168.2.1: bytes=32 time=2ms TTL=125
Reply from 192.168.2.1: bytes=32 time=2ms TTL=125
Reply from 192.168.2.1: bytes=32 time=19ms TTL=125

Ping statistics for 192.168.2.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
    Approximate round trip times in milli-seconds:
    Minimum = 2ms, Maximum = 40ms, Average = 15ms
```

**0% de perte** — connectivité totale confirmée.

### Tracert

```
C:\> tracert 192.168.2.1

Tracing route to 192.168.2.1 over a maximum of 30 hops:

1   0 ms   0 ms   0 ms   192.168.2.126   ← Passerelle R6 (Toulouse)
2   5 ms   2 ms   0 ms   192.168.3.14    ← Interface R5 (WAN)
3   2 ms   1 ms   2 ms   192.168.3.18    ← Interface R4 (Marseille)
4   1 ms   1 ms   0 ms   192.168.2.1     ← PC4 destination

Trace complete.
```

**Analyse du chemin :**

```
PC5 (Toulouse)
    ↓
R6 (192.168.2.126) — passerelle LAN Toulouse
    ↓
R5 (192.168.3.14) — routeur WAN intermédiaire
    ↓
R4 (192.168.3.18) — routeur Marseille
    ↓
PC4 (192.168.2.1) — destination
```

Le paquet traverse **3 routeurs** pour aller de Toulouse à Marseille, ce qui correspond exactement à la topologie définie. ✅

---

## Observations

- La **première réponse ping** (40ms) est plus lente car ARP doit résoudre les adresses MAC — comportement normal.
- Les réponses suivantes (2ms) reflètent la latence réelle de la simulation.
- Le **TTL = 125** indique que le paquet a traversé 3 routeurs (TTL initial 128 − 3 = 125).

---

## Commandes de vérification sur les routeurs

```cisco
! Vérifier les interfaces actives
Router# show ip interface brief

! Vérifier la table de routage
Router# show ip route

! Vérifier les sessions DHCP actives
R1# show ip dhcp binding

! Vérifier SSH
R1# show ip ssh
```
