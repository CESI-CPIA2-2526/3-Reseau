---
marp: true
theme: default
paginate: true
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
header: '**Fondamentaux des Réseaux** | CESI'
footer: 'Rohan Fossé | 2026'
style: |
  section {
    font-size: 28px;
  }
  h1 {
    color: #0066cc;
    border-bottom: 3px solid #0066cc;
    padding-bottom: 10px;
  }
  h2 {
    color: #0088ff;
  }
  h3 {
    color: #00aaff;
  }
  table {
    font-size: 22px;
    border-collapse: collapse;
  }
  table th {
    background-color: #0066cc;
    color: white;
    padding: 8px;
  }
  table td {
    padding: 6px;
    border: 1px solid #ddd;
  }
  code {
    background: #f4f4f4;
    padding: 2px 6px;
    border-radius: 3px;
  }
  header {
    color: #0066cc;
    font-size: 18px;
    padding: 10px;
  }
  footer {
    color: #666;
    font-size: 16px;
  }
  section::after {
    content: attr(data-marpit-pagination) ' / ' attr(data-marpit-pagination-total);
    position: absolute;
    bottom: 20px;
    right: 30px;
    font-size: 18px;
    color: #0066cc;
    font-weight: bold;
  }
  section.invert::after {
    color: white;
  }
  /* Barre de progression en haut */
  section::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 6px;
    background: #e0e0e0;
    z-index: 1000;
  }
  /* Remplissage progressif - sera calculé par slide */
  section[data-marpit-pagination="1"]::before { background: linear-gradient(to right, #0066cc 3%, #e0e0e0 3%); }
  section[data-marpit-pagination="2"]::before { background: linear-gradient(to right, #0066cc 6%, #e0e0e0 6%); }
  section[data-marpit-pagination="3"]::before { background: linear-gradient(to right, #0066cc 9%, #e0e0e0 9%); }
  section[data-marpit-pagination="4"]::before { background: linear-gradient(to right, #0066cc 12%, #e0e0e0 12%); }
  section[data-marpit-pagination="5"]::before { background: linear-gradient(to right, #0066cc 15%, #e0e0e0 15%); }
  section[data-marpit-pagination="6"]::before { background: linear-gradient(to right, #0066cc 18%, #e0e0e0 18%); }
  section[data-marpit-pagination="7"]::before { background: linear-gradient(to right, #0066cc 21%, #e0e0e0 21%); }
  section[data-marpit-pagination="8"]::before { background: linear-gradient(to right, #0066cc 24%, #e0e0e0 24%); }
  section[data-marpit-pagination="9"]::before { background: linear-gradient(to right, #0066cc 27%, #e0e0e0 27%); }
  section[data-marpit-pagination="10"]::before { background: linear-gradient(to right, #0066cc 30%, #e0e0e0 30%); }
  section[data-marpit-pagination="11"]::before { background: linear-gradient(to right, #0066cc 33%, #e0e0e0 33%); }
  section[data-marpit-pagination="12"]::before { background: linear-gradient(to right, #0066cc 36%, #e0e0e0 36%); }
  section[data-marpit-pagination="13"]::before { background: linear-gradient(to right, #0066cc 39%, #e0e0e0 39%); }
  section[data-marpit-pagination="14"]::before { background: linear-gradient(to right, #0066cc 42%, #e0e0e0 42%); }
  section[data-marpit-pagination="15"]::before { background: linear-gradient(to right, #0066cc 45%, #e0e0e0 45%); }
  section[data-marpit-pagination="16"]::before { background: linear-gradient(to right, #0066cc 48%, #e0e0e0 48%); }
  section[data-marpit-pagination="17"]::before { background: linear-gradient(to right, #0066cc 51%, #e0e0e0 51%); }
  section[data-marpit-pagination="18"]::before { background: linear-gradient(to right, #0066cc 54%, #e0e0e0 54%); }
  section[data-marpit-pagination="19"]::before { background: linear-gradient(to right, #0066cc 57%, #e0e0e0 57%); }
  section[data-marpit-pagination="20"]::before { background: linear-gradient(to right, #0066cc 60%, #e0e0e0 60%); }
  section[data-marpit-pagination="21"]::before { background: linear-gradient(to right, #0066cc 63%, #e0e0e0 63%); }
  section[data-marpit-pagination="22"]::before { background: linear-gradient(to right, #0066cc 66%, #e0e0e0 66%); }
  section[data-marpit-pagination="23"]::before { background: linear-gradient(to right, #0066cc 69%, #e0e0e0 69%); }
  section[data-marpit-pagination="24"]::before { background: linear-gradient(to right, #0066cc 72%, #e0e0e0 72%); }
  section[data-marpit-pagination="25"]::before { background: linear-gradient(to right, #0066cc 75%, #e0e0e0 75%); }
  section[data-marpit-pagination="26"]::before { background: linear-gradient(to right, #0066cc 78%, #e0e0e0 78%); }
  section[data-marpit-pagination="27"]::before { background: linear-gradient(to right, #0066cc 81%, #e0e0e0 81%); }
  section[data-marpit-pagination="28"]::before { background: linear-gradient(to right, #0066cc 84%, #e0e0e0 84%); }
  section[data-marpit-pagination="29"]::before { background: linear-gradient(to right, #0066cc 87%, #e0e0e0 87%); }
  section[data-marpit-pagination="30"]::before { background: linear-gradient(to right, #0066cc 90%, #e0e0e0 90%); }
  section[data-marpit-pagination="31"]::before { background: linear-gradient(to right, #0066cc 93%, #e0e0e0 93%); }
  section[data-marpit-pagination="32"]::before { background: linear-gradient(to right, #0066cc 96%, #e0e0e0 96%); }
  section[data-marpit-pagination="33"]::before { background: linear-gradient(to right, #0066cc 100%, #e0e0e0 100%); }
---

<!-- _class: invert -->
<!-- _header: "" -->
<!-- _footer: "" -->
<!-- _paginate: false -->

# Projet Réseau
## Rohan Fossé

### Module : Fondamentaux des Réseaux
De la théorie à la pratique

---

#### Janvier 2026

---

# Vue d'ensemble

## Objectif
Fondamentaux des réseaux, de la théorie à la pratique

## Les boucles
1. Modèles OSI & TCP/IP
2. Accès réseau (physique & liaison)
3. Routage et adressage IP
4. Réseau local et services

---

# Pourquoi des modèles en couches ?

## Avantages
- **Modularité** : Modifier une couche indépendamment
- **Standardisation** : Compatibilité entre fabricants
- **Simplification** : Division des problèmes complexes

---

# Le modèle OSI - 7 couches

| Couche | Nom | Rôle |
|--------|-----|------|
| **7** | Application | Interface utilisateur |
| **6** | Présentation | Format, chiffrement |
| **5** | Session | Gestion sessions |
| **4** | Transport | TCP/UDP |
| **3** | Réseau | Routage IP |
| **2** | Liaison | Trames, MAC |
| **1** | Physique | Transmission bits |

---

# Détails couches basses

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">

<div>

## Couche 1 - Physique
- Transmission bits
- Câbles, hubs

## Couche 2 - Liaison
- Trames, MAC
- Switches

</div>

<div>

## Couche 3 - Réseau
- Paquets, IP
- Routeurs

## Couche 4 - Transport
- TCP (fiable)
- UDP (rapide)

</div>

</div>

---

# Ports et services

| Port | Service |
|------|---------|
| 80 | HTTP |
| 443 | HTTPS |
| 22 | SSH |
| 53 | DNS |
| 21 | FTP |
| 25 | SMTP |

---

# TCP/IP - 4 couches

```
OSI (7)              TCP/IP (4)
─────────            ──────────
7-6-5 App/Pres/Ses → Application
4 Transport        → Transport
3 Réseau           → Internet
2-1 Liaison/Phys   → Accès réseau
```

**Modèle pratique** utilisé sur Internet

---

# L'encapsulation des données

## Le processus d'emballage successif

```
Application    → DONNÉES
                 ↓ (+ en-tête TCP/UDP)
Transport      → SEGMENT / DATAGRAMME
                 ↓ (+ en-tête IP)
Réseau         → PAQUET
                 ↓ (+ en-tête Ethernet + FCS)
Liaison        → TRAME
                 ↓ (conversion en signaux)
Physique       → BITS
```

## À la réception
**Désencapsulation** : Chaque couche retire son en-tête

---

# Exemple - Navigation Web

## Consulter www.example.com

1. **L7** : Requête HTTP
2. **L4** : TCP + ports
3. **L3** : IP source/dest
4. **L2** : MAC source/dest
5. **L1** : Signaux électriques

**Réception** : Désencapsulation inverse

---

# Supports physiques

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">

<div>

## Câble cuivre (UTP)
| Cat | Vitesse | Dist |
|-----|---------|------|
| 5e  | 1 Gbps  | 100m |
| 6   | 10 Gbps | 55m  |
| 6a  | 10 Gbps | 100m |

**Connecteur : RJ45**

</div>

<div>

## Fibre optique
| Type | Distance |
|------|----------|
| Monomode | 10-100 km |
| Multimode | 500m-2km |

**Très haut débit, immunité**

</div>

</div>

---


---

# Wi-Fi (IEEE 802.11)

| Norme | Fréquence | Débit max |
|-------|-----------|-----------|
| 802.11n (Wi-Fi 4) | 2.4/5 GHz | 600 Mbps |
| 802.11ac (Wi-Fi 5) | 5 GHz | 3.5 Gbps |
| 802.11ax (Wi-Fi 6) | 2.4/5/6 GHz | 9.6 Gbps |

**Avantages** : Mobilité, déploiement facile
**Inconvénients** : Interférences, sécurité complexe

---

# Adressage MAC

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">

<div>

## Format
**48 bits** (6 octets)
`00:1A:2B:3C:4D:5E`

**Structure**
- 3 octets : Fabricant (OUI)
- 3 octets : Série unique

</div>

<div>

## Types
- **Unicast** : 1 destinataire
- **Broadcast** : Tous
  `FF:FF:FF:FF:FF:FF`
- **Multicast** : Groupe

</div>

</div>

---

# Trame Ethernet II

```
┌──────┬──────┬──────┬──────┬─────┬─────┐
│Préam │ MAC  │ MAC  │ Type │Data │ FCS │
│ 8oct │ dest │ src  │ 2oct │1500 │4oct │
└──────┴──────┴──────┴──────┴─────┴─────┘
```

**Taille** : 64 à 1518 octets | **MTU** : 1500

---

# Protocole ARP

**Problème** : Connaît IP, besoin MAC
**Solution** : ARP = IP ↔ MAC

## Fonctionnement
1. Requête broadcast : "Qui a l'IP X ?"
2. Réponse unicast : "Moi ! MAC = Y"
3. Cache ARP temporaire

---

# Équipements réseau

| Équipement | Couche | Fonction |
|------------|--------|----------|
| **Hub** | 1 | Répète signal partout (obsolète) |
| **Switch** | 2 | Transmet selon MAC |
| **Routeur** | 3 | Route selon IP |

---

# Switch - Table MAC

## Processus
1. Trame arrive → Note "MAC source → port"
2. MAC connue ? → Envoi direct
3. MAC inconnue ? → Diffusion

**Timeout** : 300s

---

# IPv4

**Format** : 32 bits / 4 octets
`192.168.1.100` = `11000000.10101000.00000001.01100100`

**Structure**
- Partie réseau + Partie hôte
- Masque : `255.255.255.0` ou `/24`

---

# Classes IPv4

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">

<div>

| Classe | Masque | Hôtes |
|--------|--------|-------|
| **A** | /8 | 16M+ |
| **B** | /16 | 65k+ |
| **C** | /24 | 254 |

</div>

<div>

**Privées (RFC 1918)**
- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

**Loopback** : `127.0.0.1`

</div>

</div>

---

# Subnetting

**Pourquoi ?** Segmentation, sécurité, optimisation

**Exemple : `192.168.1.0/24`**
- Sans : 1 réseau, 254 hôtes
- Avec /26 : 4 réseaux, 62 hôtes chacun

---

# Calcul subnetting

**Formules**
- Sous-réseaux = 2^(bits empruntés)
- Hôtes = 2^(bits hôte) - 2

**Exemple /24 → /26**
- 2 bits empruntés = 4 sous-réseaux
- 6 bits hôte = 62 hôtes

---

# Routage

**Fonction** : Acheminer paquets entre réseaux

**Types de routes**
- Connectées (directes)
- Statiques (manuelles)
- Dynamiques (RIP, OSPF, EIGRP)

---

# Passerelle par défaut

**0.0.0.0/0** = Route de dernier recours

PC → Internet : Utilise la passerelle par défaut

---

# VLANs

**Définition** : Segmentation logique réseau

**Avantages**
- Sécurité (isolation)
- Performance (moins broadcast)
- Flexibilité

**Types** : Data, Voice, Management

---

# Configuration VLAN

```
# Créer VLAN
vlan 10
 name COMPTA

# Port access
interface fa0/1
 switchport mode access
 switchport access vlan 10

# Port trunk
interface gi0/1
 switchport mode trunk
```

---

# DNS

**Fonction** : Nom → IP
`www.google.com` → `142.250.74.206`

**Hiérarchie**
```
. (root) → .com → google.com → www
```

---

# Enregistrements DNS

| Type | Fonction |
|------|----------|
| **A** | Nom → IPv4 |
| **AAAA** | Nom → IPv6 |
| **CNAME** | Alias |
| **MX** | Messagerie |
| **NS** | Serveur noms |

---

# Résolution DNS

1. Cache local
2. Serveur récursif
3. Serveur racine
4. Serveur TLD
5. Serveur autoritaire
6. Mise en cache

**Commandes** : `nslookup`, `dig`

---

# DHCP

**Fonction** : Attribution auto IP

**Processus DORA**
1. **D**iscover (broadcast)
2. **O**ffer (serveur)
3. **R**equest (client)
4. **A**cknowledge (serveur)

---

# Sécurité réseau

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">

<div>

**CIA Triad**
- Confidentialité
- Intégrité
- Disponibilité

</div>

<div>

**Bonnes pratiques**
- HTTPS, SSH, TLS
- Mots de passe forts
- VLANs
- Mises à jour

</div>

</div>

---

# Outils diagnostic

| Commande | Fonction |
|----------|----------|
| `ping` | Test connectivité |
| `tracert` | Tracer chemin |
| `ipconfig` | Config IP |
| `nslookup` | Requête DNS |
| `arp -a` | Table ARP |

**Wireshark** : Analyse trafic

---

# Travaux pratiques

1. Configuration LAN de base
2. VLANs et trunking
3. Subnetting et routage
4. DHCP et DNS
5. Analyse Wireshark

---

# Points clés

1. OSI (7) et TCP/IP (4)
2. Encapsulation des données
3. MAC (L2) vs IP (L3)
4. ARP = IP ↔ MAC
5. Switch (MAC) vs Routeur (IP)
6. Subnetting et VLANs
7. DNS et DHCP

---

# Pour aller plus loin

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">

<div>

**Certifications**
- CCNA
- CompTIA Network+

**Outils**
- Packet Tracer
- GNS3

</div>

<div>

**Documentation**
- RFCs
- Cisco Academy
- Forums techniques

</div>

</div>

---

# Questions

1. Couche OSI du routage ?
2. TCP vs UDP ?
3. Hôtes dans /26 ?
4. Rôle ARP ?
5. Qu'est-ce qu'un VLAN ?
6. Commande test connectivité ?
7. DNS = ?
8. 3 premiers octets MAC = ?

---

# Réponses

1. Couche 3
2. TCP (fiable) / UDP (rapide)
3. 62 hôtes
4. IP → MAC
5. Segmentation logique
6. `ping`
7. Domain Name System
8. OUI (fabricant)

---

<!-- _class: invert -->
# Merci !
