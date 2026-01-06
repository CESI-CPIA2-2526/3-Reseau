# Guide des Boucles d'Apprentissage - Réseaux et Système

## Vue d'ensemble du parcours

Ce document présente les différentes boucles d'apprentissage du module Réseaux et Système, structurées selon une approche par problèmes (PBL). Chaque boucle développe progressivement vos compétences en réseautique, de la compréhension des modèles théoriques jusqu'à la mise en œuvre pratique de solutions réseau.

## Boucle I - Modèles de réseaux

### Objectifs d'apprentissage

À l'issue de cette boucle, vous serez capable de :

- Expliquer comment les protocoles et services réseau permettent la communication sur les réseaux
- Comprendre et différencier les modèles de référence OSI et TCP/IP
- Identifier les rôles de chaque couche dans les deux modèles
- Établir la correspondance entre les protocoles réseau et les couches appropriées

### Comprendre les modèles de référence

#### Pourquoi des modèles en couches ?

Imaginez que vous souhaitez envoyer un colis à un ami. Vous ne vous occupez pas directement du transport routier, aérien ou maritime. Vous confiez votre colis à un service postal qui gère toute la logistique. Les réseaux informatiques fonctionnent de la même manière : chaque couche se spécialise dans une tâche précise et communique avec les couches adjacentes.

**Avantages de cette approche :**

- **Modularité** : Chaque couche est indépendante, on peut modifier une couche sans affecter les autres
- **Standardisation** : Les fabricants peuvent créer des équipements compatibles
- **Simplification** : Diviser un problème complexe en sous-problèmes plus simples
- **Interopérabilité** : Différentes technologies peuvent coexister

#### Le modèle OSI (Open Systems Interconnection)

Le modèle OSI est un modèle théorique créé par l'ISO (International Organization for Standardization) en 1984. Il divise la communication réseau en **7 couches distinctes**.

**Mnémotechnique pour retenir les couches (de bas en haut) :**
"**P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way"

- **P**hysique (Physical)
- **D**onnées (Data Link)
- **N**etwork (Réseau)
- **T**ransport
- **S**ession
- **P**résentation
- **A**pplication

##### Couche 1 - Physique (Physical Layer)

**Rôle** : Transmission des bits bruts (0 et 1) sur un support physique.

**Ce qu'elle fait concrètement :**

- Définit les caractéristiques électriques (voltage, fréquence)
- Spécifie le type de câble (cuivre, fibre optique, ondes radio)
- Détermine la forme des connecteurs (RJ45, fibre LC/SC)
- Gère l'encodage des bits (comment représenter un 0 ou un 1)

**Analogie** : C'est la route sur laquelle roule le camion de livraison. Peu importe ce qu'il transporte, il faut une route physique.

**Équipements** : Câbles, répéteurs, hubs, connecteurs

**Exemple** : Un signal électrique de +5V représente un bit "1", 0V représente un bit "0" sur un câble Ethernet.

##### Couche 2 - Liaison de données (Data Link Layer)

**Rôle** : Assurer un transfert fiable entre deux équipements directement connectés.

**Ce qu'elle fait concrètement :**

- Organise les bits en **trames** (frames)
- Ajoute des adresses **MAC** (adresses physiques uniques)
- Détecte et corrige les erreurs de transmission
- Contrôle le flux de données (pour ne pas surcharger le destinataire)

**Sous-couches** :

- **LLC** (Logical Link Control) : Interface avec la couche réseau
- **MAC** (Media Access Control) : Contrôle d'accès au support, adressage physique

**Analogie** : C'est l'étiquette sur votre colis avec l'adresse de départ et d'arrivée pour le trajet local.

**Équipements** : Commutateurs (switches), ponts (bridges), cartes réseau (NIC)

**Exemple** : Une adresse MAC ressemble à `00:1A:2B:3C:4D:5E` (48 bits en hexadécimal).

##### Couche 3 - Réseau (Network Layer)

**Rôle** : Acheminer les données à travers plusieurs réseaux interconnectés.

**Ce qu'elle fait concrètement :**

- Assigne des adresses **IP** logiques (IPv4 ou IPv6)
- Détermine le meilleur chemin (**routage**)
- Fragmente les paquets si nécessaire
- Gère l'interconnexion entre réseaux différents

**Analogie** : C'est le système de code postal et de routage qui permet d'acheminer votre colis à travers plusieurs villes et pays.

**Équipements** : Routeurs, commutateurs de couche 3 (L3 switches)

**Protocoles** : IP, ICMP (ping), IGMP, ARP

**Exemple** : Votre ordinateur (192.168.1.10) envoie un paquet à un serveur web (8.8.8.8), le routeur détermine le chemin optimal.

##### Couche 4 - Transport

**Rôle** : Assurer une communication fiable de bout en bout entre applications.

**Ce qu'elle fait concrètement :**

- Segmente les données en **segments** ou **datagrammes**
- Assure la fiabilité (avec TCP) ou la rapidité (avec UDP)
- Gère le **multiplexage** : plusieurs applications simultanées via les **ports**
- Contrôle le flux et la congestion
- Ré-assemble les segments dans l'ordre

**Deux protocoles principaux :**

**TCP (Transmission Control Protocol)** - Fiable mais plus lent

- Établit une connexion (handshake en 3 étapes)
- Garantit la livraison et l'ordre des données
- Utilisé pour : HTTP, HTTPS, FTP, SSH, email

**UDP (User Datagram Protocol)** - Rapide mais non fiable

- Sans connexion
- Pas de garantie de livraison
- Utilisé pour : DNS, streaming vidéo/audio, jeux en ligne, VoIP

**Analogie** : TCP est comme un courrier recommandé avec accusé de réception. UDP est comme jeter une bouteille à la mer.

**Exemple** : Le port 80 pour HTTP, 443 pour HTTPS, 22 pour SSH, 53 pour DNS.

##### Couche 5 - Session

**Rôle** : Gérer, établir et terminer les sessions de communication entre applications.

**Ce qu'elle fait concrètement :**

- Ouvre, maintient et ferme les sessions
- Synchronise les échanges
- Gère les points de reprise en cas d'interruption

**Analogie** : C'est comme une conversation téléphonique : vous décrochez (ouverture), vous parlez (maintien), vous raccrochez (fermeture).

**Protocoles** : NetBIOS, RPC, PPTP

**Note** : Cette couche est souvent intégrée aux applications modernes.

##### Couche 6 - Présentation

**Rôle** : Formater et coder les données pour l'application.

**Ce qu'elle fait concrètement :**

- Conversion de formats de données (ASCII, EBCDIC, Unicode)
- Chiffrement/déchiffrement (SSL/TLS)
- Compression/décompression des données
- Conversion de représentation (ex: big-endian vers little-endian)

**Analogie** : C'est comme un traducteur qui convertit votre langue dans celle du destinataire.

**Exemples** : JPEG, GIF, MP3, SSL/TLS, ASCII, MPEG

##### Couche 7 - Application

**Rôle** : Fournir des services réseau directement aux applications utilisateur.

**Ce qu'elle fait concrètement :**

- Interface entre le réseau et les logiciels
- Fournit des services comme le transfert de fichiers, l'email, le web

**Analogie** : C'est l'application que vous utilisez réellement (navigateur web, client email, etc.).

**Protocoles** :

- **HTTP/HTTPS** : Navigation web
- **FTP/SFTP** : Transfert de fichiers
- **SMTP/POP3/IMAP** : Email
- **DNS** : Résolution de noms
- **DHCP** : Attribution d'adresses IP
- **SSH** : Connexion sécurisée à distance

#### Le modèle TCP/IP (DoD Model)

Le modèle TCP/IP est un modèle **pratique** développé par le DoD (Department of Defense) américain. C'est le modèle réellement utilisé sur Internet. Il comporte **4 couches**.

##### Comparaison OSI vs TCP/IP

```
OSI (7 couches)          TCP/IP (4 couches)
─────────────────────    ──────────────────
7. Application      ┐
6. Présentation     ├──→  4. Application
5. Session          ┘
4. Transport        ───→  3. Transport
3. Réseau           ───→  2. Internet
2. Liaison données  ┐
1. Physique         ├──→  1. Accès réseau
                    ┘
```

##### Couche 1 - Accès réseau (Network Access)

Combine les couches physique et liaison de données de l'OSI.

- **Protocoles** : Ethernet, Wi-Fi (802.11), PPP
- Gère l'accès physique au réseau et la transmission des trames

##### Couche 2 - Internet

Équivalent de la couche réseau OSI.

- **Protocoles** : IP, ICMP, ARP, IGMP
- Responsable de l'adressage logique et du routage

##### Couche 3 - Transport

Identique à la couche transport OSI.

- **Protocoles** : TCP, UDP
- Gère la communication de bout en bout

##### Couche 4 - Application

Combine les couches session, présentation et application de l'OSI.

- **Protocoles** : HTTP, FTP, SMTP, DNS, DHCP, SSH, Telnet
- Fournit tous les services applicatifs

#### Le processus d'encapsulation

Lorsque vous envoyez des données sur un réseau, chaque couche ajoute ses propres informations (en-tête). C'est comme emballer un cadeau dans plusieurs boîtes.

**Exemple concret : Vous envoyez un email**

1. **Couche Application** : Votre message email
   → Ajoute les en-têtes SMTP (expéditeur, destinataire, sujet)
   → Produit des **DONNÉES**

2. **Couche Transport** :
   → Ajoute l'en-tête TCP (ports source et destination, numéros de séquence)
   → Produit un **SEGMENT** (TCP) ou **DATAGRAMME** (UDP)

3. **Couche Réseau** :
   → Ajoute l'en-tête IP (adresses IP source et destination)
   → Produit un **PAQUET**

4. **Couche Liaison de données** :
   → Ajoute l'en-tête Ethernet (adresses MAC source et destination) et le trailer (FCS)
   → Produit une **TRAME**

5. **Couche Physique** :
   → Convertit la trame en **BITS** (signaux électriques, lumineux ou radio)
   → Transmet sur le support physique

**À la réception, le processus inverse se produit (désencapsulation) :**
Chaque couche retire son en-tête et passe les données à la couche supérieure.

#### Terminologie des unités de données

| Couche      | Nom de l'unité                   | Contenu                       |
| ----------- | -------------------------------- | ----------------------------- |
| Application | Données                          | Message applicatif brut       |
| Transport   | Segment (TCP) / Datagramme (UDP) | Données + en-tête L4          |
| Réseau      | Paquet                           | Segment + en-tête L3 (IP)     |
| Liaison     | Trame (Frame)                    | Paquet + en-tête L2 + trailer |
| Physique    | Bits                             | Trame convertie en signaux    |

#### Exemple pratique complet

**Scénario** : Vous consultez le site web www.example.com

1. **Application (L7)** : Votre navigateur envoie une requête HTTP GET
2. **Transport (L4)** : TCP segmente la requête, ajoute le port source (ex: 54321) et destination (80 pour HTTP)
3. **Réseau (L3)** : IP ajoute votre adresse (192.168.1.100) et celle du serveur (93.184.216.34)
4. **Liaison (L2)** : Ethernet ajoute votre MAC et celle de la passerelle par défaut
5. **Physique (L1)** : La trame est convertie en signaux électriques sur le câble

Le processus inverse se produit sur le serveur web qui reçoit votre requête.

### Approche pédagogique

Cette boucle introduit les fondements théoriques essentiels à la compréhension des réseaux. L'apprentissage s'articule autour de cas pratiques permettant de visualiser concrètement le rôle de chaque couche lors d'une communication réseau.

**Exercices recommandés** :

- Utilisez Wireshark pour capturer et analyser des trames réseau
- Identifiez les différentes couches dans une capture
- Tracez le chemin d'un paquet de votre ordinateur à un serveur distant

## Boucle II - Accès réseau

### Objectifs d'apprentissage

À l'issue de cette boucle, vous serez capable de :

- Expliquer comment les protocoles de couche physique et liaison de données prennent en charge les communications sur les réseaux
- Comprendre l'encapsulation des trames et leur transmission
- Analyser le fonctionnement des protocoles de la couche liaison de données
- Identifier les caractéristiques des supports physiques (cuivre, fibre optique, sans fil)

### La couche physique : Le support de transmission

#### Les différents types de supports

##### 1. Câbles en cuivre (paires torsadées)

**Câble UTP (Unshielded Twisted Pair)**

Le câble Ethernet standard utilisé dans la plupart des réseaux locaux. Il contient 4 paires de fils torsadés ensemble.

**Pourquoi torsader les fils ?**

- Réduit les interférences électromagnétiques (EMI)
- Annule le bruit entre les paires (diaphonie)
- Améliore la qualité du signal

**Catégories de câbles :**

| Catégorie | Bande passante | Utilisation                            |
| --------- | -------------- | -------------------------------------- |
| Cat 5e    | 100 MHz        | Gigabit Ethernet (1 Gbps) jusqu'à 100m |
| Cat 6     | 250 MHz        | Gigabit Ethernet, 10 Gbps jusqu'à 55m  |
| Cat 6a    | 500 MHz        | 10 Gigabit Ethernet jusqu'à 100m       |
| Cat 7     | 600 MHz        | 10 Gigabit Ethernet, blindé            |

**Connecteur RJ45** : Le connecteur standard à 8 broches utilisé pour Ethernet

**Normes de câblage :**

- **T568A** et **T568B** : Ordre des fils dans le connecteur
- **Câble droit (straight-through)** : Relie un ordinateur à un switch
- **Câble croisé (crossover)** : Relie deux ordinateurs directement (moins utilisé avec Auto-MDIX)

**Limites :**

- Distance maximale : 100 mètres
- Sensible aux interférences électromagnétiques
- Sensible à l'atténuation du signal

##### 2. Fibre optique

La fibre optique transmet des données sous forme d'impulsions lumineuses. C'est la technologie la plus performante pour les longues distances.

**Avantages :**

- Très longue distance (plusieurs kilomètres)
- Immunité aux interférences électromagnétiques
- Très haut débit (jusqu'à 100 Gbps et plus)
- Sécurité accrue (difficile à intercepter)
- Pas d'atténuation significative sur de grandes distances

**Types de fibre :**

**Fibre monomode (SMF - Single Mode Fiber)**

- Cœur très fin (8-10 micromètres)
- Un seul rayon lumineux (mode)
- Longue distance : 10-100 km
- Plus coûteuse
- Laser comme source lumineuse
- Utilisation : Interconnexion entre bâtiments, backbones, WAN

**Fibre multimode (MMF - Multi Mode Fiber)**

- Cœur plus large (50 ou 62.5 micromètres)
- Plusieurs rayons lumineux
- Distance moyenne : 500m à 2km
- Moins coûteuse
- LED comme source lumineuse
- Utilisation : Réseaux locaux (LAN), centres de données

**Connecteurs courants :**

- **LC** (Lucent Connector) : Petit, moderne, utilisé dans les datacenters
- **SC** (Subscriber Connector) : Carré, connexion push-pull
- **ST** (Straight Tip) : Ancien, connexion à baïonnette

##### 3. Sans fil (Wireless)

Transmission par ondes radio dans l'air.

**Normes Wi-Fi (IEEE 802.11) :**

| Norme              | Année | Fréquence   | Débit max | Portée |
| ------------------ | ----- | ----------- | --------- | ------ |
| 802.11b            | 1999  | 2.4 GHz     | 11 Mbps   | ~35m   |
| 802.11g            | 2003  | 2.4 GHz     | 54 Mbps   | ~38m   |
| 802.11n (Wi-Fi 4)  | 2009  | 2.4/5 GHz   | 600 Mbps  | ~70m   |
| 802.11ac (Wi-Fi 5) | 2013  | 5 GHz       | 3.5 Gbps  | ~35m   |
| 802.11ax (Wi-Fi 6) | 2019  | 2.4/5/6 GHz | 9.6 Gbps  | ~30m   |

**Avantages :**

- Mobilité
- Facilité de déploiement
- Pas de câblage

**Inconvénients :**

- Sensible aux interférences (murs, autres appareils)
- Moins sécurisé (nécessite chiffrement WPA2/WPA3)
- Débit partagé entre tous les utilisateurs
- Portée limitée

### La couche liaison de données : Organisation et adressage

#### Adressage MAC (Media Access Control)

**Qu'est-ce qu'une adresse MAC ?**

C'est l'adresse physique unique gravée dans la carte réseau (NIC) de chaque équipement réseau.

**Format :** 48 bits (6 octets) en hexadécimal
**Exemple :** `00:1A:2B:3C:4D:5E` ou `00-1A-2B-3C-4D-5E`

**Structure :**

- **3 premiers octets (OUI)** : Identifiant du fabricant (Organizational Unique Identifier)
  - Exemple : `00:1A:2B` = Cisco Systems
- **3 derniers octets** : Numéro de série unique attribué par le fabricant

**Types d'adresses MAC :**

1. **Unicast** : Adresse d'un seul destinataire

   - Bit le moins significatif du premier octet = 0
   - Exemple : `00:1A:2B:3C:4D:5E`

2. **Broadcast** : Adresse vers tous les équipements du réseau

   - Tous les bits à 1
   - `FF:FF:FF:FF:FF:FF`

3. **Multicast** : Adresse vers un groupe d'équipements
   - Bit le moins significatif du premier octet = 1
   - Exemple : `01:00:5E:xx:xx:xx`

#### Structure d'une trame Ethernet II

Une trame est l'unité de données de la couche liaison.

```
┌─────────────┬──────────┬──────────┬──────┬──────────────┬─────┐
│  Préambule  │   MAC    │   MAC    │ Type │   Données    │ FCS │
│   (8 oct)   │  dest.   │  source  │(2oct)│  (46-1500)   │(4oct)│
│             │  (6 oct) │  (6 oct) │      │              │     │
└─────────────┴──────────┴──────────┴──────┴──────────────┴─────┘
```

**Détails de chaque champ :**

1. **Préambule (8 octets)** :

   - 7 octets de synchronisation (`10101010`)
   - 1 octet de délimiteur de début de trame (SFD : `10101011`)
   - Signale l'arrivée d'une trame

2. **Adresse MAC de destination (6 octets)** :

   - À qui est destinée la trame

3. **Adresse MAC source (6 octets)** :

   - Qui envoie la trame

4. **Type/Longueur (2 octets)** :

   - Indique le protocole de couche supérieure
   - `0x0800` = IPv4
   - `0x86DD` = IPv6
   - `0x0806` = ARP

5. **Données (46 à 1500 octets)** :

   - Contient le paquet IP et les données applicatives
   - Minimum 46 octets (rembourrage si nécessaire)
   - Maximum 1500 octets = **MTU** (Maximum Transmission Unit)

6. **FCS - Frame Check Sequence (4 octets)** :
   - Contrôle d'erreur (CRC - Cyclic Redundancy Check)
   - Permet de détecter les trames corrompues

**Taille totale d'une trame :** 64 à 1518 octets (sans le préambule)

#### Le protocole ARP (Address Resolution Protocol)

**Problème à résoudre :**
Votre ordinateur connaît l'adresse IP de destination (ex: 192.168.1.50) mais a besoin de l'adresse MAC pour envoyer la trame. Comment la trouver ?

**Solution : ARP**

ARP fait le lien entre l'adresse IP (couche 3) et l'adresse MAC (couche 2).

**Fonctionnement en 4 étapes :**

1. **Requête ARP (Broadcast)** :

   - PC-A veut communiquer avec 192.168.1.50
   - PC-A envoie un broadcast ARP : "Qui a l'IP 192.168.1.50 ? Dis-le à 192.168.1.10"
   - MAC destination : `FF:FF:FF:FF:FF:FF` (tous les équipements reçoivent)

2. **Réception par tous** :

   - Tous les équipements du réseau local reçoivent la requête
   - Seul celui qui a l'IP 192.168.1.50 répond

3. **Réponse ARP (Unicast)** :

   - PC-B (192.168.1.50) répond : "C'est moi, mon MAC est 00:1A:2B:3C:4D:5E"
   - Envoie directement à PC-A (unicast)

4. **Mise en cache** :
   - PC-A enregistre l'association dans sa table ARP
   - Valable quelques minutes (timeout)
   - Évite de refaire une requête ARP à chaque fois

**Commandes utiles :**

- `arp -a` : Afficher la table ARP
- `arp -d` : Vider la table ARP

**Table ARP exemple :**

```
Adresse IP        Adresse MAC         Type
192.168.1.1       00:11:22:33:44:55   dynamique
192.168.1.50      00:1A:2B:3C:4D:5E   dynamique
192.168.1.254     AA:BB:CC:DD:EE:FF   dynamique
```

#### Commutation Ethernet (Switching)

Un switch (commutateur) est un équipement de couche 2 qui connecte plusieurs équipements sur un réseau local.

**Différence Hub vs Switch :**

**Hub (répéteur multiport)** - Obsolète

- Couche 1 (physique)
- Envoie les données à tous les ports (broadcast)
- Domaine de collision partagé (risque de collisions)
- Inefficace et insécurisé

**Switch (commutateur)** - Standard moderne

- Couche 2 (liaison de données)
- Envoie les données uniquement au port de destination
- Domaine de collision par port
- Efficace et plus sécurisé

**Fonctionnement d'un switch :**

1. **Apprentissage (Learning)** :

   - Le switch construit une table MAC (CAM table)
   - Associe chaque adresse MAC au port correspondant
   - Apprend en observant l'adresse MAC source des trames reçues

2. **Transfert (Forwarding)** :

   - Quand une trame arrive, le switch consulte sa table MAC
   - Si le MAC de destination est connu : **forward** vers le port spécifique
   - Si le MAC de destination est inconnu : **flood** (envoie sur tous les ports sauf celui d'origine)

3. **Filtrage (Filtering)** :
   - Ne transfère pas les trames inutiles
   - Réduit le trafic réseau

**Table MAC (CAM table) exemple :**

```
Port    Adresse MAC         VLAN
Fa0/1   00:11:22:33:44:55   1
Fa0/2   AA:BB:CC:DD:EE:FF   1
Fa0/3   00:1A:2B:3C:4D:5E   1
Fa0/24  FF:EE:DD:CC:BB:AA   1
```

**Méthodes de commutation :**

1. **Store-and-Forward** (stockage et retransmission) :

   - Reçoit la trame complète
   - Vérifie le FCS (détection d'erreurs)
   - Puis retransmet si la trame est valide
   - Plus lent mais plus fiable

2. **Cut-Through** (à la volée) :

   - Commence à retransmettre dès réception de l'adresse MAC de destination
   - Plus rapide mais pas de vérification d'erreurs
   - Peut propager des trames corrompues

3. **Fragment-Free** :
   - Compromis : lit les 64 premiers octets
   - Détecte les collisions mais plus rapide que store-and-forward

#### Domaines de collision et de broadcast

**Domaine de collision :**

- Zone du réseau où les trames peuvent entrer en collision
- Hub : 1 domaine de collision pour tous les ports
- Switch : 1 domaine de collision par port

**Domaine de broadcast :**

- Zone où un broadcast est propagé
- Switch : 1 domaine de broadcast pour tout le switch (par défaut)
- Routeur : Sépare les domaines de broadcast

### Approche pédagogique

L'apprentissage combine théorie et manipulation pratique avec Packet Tracer. Vous découvrirez comment les données sont réellement transmises sur le réseau, du signal électrique ou optique jusqu'à la trame Ethernet.

**Exercices pratiques recommandés :**

- Construire un réseau simple avec switches et PC dans Packet Tracer
- Observer les trames Ethernet avec Wireshark
- Analyser les requêtes et réponses ARP
- Examiner la table MAC d'un switch
- Comparer les performances des différents supports (cuivre, fibre, Wi-Fi)
- Câbler physiquement un câble RJ45 selon les normes T568A/B

## Boucle III - Routage

### Objectifs d'apprentissage

À l'issue de cette boucle, vous serez capable de :

- Expliquer comment les routeurs utilisent les informations de la couche réseau pour diriger les paquets
- Comprendre le fonctionnement des tables de routage
- Configurer des routes statiques de base
- Analyser le processus de décision de routage
- Comprendre les bases du routage dynamique

### Qu'est-ce qu'un routeur ?

Un **routeur** est un équipement de couche 3 (réseau) qui interconnecte différents réseaux IP. Son rôle principal est de déterminer le meilleur chemin pour acheminer les paquets vers leur destination.

**Analogie :** Le routeur est comme un aiguilleur dans une gare qui dirige les trains (paquets) vers le bon quai (interface) en consultant l'horaire (table de routage).

**Différence Switch vs Routeur :**

| Critère              | Switch                | Routeur                   |
| -------------------- | --------------------- | ------------------------- |
| Couche OSI           | 2 (Liaison)           | 3 (Réseau)                |
| Adressage            | Adresses MAC          | Adresses IP               |
| Portée               | Réseau local (LAN)    | Interconnexion de réseaux |
| Domaine de broadcast | 1 seul                | Sépare les domaines       |
| Fonction             | Commutation de trames | Routage de paquets        |

### Fonctions principales d'un routeur

#### 1. Détermination du chemin (Path Determination)

Le routeur choisit le meilleur chemin vers la destination en consultant sa **table de routage**.

**Critères de décision :**

- **Correspondance la plus longue** (Longest Prefix Match) : Choisit la route la plus spécifique
- **Distance administrative** (AD) : Si plusieurs sources (statique, RIP, OSPF)
- **Métrique** : Si plusieurs chemins avec le même protocole

#### 2. Commutation de paquets (Packet Switching)

Le routeur transfère le paquet de l'interface d'entrée vers l'interface de sortie appropriée.

**Processus en 6 étapes :**

1. **Réception du paquet** sur une interface
2. **Décapsulation** : Retire l'en-tête de trame Ethernet (couche 2)
3. **Examen de l'IP de destination** dans l'en-tête IP
4. **Consultation de la table de routage** pour trouver la meilleure route
5. **Ré-encapsulation** : Crée une nouvelle trame pour l'interface de sortie
6. **Transmission** du paquet sur l'interface appropriée

**Important :** À chaque saut (hop), les adresses MAC changent, mais les adresses IP source et destination restent identiques.

### La table de routage

La table de routage est la "carte routière" du routeur. Elle contient toutes les routes connues vers les différents réseaux.

#### Commande pour afficher la table de routage

**Cisco IOS :**

```
Router# show ip route
```

#### Structure d'une entrée de route

Exemple d'entrée :

```
C    192.168.1.0/24 is directly connected, GigabitEthernet0/0
```

**Éléments d'une route :**

- **Code source** : Comment la route a été apprise (C, S, R, O, D, etc.)
- **Réseau de destination** : 192.168.1.0/24
- **Distance administrative / Métrique** : [AD/Métrique]
- **Next-hop** : Adresse IP du prochain routeur
- **Horodatage** : Depuis combien de temps la route existe
- **Interface de sortie** : Par quelle interface envoyer le paquet

#### Codes source des routes

| Code    | Signification | Description                                 |
| ------- | ------------- | ------------------------------------------- |
| **C**   | Connected     | Réseau directement connecté à une interface |
| **L**   | Local         | Adresse IP de l'interface elle-même         |
| **S**   | Static        | Route configurée manuellement               |
| **D**   | EIGRP         | Route apprise via EIGRP                     |
| **O**   | OSPF          | Route apprise via OSPF                      |
| **R**   | RIP           | Route apprise via RIP                       |
| **B**   | BGP           | Route apprise via BGP                       |
| **S\*** | Static        | Route statique candidate par défaut         |

#### Exemple de table de routage complète

```
Router# show ip route

Codes: C - connected, S - static, R - RIP, O - OSPF

Gateway of last resort is 10.0.0.1 to network 0.0.0.0

S*   0.0.0.0/0 [1/0] via 10.0.0.1                    ← Route par défaut
C    10.0.0.0/24 is directly connected, Gi0/0
L    10.0.0.2/32 is directly connected, Gi0/0
C    192.168.1.0/24 is directly connected, Gi0/1
L    192.168.1.1/32 is directly connected, Gi0/1
S    192.168.10.0/24 [1/0] via 10.0.0.5              ← Route statique
O    172.16.0.0/16 [110/20] via 10.0.0.3, Gi0/0     ← Route OSPF
```

### Routes statiques

Une **route statique** est une route configurée manuellement par l'administrateur. Elle ne change pas automatiquement.

#### Avantages des routes statiques

- Pas de charge CPU (pas de calcul)
- Pas de bande passante utilisée (pas d'échange de messages)
- Sécurité accrue (contrôle total)
- Prévisibilité du chemin

#### Inconvénients

- Configuration manuelle fastidieuse sur de grands réseaux
- Pas d'adaptation automatique aux pannes
- Maintenance complexe
- Ne scale pas (difficile pour des centaines de routes)

#### Configuration d'une route statique

**Syntaxe Cisco IOS :**

```
Router(config)# ip route réseau-destination masque {next-hop | interface-sortie} [distance-administrative]
```

**Exemples pratiques :**

1. **Route statique avec next-hop :**

```
Router(config)# ip route 192.168.10.0 255.255.255.0 10.0.0.5
```

→ Pour atteindre 192.168.10.0/24, envoyer les paquets à 10.0.0.5

2. **Route statique avec interface de sortie :**

```
Router(config)# ip route 192.168.20.0 255.255.255.0 Serial0/0/0
```

→ Pour atteindre 192.168.20.0/24, utiliser l'interface Serial0/0/0

3. **Route par défaut (Default Route) :**

```
Router(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.1
```

→ Tout trafic sans route spécifique va vers 10.0.0.1 (passerelle par défaut)
→ Équivalent à la "gateway of last resort"

4. **Route statique flottante (Backup) :**

```
Router(config)# ip route 192.168.10.0 255.255.255.0 10.0.0.6 210
```

→ Distance administrative de 210 (haute) : utilisée seulement si la route principale échoue

#### Route récapitulative (Summary Route)

Une route qui représente plusieurs sous-réseaux avec une seule entrée.

**Exemple :**
Au lieu de :

```
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
```

On peut créer une route récapitulative :

```
192.168.0.0/22  (regroupe les 4 sous-réseaux)
```

**Avantages :**

- Réduit la taille de la table de routage
- Diminue les ressources CPU et mémoire
- Améliore la stabilité (une panne d'un sous-réseau n'affecte pas la route récapitulative)

### Routage dynamique

Le **routage dynamique** utilise des protocoles qui permettent aux routeurs d'échanger automatiquement des informations sur les réseaux.

#### Protocoles de routage dynamique

##### 1. RIP (Routing Information Protocol)

**Caractéristiques :**

- Protocole à **vecteur de distance** (Distance Vector)
- Métrique : **Nombre de sauts (hop count)**
- Maximum : 15 sauts (16 = inaccessible)
- Mises à jour : Toutes les 30 secondes (broadcast complet)
- Convergence lente
- Simple mais obsolète pour les grands réseaux

**Versions :**

- **RIPv1** : Classful (pas de VLSM), broadcast
- **RIPv2** : Classless (VLSM), multicast, authentification

**Configuration RIPv2 :**

```
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 192.168.1.0
Router(config-router)# network 10.0.0.0
Router(config-router)# no auto-summary
```

##### 2. OSPF (Open Shortest Path First)

**Caractéristiques :**

- Protocole à **état de liens** (Link State)
- Métrique : **Coût** basé sur la bande passante
  - Coût = 10⁸ / Bande passante en bps
  - FastEthernet (100 Mbps) : Coût = 1
  - Ethernet (10 Mbps) : Coût = 10
- Convergence rapide
- Scalable (supporte de très grands réseaux)
- Utilise l'algorithme de Dijkstra (SPF - Shortest Path First)
- Mises à jour : Uniquement en cas de changement (pas périodiques)

**Concepts OSPF :**

**Areas (zones)** : Découpe hiérarchique du réseau

- **Area 0** : Backbone (obligatoire)
- **Areas normales** : Connectées à l'Area 0

**Routeurs OSPF :**

- **IR** (Internal Router) : Toutes les interfaces dans la même area
- **ABR** (Area Border Router) : Connecte plusieurs areas
- **ASBR** (Autonomous System Border Router) : Connecte OSPF à d'autres protocoles
- **Backbone Router** : Au moins une interface dans l'Area 0

**Configuration OSPF :**

```
Router(config)# router ospf 1
Router(config-router)# router-id 1.1.1.1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 10.0.0.0 0.255.255.255 area 0
Router(config-router)# passive-interface GigabitEthernet0/1
```

**Note :** Le masque dans OSPF est un **wildcard mask** (inverse du masque de sous-réseau)

- Masque : 255.255.255.0 → Wildcard : 0.0.0.255

##### 3. EIGRP (Enhanced Interior Gateway Routing Protocol)

**Caractéristiques :**

- Protocole hybride (Cisco propriétaire, devenu ouvert en 2013)
- Métrique composite : Bande passante + Délai (par défaut)
- Convergence très rapide
- Supporte VLSM et CIDR
- Mises à jour partielles et incrémentales
- Utilise l'algorithme DUAL (Diffusing Update Algorithm)

**Avantages :**

- Utilisation efficace de la bande passante
- Support du load balancing (répartition de charge)
- Facile à configurer
- Convergence plus rapide qu'OSPF dans certains cas

**Configuration EIGRP :**

```
Router(config)# router eigrp 100
Router(config-router)# network 192.168.1.0
Router(config-router)# network 10.0.0.0
Router(config-router)# no auto-summary
```

#### Distance administrative (AD)

La **distance administrative** est un indice de confiance (0-255) utilisé quand plusieurs protocoles proposent une route vers la même destination. **Plus la valeur est basse, plus la source est fiable.**

| Source              | Distance Administrative |
| ------------------- | ----------------------- |
| Interface connectée | 0                       |
| Route statique      | 1                       |
| EIGRP (résumé)      | 5                       |
| eBGP                | 20                      |
| EIGRP (interne)     | 90                      |
| OSPF                | 110                     |
| RIP                 | 120                     |
| EIGRP (externe)     | 170                     |
| iBGP                | 200                     |
| Route inconnue      | 255 (invalide)          |

**Exemple :**
Si un routeur reçoit une route vers 10.0.0.0/8 via :

- Route statique (AD = 1)
- OSPF (AD = 110)
- RIP (AD = 120)

→ Il choisira la **route statique** (AD la plus faible)

#### Métrique

La **métrique** est utilisée par un protocole de routage pour comparer plusieurs chemins vers la même destination **au sein du même protocole**.

| Protocole | Métrique                            |
| --------- | ----------------------------------- |
| RIP       | Nombre de sauts (hop count)         |
| OSPF      | Coût (basé sur bande passante)      |
| EIGRP     | Composite (bande passante + délai)  |
| BGP       | Attributs multiples (AS-Path, etc.) |

#### Convergence

La **convergence** est le processus par lequel tous les routeurs ont une vue cohérente et à jour de la topologie réseau.

**Temps de convergence :** Durée entre un changement (panne, nouveau lien) et la stabilisation complète des tables de routage.

**Facteurs affectant la convergence :**

- Fréquence des mises à jour
- Algorithme utilisé (Link State converge plus vite que Distance Vector)
- Taille du réseau
- Timers de protocole

### Dépannage du routage

#### Commandes essentielles

**Afficher la table de routage :**

```
Router# show ip route
```

**Afficher les protocoles de routage actifs :**

```
Router# show ip protocols
```

**Afficher les interfaces et leurs états :**

```
Router# show ip interface brief
```

**Tester la connectivité :**

```
Router# ping 192.168.10.1
Router# traceroute 192.168.10.1
```

**Afficher les voisins OSPF :**

```
Router# show ip ospf neighbor
```

**Afficher les voisins EIGRP :**

```
Router# show ip eigrp neighbors
```

#### Problèmes courants

1. **Pas de route vers la destination**

   - Vérifier que la route existe dans la table : `show ip route`
   - Configurer une route statique ou activer le routage dynamique

2. **Interface down**

   - Vérifier l'état : `show ip interface brief`
   - Activer l'interface : `no shutdown`

3. **Routes apprises mais pas utilisées**

   - Vérifier la distance administrative
   - Vérifier la métrique

4. **Boucles de routage**
   - Vérifier la configuration des routes statiques
   - S'assurer de la convergence du protocole dynamique

### Approche pédagogique

Cette boucle développe votre compréhension du fonctionnement des routeurs à travers des exercices de configuration progressifs. Vous apprendrez à diagnostiquer des problèmes de routage et à optimiser les chemins de communication.

**Exercices pratiques recommandés :**

- Configurer un réseau avec plusieurs routeurs dans Packet Tracer
- Implémenter des routes statiques et une route par défaut
- Observer la table de routage et comprendre chaque entrée
- Simuler une panne et observer l'impact sur le routage
- Configurer RIP, puis OSPF, et comparer les résultats
- Utiliser `traceroute` pour visualiser le chemin des paquets
- Créer des routes récapitulatives pour optimiser les tables de routage

## Boucle IV - Adressage IP

### Objectifs d'apprentissage

À l'issue de cette boucle, vous serez capable de :

- Calculer et attribuer des adresses IPv4 et IPv6
- Comprendre et appliquer les masques de sous-réseau
- Créer des schémas de sous-réseautage adaptés aux besoins
- Différencier les types d'adresses (unicast, multicast, broadcast)
- Préparer la transition vers IPv6

### Adressage IPv4

#### Structure d'une adresse IPv4

Une adresse IPv4 est un identifiant unique de **32 bits** écrit sous forme de **4 octets en notation décimale** séparés par des points.

**Format :** `xxx.xxx.xxx.xxx` où chaque xxx est un nombre entre 0 et 255

**Exemple :** `192.168.1.100`

**En binaire :** `11000000.10101000.00000001.01100100`

#### Composition d'une adresse IP

Chaque adresse IP contient deux parties :

1. **Partie réseau** : Identifie le réseau
2. **Partie hôte** : Identifie l'équipement sur ce réseau

Le **masque de sous-réseau** détermine quelle portion est le réseau et quelle portion est l'hôte.

#### Masque de sous-réseau

Le masque est aussi composé de 32 bits. Les bits à 1 indiquent la partie réseau, les bits à 0 la partie hôte.

**Exemple :**

```
Adresse IP   : 192.168.1.100
Masque       : 255.255.255.0
En binaire   :
IP           : 11000000.10101000.00000001.01100100
Masque       : 11111111.11111111.11111111.00000000
               └────── Réseau ──────┘└── Hôte ──┘
```

**Notation CIDR (Classless Inter-Domain Routing) :**
Au lieu de 255.255.255.0, on écrit `/24` (24 bits pour le réseau)
→ `192.168.1.100/24`

#### Classes d'adresses IPv4 (historique)

| Classe | Premier octet | Masque par défaut | CIDR | Nombre de réseaux      | Hôtes par réseau |
| ------ | ------------- | ----------------- | ---- | ---------------------- | ---------------- |
| A      | 1-126         | 255.0.0.0         | /8   | 126                    | 16 777 214       |
| B      | 128-191       | 255.255.0.0       | /16  | 16 384                 | 65 534           |
| C      | 192-223       | 255.255.255.0     | /24  | 2 097 152              | 254              |
| D      | 224-239       | -                 | -    | Multicast              | -                |
| E      | 240-255       | -                 | -    | Réservé (expérimental) | -                |

**Note :** 127.x.x.x est réservé pour le loopback (localhost)

**Aujourd'hui, on n'utilise plus les classes strictes, mais le CIDR qui permet un découpage plus flexible.**

#### Adresses IP spéciales

**Adresse réseau :** Tous les bits hôte à 0

- Exemple : `192.168.1.0/24`
- Identifie le réseau lui-même, pas assignable à un équipement

**Adresse de broadcast :** Tous les bits hôte à 1

- Exemple : `192.168.1.255/24`
- Message envoyé à tous les équipements du réseau, pas assignable

**Adresses privées (RFC 1918) :** Non routables sur Internet

| Classe | Plage privée                  | CIDR           | Nombre de réseaux |
| ------ | ----------------------------- | -------------- | ----------------- |
| A      | 10.0.0.0 - 10.255.255.255     | 10.0.0.0/8     | 1 réseau énorme   |
| B      | 172.16.0.0 - 172.31.255.255   | 172.16.0.0/12  | 16 réseaux        |
| C      | 192.168.0.0 - 192.168.255.255 | 192.168.0.0/16 | 256 réseaux       |

**Adresse de loopback :** 127.0.0.1

- Boucle locale, pour tester la pile TCP/IP de la machine

**APIPA (169.254.x.x) :** Attribution automatique quand DHCP échoue

#### Sous-réseautage (Subnetting)

Le sous-réseautage consiste à diviser un grand réseau en plusieurs sous-réseaux plus petits.

**Pourquoi faire du sous-réseautage ?**

- Réduire les domaines de broadcast (meilleure performance)
- Améliorer la sécurité (segmentation)
- Optimiser l'utilisation des adresses IP
- Organiser logiquement le réseau par départements/sites

**Méthode de calcul du sous-réseautage**

**Étape 1 : Identifier le besoin**

- Combien de sous-réseaux nécessaires ?
- Combien d'hôtes par sous-réseau ?

**Étape 2 : Emprunter des bits**
On emprunte des bits de la partie hôte pour créer des sous-réseaux.

**Formules :**

- **Nombre de sous-réseaux** = 2^n (où n = bits empruntés)
- **Nombre d'hôtes par sous-réseau** = 2^h - 2 (où h = bits hôte restants)
  - On soustrait 2 pour l'adresse réseau et broadcast

**Exemple pratique :**

**Problème :** Vous avez le réseau `192.168.1.0/24` et vous devez créer 4 sous-réseaux.

**Solution :**

1. **Calculer les bits nécessaires :**

   - 4 sous-réseaux → 2^n ≥ 4 → n = 2 bits

2. **Nouveau masque :**

   - Masque original : /24 (11111111.11111111.11111111.00000000)
   - On emprunte 2 bits : /26 (11111111.11111111.11111111.11000000)
   - Nouveau masque : 255.255.255.192

3. **Calculer l'incrément :**

   - 256 - 192 = 64
   - Chaque sous-réseau fait 64 adresses

4. **Les 4 sous-réseaux :**

| Sous-réseau | Adresse réseau   | Première IP utilisable | Dernière IP utilisable | Broadcast     |
| ----------- | ---------------- | ---------------------- | ---------------------- | ------------- |
| 1           | 192.168.1.0/26   | 192.168.1.1            | 192.168.1.62           | 192.168.1.63  |
| 2           | 192.168.1.64/26  | 192.168.1.65           | 192.168.1.126          | 192.168.1.127 |
| 3           | 192.168.1.128/26 | 192.168.1.129          | 192.168.1.190          | 192.168.1.191 |
| 4           | 192.168.1.192/26 | 192.168.1.193          | 192.168.1.254          | 192.168.1.255 |

Chaque sous-réseau contient **62 hôtes utilisables** (64 - 2).

#### Tableau de référence des masques

| CIDR | Masque          | Nombre d'hôtes | Utilisation typique   |
| ---- | --------------- | -------------- | --------------------- |
| /32  | 255.255.255.255 | 1              | Hôte unique           |
| /30  | 255.255.255.252 | 2              | Lien point-à-point    |
| /29  | 255.255.255.248 | 6              | Très petit réseau     |
| /28  | 255.255.255.240 | 14             | Petit sous-réseau     |
| /27  | 255.255.255.224 | 30             | Petit bureau          |
| /26  | 255.255.255.192 | 62             | Département           |
| /25  | 255.255.255.128 | 126            | Moyen réseau          |
| /24  | 255.255.255.0   | 254            | Réseau standard       |
| /23  | 255.255.254.0   | 510            | 2 réseaux de classe C |
| /22  | 255.255.252.0   | 1022           | 4 réseaux de classe C |
| /16  | 255.255.0.0     | 65 534         | Classe B complète     |
| /8   | 255.0.0.0       | 16 777 214     | Classe A complète     |

#### VLSM (Variable Length Subnet Mask)

VLSM permet d'utiliser différents masques de sous-réseau dans le même réseau pour optimiser l'utilisation des adresses.

**Exemple pratique :**

Vous devez créer un plan d'adressage à partir de `172.16.0.0/16` pour :

- 1 réseau de 1000 hôtes (siège social)
- 2 réseaux de 500 hôtes (succursales)
- 5 réseaux de 100 hôtes (agences)
- 10 liens point-à-point (2 hôtes chacun)

**Stratégie VLSM :** Commencer par le plus grand besoin

1. **Réseau de 1000 hôtes :**

   - 2^10 = 1024 hôtes → besoin de 10 bits hôte → /22
   - `172.16.0.0/22` (172.16.0.1 à 172.16.3.254)

2. **2 réseaux de 500 hôtes :**

   - 2^9 = 512 hôtes → besoin de 9 bits hôte → /23
   - `172.16.4.0/23` (172.16.4.1 à 172.16.5.254)
   - `172.16.6.0/23` (172.16.6.1 à 172.16.7.254)

3. **5 réseaux de 100 hôtes :**

   - 2^7 = 128 hôtes → besoin de 7 bits hôte → /25
   - `172.16.8.0/25`, `172.16.8.128/25`, `172.16.9.0/25`, etc.

4. **10 liens point-à-point :**
   - 2 hôtes → /30
   - `172.16.10.0/30`, `172.16.10.4/30`, `172.16.10.8/30`, etc.

#### NAT et PAT

**NAT (Network Address Translation) :** Traduit les adresses IP privées en adresses publiques.

**Pourquoi utiliser NAT ?**

- Conservation des adresses IPv4 publiques (épuisement)
- Sécurité (masque la topologie interne)
- Flexibilité (changer de FAI sans rechanger toutes les IP internes)

**Types de NAT :**

**NAT statique :** 1 IP privée ↔ 1 IP publique (mapping fixe)

```
192.168.1.10 (privée) ↔ 203.0.113.10 (publique)
```

**NAT dynamique :** Pool d'IP publiques partagées

```
192.168.1.x (privées) ↔ Pool 203.0.113.10-20 (publiques)
```

**PAT (Port Address Translation) ou NAT Overload :** Plusieurs IP privées ↔ 1 IP publique (utilise les ports)

```
192.168.1.10:5000 → 203.0.113.5:10000
192.168.1.11:5001 → 203.0.113.5:10001
192.168.1.12:5002 → 203.0.113.5:10002
```

**C'est le type le plus utilisé (votre box internet à la maison).**

### Adressage IPv6

IPv6 a été créé pour résoudre l'épuisement des adresses IPv4.

#### Différences IPv4 vs IPv6

| Caractéristique   | IPv4                | IPv6                         |
| ----------------- | ------------------- | ---------------------------- |
| Taille d'adresse  | 32 bits             | 128 bits                     |
| Notation          | Décimale pointée    | Hexadécimale avec :          |
| Nombre d'adresses | ~4,3 milliards      | 340 sextillions              |
| Broadcast         | Oui                 | Non (remplacé par multicast) |
| Fragmentation     | Routeurs et hôtes   | Hôtes uniquement             |
| En-tête           | Variable (options)  | Fixe (simplifié)             |
| Configuration     | Manuelle ou DHCP    | Auto-configuration (SLAAC)   |
| Sécurité          | Optionnelle (IPsec) | Intégrée (IPsec obligatoire) |

#### Structure d'une adresse IPv6

**Format :** 128 bits divisés en **8 groupes de 16 bits** (en hexadécimal)

**Exemple complet :**

```
2001:0DB8:0000:0042:0000:0000:0000:1234
```

**Règles d'abréviation :**

1. **Supprimer les zéros de tête dans chaque groupe :**

   ```
   2001:DB8:0:42:0:0:0:1234
   ```

2. **Remplacer une séquence de groupes de zéros par :: (une seule fois) :**
   ```
   2001:DB8:0:42::1234
   ```

**Autres exemples :**

```
Complet  : 2001:0DB8:0000:0000:0000:0000:0000:0001
Abrégé   : 2001:DB8::1

Complet  : FE80:0000:0000:0000:0202:B3FF:FE1E:8329
Abrégé   : FE80::202:B3FF:FE1E:8329
```

**Préfixe IPv6 :**
Comme le masque en IPv4, indique la partie réseau.

```
2001:DB8:ACAD:1::/64
```

→ Les 64 premiers bits = réseau, les 64 derniers = interface

#### Types d'adresses IPv6

**1. Unicast :** Une seule destination

- **Global Unicast (2000::/3)** : Équivalent des IP publiques IPv4, routable sur Internet

  - Exemple : `2001:DB8:ACAD:1::10/64`

- **Link-Local (FE80::/10)** : Communication sur le lien local uniquement, non routable

  - Exemple : `FE80::1`
  - Auto-configurée automatiquement sur chaque interface

- **Unique Local (FC00::/7)** : Équivalent des IP privées IPv4

  - Exemple : `FD00:1234:5678::1`

- **Loopback** : `::1` (équivalent de 127.0.0.1)

- **Unspecified** : `::` (0.0.0.0 en IPv4)

**2. Multicast (FF00::/8)** : Un-vers-plusieurs

- `FF02::1` : Tous les nœuds du lien local
- `FF02::2` : Tous les routeurs du lien local

**3. Anycast :** Adresse attribuée à plusieurs interfaces, le paquet va au plus proche

#### Configuration IPv6

**SLAAC (Stateless Address Autoconfiguration) :**
L'hôte génère automatiquement son adresse IPv6 à partir du préfixe annoncé par le routeur.

**Processus :**

1. Routeur annonce le préfixe du réseau (ex: `2001:DB8:ACAD:1::/64`)
2. L'hôte génère l'identifiant d'interface (EUI-64 ou aléatoire)
3. L'hôte combine : préfixe + identifiant = adresse complète

**DHCPv6 :** Attribution centralisée (comme DHCP en IPv4)

**Double pile (Dual Stack) :** IPv4 et IPv6 fonctionnent simultanément sur le même équipement

### Approche pédagogique

L'accent est mis sur la pratique intensive du calcul de sous-réseaux à travers des exercices variés. Vous développerez une aisance dans la manipulation des adresses IP, compétence fondamentale pour tout administrateur réseau.

**Exercices pratiques recommandés :**

- Pratiquer le sous-réseautage avec différents scénarios (4, 8, 16 sous-réseaux)
- Créer un plan d'adressage VLSM complet pour une entreprise fictive
- Convertir des adresses IPv6 complètes en format abrégé et vice-versa
- Identifier le réseau, la première IP utilisable, la dernière IP utilisable et le broadcast
- Utiliser un calculateur IP en ligne pour vérifier vos calculs
- Configurer NAT/PAT sur un routeur dans Packet Tracer
- Configurer IPv6 SLAAC et DHCPv6 sur un réseau

## Boucle VII - Réseau local (LAN)

### Objectifs d'apprentissage

À l'issue de cette boucle, vous serez capable de :

- Concevoir et implémenter des VLANs pour segmenter un réseau
- Configurer le protocole Spanning Tree pour prévenir les boucles
- Comprendre et utiliser l'agrégation de liens (EtherChannel)
- Mettre en œuvre la communication inter-VLAN
- Appliquer les bonnes pratiques de sécurisation des commutateurs

### Les VLANs (Virtual Local Area Networks)

#### Qu'est-ce qu'un VLAN ?

Un **VLAN** est un réseau local virtuel qui segmente logiquement un réseau physique. Plusieurs VLANs peuvent coexister sur le même switch.

**Analogie :** Imaginez un immeuble avec plusieurs appartements. Chaque appartement (VLAN) est isolé des autres, même s'ils partagent le même bâtiment (switch).

#### Pourquoi utiliser des VLANs ?

**Avantages :**

- **Segmentation logique** : Grouper les utilisateurs par fonction (comptabilité, RH, IT) indépendamment de leur emplacement physique
- **Sécurité** : Isolation du trafic entre départements
- **Performance** : Réduction des domaines de broadcast
- **Flexibilité** : Déplacer un utilisateur de VLAN sans recâbler
- **Gestion simplifiée** : Organisation logique du réseau

**Problème sans VLAN :**
Tous les équipements sur un switch partagent le même domaine de broadcast → Surcharge réseau et risques de sécurité.

**Solution avec VLAN :**
Chaque VLAN = 1 domaine de broadcast séparé → Trafic isolé.

#### Types de VLANs

**VLAN par défaut (VLAN 1) :**

- Présent sur tous les switches Cisco
- Tous les ports y sont affectés par défaut
- Ne peut pas être supprimé
- Utilisé pour le trafic de gestion (à éviter pour la sécurité)

**VLAN de données :** Trafic utilisateur normal (VLAN 10, 20, 30, etc.)

**VLAN natif :** Sur un trunk, trafic non-taggé (par défaut VLAN 1)

**VLAN de gestion :** Pour administrer le switch à distance (SSH, Telnet)

**VLAN voix :** Spécialisé pour la VoIP (téléphonie IP)

#### Configuration des VLANs

**Créer un VLAN :**

```cisco
Switch(config)# vlan 10
Switch(config-vlan)# name COMPTABILITE
Switch(config-vlan)# exit

Switch(config)# vlan 20
Switch(config-vlan)# name RESSOURCES_HUMAINES
Switch(config-vlan)# exit
```

**Affecter un port à un VLAN (mode access) :**

```cisco
Switch(config)# interface fastethernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
```

**Vérifier la configuration :**

```cisco
Switch# show vlan brief
Switch# show interfaces trunk
```

#### Trunk (Liaison trunk)

Un **trunk** est un lien entre switches qui transporte le trafic de plusieurs VLANs simultanément.

**Port access vs Port trunk :**

| Critère           | Access                  | Trunk           |
| ----------------- | ----------------------- | --------------- |
| Connexion         | PC, imprimante, serveur | Switch à switch |
| VLANs transportés | 1 seul VLAN             | Plusieurs VLANs |
| Tagging           | Pas de tag              | Tags 802.1Q     |

**Protocole de tagging : 802.1Q**

802.1Q ajoute un **tag de 4 octets** dans la trame Ethernet pour identifier le VLAN.

```
Trame normale   : [MAC dest][MAC src][Type][Données][FCS]
Trame 802.1Q    : [MAC dest][MAC src][TAG 802.1Q][Type][Données][FCS]
                                       └─ VLAN ID ─┘
```

**Configuration d'un trunk :**

```cisco
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk native vlan 99
Switch(config-if)# switchport trunk allowed vlan 10,20,30
Switch(config-if)# exit
```

**VLAN natif :**
Le VLAN natif transporte le trafic non-taggé sur un trunk.

- Par défaut : VLAN 1
- **Bonne pratique** : Changer pour un VLAN inutilisé (ex: VLAN 99) pour des raisons de sécurité

#### VTP (VLAN Trunking Protocol)

VTP permet de synchroniser automatiquement la configuration des VLANs entre plusieurs switches.

**Modes VTP :**

**Server (Serveur) :**

- Peut créer, modifier, supprimer des VLANs
- Propage les modifications aux autres switches
- Sauvegarde la config VLAN en NVRAM

**Client :**

- Reçoit les mises à jour VTP
- Ne peut pas créer/modifier les VLANs localement
- Ne sauvegarde pas en NVRAM

**Transparent :**

- Ne participe pas à VTP
- Transmet les messages VTP mais ne les applique pas
- Peut créer des VLANs locaux
- Sauvegarde en NVRAM

**Configuration VTP :**

```cisco
Switch(config)# vtp mode server
Switch(config)# vtp domain ENTREPRISE
Switch(config)# vtp password secret123
Switch(config)# vtp version 2
```

**Attention :** VTP peut propager des suppressions de VLANs ! Précautions nécessaires.

### Routage inter-VLAN

**Problème :** Les VLANs sont isolés. Comment faire communiquer VLAN 10 avec VLAN 20 ?

**Solution :** Routage inter-VLAN (couche 3)

#### Méthode 1 : Router-on-a-Stick

Un routeur avec **une seule interface physique** divisée en **sous-interfaces logiques**, une par VLAN.

**Configuration du routeur :**

```cisco
Router(config)# interface gigabitethernet 0/0
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface gigabitethernet 0/0.10
Router(config-subif)# encapsulation dot1q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit

Router(config)# interface gigabitethernet 0/0.20
Router(config-subif)# encapsulation dot1q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit
```

**Configuration du switch :**

```cisco
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
```

**Avantages :** Peu coûteux, utilise un seul port physique

**Inconvénients :** Goulet d'étranglement (une seule interface), pas scalable

#### Méthode 2 : Switch multicouche (Layer 3 Switch)

Un switch capable de faire du routage (couche 3).

**Configuration :**

```cisco
Switch(config)# ip routing

Switch(config)# interface vlan 10
Switch(config-if)# ip address 192.168.10.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

Switch(config)# interface vlan 20
Switch(config-if)# ip address 192.168.20.1 255.255.255.0
Switch(config-if)# no shutdown
```

**Avantages :** Performances élevées, scalable, pas de goulet d'étranglement

**Inconvénients :** Plus coûteux qu'un switch de couche 2

### Spanning Tree Protocol (STP)

#### Problème : Les boucles de commutation

**Scénario :** Vous connectez 3 switches en triangle pour la redondance.

**Problème :** Sans STP, une trame broadcast boucle infiniment :

1. **Tempête de broadcast** : Saturation du réseau
2. **Instabilité de la table MAC** : Le switch ne sait plus sur quel port est l'équipement
3. **Copies multiples** : Les trames sont dupliquées à l'infini

**Solution : STP bloque certains ports** pour créer une topologie sans boucle tout en conservant la redondance.

#### Fonctionnement de STP

**1. Élection du pont racine (Root Bridge)**

Le switch avec le **Bridge ID le plus bas** devient le pont racine.

**Bridge ID = Priorité (2 octets) + Adresse MAC (6 octets)**

- Priorité par défaut : 32768
- Plus le Bridge ID est bas, mieux c'est

**Forcer un switch à devenir root :**

```cisco
Switch(config)# spanning-tree vlan 1 priority 4096
```

**Valeurs possibles :** Multiples de 4096 (0, 4096, 8192, 16384, 24576, 32768, etc.)

**2. Calcul du coût vers le root**

Chaque port calcule son **coût** pour atteindre le pont racine.

| Vitesse  | Coût STP (802.1D) | Coût RSTP (802.1w) |
| -------- | ----------------- | ------------------ |
| 10 Mbps  | 100               | 2 000 000          |
| 100 Mbps | 19                | 200 000            |
| 1 Gbps   | 4                 | 20 000             |
| 10 Gbps  | 2                 | 2 000              |

**3. États des ports STP**

| État           | Description                                  | Durée  |
| -------------- | -------------------------------------------- | ------ |
| **Disabled**   | Port désactivé administrativement            | -      |
| **Blocking**   | Reçoit des BPDU, ne transfère pas de données | 20 sec |
| **Listening**  | Reçoit et envoie des BPDU, ne transfère pas  | 15 sec |
| **Learning**   | Apprend les adresses MAC                     | 15 sec |
| **Forwarding** | Transfère normalement le trafic              | -      |

**Temps de convergence STP classique (802.1D) :** 30-50 secondes

**4. Rôles des ports**

- **Root Port (RP)** : Meilleur chemin vers le pont racine (1 par switch non-root)
- **Designated Port (DP)** : Port actif qui transfère le trafic vers un segment
- **Blocked Port** : Port bloqué pour éviter les boucles

#### Variantes de STP

**PVST+ (Per-VLAN Spanning Tree Plus) - Cisco propriétaire**

- Une instance STP par VLAN
- Permet de balancer la charge entre VLANs

**RSTP (Rapid Spanning Tree Protocol - 802.1w)**

- Convergence rapide : 2-3 secondes (au lieu de 30-50)
- États simplifiés : Discarding, Learning, Forwarding
- Types de ports : Edge, Root, etc.

**Configuration RSTP :**

```cisco
Switch(config)# spanning-tree mode rapid-pvst
```

#### PortFast et BPDU Guard

**PortFast :** Ports connectés à des PC (pas de boucle possible) passent directement en Forwarding

```cisco
Switch(config)# interface fastethernet 0/1
Switch(config-if)# spanning-tree portfast
```

**BPDU Guard :** Désactive le port si un BPDU est reçu (protection contre les boucles accidentelles)

```cisco
Switch(config-if)# spanning-tree bpduguard enable
```

### EtherChannel (Agrégation de liens)

#### Qu'est-ce qu'EtherChannel ?

Combine plusieurs liens physiques en un seul **lien logique** pour augmenter la bande passante et la redondance.

**Exemple :** 4 liens à 1 Gbps = 1 EtherChannel à 4 Gbps

**Avantages :**

- **Bande passante accrue** : Somme des liens
- **Redondance** : Si un lien tombe, les autres prennent le relais
- **Load balancing** : Répartition du trafic
- **Pas de boucle STP** : STP voit l'EtherChannel comme un seul lien

#### Protocoles d'agrégation

**PAgP (Port Aggregation Protocol) - Cisco propriétaire**

Modes :

- **On** : Force l'EtherChannel sans négociation (dangereux)
- **Desirable** : Initie la négociation
- **Auto** : Passif, attend la négociation

**LACP (Link Aggregation Control Protocol - 802.3ad) - Standard**

Modes :

- **On** : Force sans négociation
- **Active** : Initie la négociation
- **Passive** : Attend la négociation

**Recommandation :** Utiliser **LACP** (standard ouvert)

#### Configuration EtherChannel

**Avec LACP :**

```cisco
Switch(config)# interface range fastethernet 0/1-4
Switch(config-if-range)# channel-group 1 mode active
Switch(config-if-range)# exit

Switch(config)# interface port-channel 1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20,30
```

**Vérification :**

```cisco
Switch# show etherchannel summary
Switch# show etherchannel port-channel
```

**Règles importantes :**

- Tous les ports doivent avoir la **même vitesse et duplex**
- Tous les ports doivent être dans le **même mode** (access ou trunk)
- Tous les ports doivent être dans le **même VLAN** (si mode access)

### Sécurité LAN

#### Port Security

Limite le nombre d'adresses MAC autorisées sur un port et définit des actions en cas de violation.

**Configuration :**

```cisco
Switch(config)# interface fastethernet 0/5
Switch(config-if)# switchport mode access
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 2
Switch(config-if)# switchport port-security mac-address sticky
Switch(config-if)# switchport port-security violation shutdown
```

**Actions en cas de violation :**

- **Protect** : Ignore les trames des MAC non-autorisées
- **Restrict** : Ignore + log + compteur d'erreur
- **Shutdown** : Désactive le port (err-disabled)

**Réactiver un port err-disabled :**

```cisco
Switch(config)# interface fastethernet 0/5
Switch(config-if)# shutdown
Switch(config-if)# no shutdown
```

#### DHCP Snooping

Protège contre les serveurs DHCP malveillants (rogue DHCP).

**Fonctionnement :**

- Ports **trusted** : Peuvent envoyer des réponses DHCP (serveur légitime, uplink)
- Ports **untrusted** : Ne peuvent que faire des requêtes DHCP

**Configuration :**

```cisco
Switch(config)# ip dhcp snooping
Switch(config)# ip dhcp snooping vlan 10,20
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# ip dhcp snooping trust
```

#### Dynamic ARP Inspection (DAI)

Protège contre les attaques ARP spoofing (empoisonnement ARP).

**Utilise la table DHCP Snooping** pour valider les correspondances IP-MAC.

```cisco
Switch(config)# ip arp inspection vlan 10,20
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# ip arp inspection trust
```

### Approche pédagogique

Cette boucle se concentre sur la conception de réseaux locaux robustes et évolutifs. Les laboratoires Packet Tracer vous permettent de simuler des topologies complexes et d'observer l'impact de vos configurations.

**Exercices pratiques recommandés :**

- Créer une topologie avec 3 switches et configurer 3 VLANs
- Configurer un trunk entre switches et vérifier le tagging 802.1Q
- Implémenter le routage inter-VLAN avec router-on-a-stick
- Créer une boucle physique et observer STP bloquer un port
- Configurer un EtherChannel avec LACP entre 2 switches
- Appliquer port security et tester une violation
- Simuler une attaque DHCP rogue et configurer DHCP snooping

## Boucle X - Résolution de nom

### Objectifs d'apprentissage

À l'issue de cette boucle, vous serez capable de :

- Expliquer le fonctionnement du système DNS (Domain Name System)
- Configurer des services DNS sur un réseau
- Comprendre le processus de résolution de noms hiérarchique
- Analyser les requêtes DNS et identifier les problèmes courants
- Différencier les types d'enregistrements DNS

### Qu'est-ce que le DNS ?

**DNS (Domain Name System)** est le "annuaire téléphonique" d'Internet. Il traduit les noms de domaine lisibles par l'humain (comme www.google.com) en adresses IP compréhensibles par les machines (comme 142.250.185.78).

**Analogie :** C'est comme un répertoire de contacts sur votre téléphone. Au lieu de mémoriser le numéro "06 12 34 56 78", vous cherchez "Marie" et votre téléphone compose automatiquement.

#### Pourquoi le DNS est-il nécessaire ?

**Problème :** Les ordinateurs communiquent avec des adresses IP (ex: 172.217.14.206), mais nous préférons retenir des noms (www.example.com).

**Solution :** DNS fait la traduction automatiquement.

**Sans DNS :**

- Vous devriez mémoriser 142.250.185.78 pour accéder à Google
- Impossible de retenir les milliards d'adresses IP sur Internet

**Avec DNS :**

- Vous tapez www.google.com
- DNS trouve automatiquement l'IP correspondante
- Votre navigateur se connecte à cette IP

### Structure hiérarchique du DNS

Le DNS est organisé en **arbre inversé** avec plusieurs niveaux.

```
                        . (root)
                        /    |    \
                      /      |      \
                   com      org      fr
                  /   \      |       / \
               google amazon   |    gouv paris
                /       |      |
              www      mail   www
```

#### Niveaux de domaine

**1. Domaine racine (Root) : `.`**

- Au sommet de la hiérarchie
- 13 serveurs racine dans le monde (A-M)
- Connaissent les serveurs de tous les TLD

**2. Domaines de premier niveau (TLD - Top-Level Domain)**

**TLD génériques (gTLD) :**

- `.com` : Commercial
- `.org` : Organisation
- `.net` : Réseau
- `.edu` : Éducation
- `.gov` : Gouvernement américain
- `.info`, `.biz`, `.tech`, etc.

**TLD géographiques (ccTLD - Country Code) :**

- `.fr` : France
- `.uk` : Royaume-Uni
- `.ca` : Canada
- `.de` : Allemagne
- `.jp` : Japon

**3. Domaines de deuxième niveau**

- `google` dans google.com
- `microsoft` dans microsoft.com
- `wikipedia` dans wikipedia.org

**4. Sous-domaines**

- `www` dans www.google.com
- `mail` dans mail.google.com
- `drive` dans drive.google.com

**Exemple complet : www.shop.amazon.com**

```
www.shop.amazon.com.
└─┬─┘└┬─┘└──┬──┘└┬┘└─ Root (point final implicite)
  │   │     │    └──── TLD (.com)
  │   │     └───────── Domaine de 2e niveau (amazon)
  │   └─────────────── Sous-domaine (shop)
  └─────────────────── Hôte (www)
```

### Types d'enregistrements DNS

Les enregistrements DNS (Resource Records - RR) stockent différentes informations.

#### Enregistrements principaux

**A (Address) - IPv4**

- Associe un nom de domaine à une adresse IPv4

```
www.example.com.    IN    A    192.168.1.100
```

**AAAA (Address IPv6)**

- Associe un nom de domaine à une adresse IPv6

```
www.example.com.    IN    AAAA    2001:DB8::1
```

**CNAME (Canonical Name) - Alias**

- Crée un alias vers un autre nom de domaine
- Utile pour pointer plusieurs noms vers la même IP

```
blog.example.com.    IN    CNAME    www.example.com.
```

→ blog.example.com pointe vers www.example.com

**MX (Mail Exchange) - Serveur mail**

- Indique les serveurs de messagerie pour le domaine
- Priorité : Plus le nombre est bas, plus prioritaire

```
example.com.    IN    MX    10    mail1.example.com.
example.com.    IN    MX    20    mail2.example.com.
```

**PTR (Pointer) - Résolution inverse**

- Associe une adresse IP à un nom de domaine (inverse de A)
- Utilisé pour la résolution inverse (reverse DNS)

```
100.1.168.192.in-addr.arpa.    IN    PTR    www.example.com.
```

**NS (Name Server) - Serveur de noms**

- Indique les serveurs DNS autoritaires pour la zone

```
example.com.    IN    NS    ns1.example.com.
example.com.    IN    NS    ns2.example.com.
```

**SOA (Start of Authority)**

- Premier enregistrement d'une zone DNS
- Contient des informations sur la zone (numéro de série, timers, etc.)

```
example.com.    IN    SOA    ns1.example.com. admin.example.com. (
                               2024010101  ; Serial
                               3600        ; Refresh
                               1800        ; Retry
                               604800      ; Expire
                               86400 )     ; Minimum TTL
```

**TXT (Text) - Texte libre**

- Stocke du texte arbitraire
- Utilisé pour SPF (anti-spam), DKIM, vérification de domaine

```
example.com.    IN    TXT    "v=spf1 mx -all"
```

### Processus de résolution DNS

#### Résolution récursive

Le client DNS (votre ordinateur) demande au serveur DNS de faire tout le travail.

**Exemple : Vous tapez www.google.com**

1. **Client → Résolveur DNS local** (souvent votre FAI)

   - "Quelle est l'IP de www.google.com ?"

2. **Résolveur → Serveur racine**

   - "Où trouver .com ?"
   - Racine répond : "Demande aux serveurs .com"

3. **Résolveur → Serveur TLD .com**

   - "Où trouver google.com ?"
   - TLD répond : "Demande aux serveurs NS de google.com"

4. **Résolveur → Serveur NS google.com**

   - "Quelle est l'IP de www.google.com ?"
   - NS répond : "142.250.185.78"

5. **Résolveur → Client**
   - "Voici l'IP : 142.250.185.78"

**Le client a fait 1 seule requête, mais le résolveur en a fait 4 (récursion).**

#### Résolution itérative

Le serveur DNS renvoie la meilleure réponse qu'il connaît, sans faire le travail complet.

**Chaque serveur dit :** "Je ne sais pas, mais demande à celui-ci."

#### Cache DNS

Pour améliorer les performances, les résolveurs DNS **mettent en cache** les résultats.

**TTL (Time To Live) :** Durée de validité du cache (en secondes)

```
www.example.com.    3600    IN    A    192.168.1.100
                    └─┬─┘
                   TTL = 1 heure
```

**Avantages :**

- Réduit le trafic réseau
- Accélère les résolutions suivantes
- Diminue la charge sur les serveurs DNS

**Inconvénients :**

- Propagation lente des changements
- Si vous changez l'IP, le cache doit expirer

**Vider le cache DNS local (Windows) :**

```
ipconfig /flushdns
```

**Vider le cache DNS local (Linux) :**

```
sudo systemd-resolve --flush-caches
```

### Configuration DNS

#### Configuration client

**Windows :**

```
ipconfig /all
```

→ Affiche les serveurs DNS configurés

**Linux :**

```
cat /etc/resolv.conf
```

**Exemple de fichier resolv.conf :**

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

#### Serveurs DNS publics courants

| Fournisseur | DNS Primaire   | DNS Secondaire  |
| ----------- | -------------- | --------------- |
| Google      | 8.8.8.8        | 8.8.4.4         |
| Cloudflare  | 1.1.1.1        | 1.0.0.1         |
| OpenDNS     | 208.67.222.222 | 208.67.220.220  |
| Quad9       | 9.9.9.9        | 149.112.112.112 |

#### DNS primaire vs secondaire

**Serveur DNS primaire (Master) :**

- Contient la copie originale (autoritaire) des données de zone
- Toutes les modifications se font ici
- Notifie les serveurs secondaires des changements

**Serveur DNS secondaire (Slave) :**

- Copie en lecture seule des données de zone
- Obtient les données via **transfert de zone** depuis le primaire
- Redondance en cas de panne du primaire
- Répartition de charge

**Transfert de zone :**

- **AXFR** (Full Zone Transfer) : Transfert complet de la zone
- **IXFR** (Incremental Zone Transfer) : Transfert des changements uniquement

### Dépannage DNS

#### Commande nslookup

Interroge les serveurs DNS pour résoudre un nom.

**Utilisation basique :**

```
nslookup www.google.com
```

**Sortie :**

```
Server:  8.8.8.8
Address: 8.8.8.8#53

Non-authoritative answer:
Name:    www.google.com
Address: 142.250.185.78
```

**Interroger un serveur DNS spécifique :**

```
nslookup www.google.com 1.1.1.1
```

**Requête sur un type d'enregistrement spécifique :**

```
nslookup -type=MX google.com
nslookup -type=NS google.com
nslookup -type=AAAA www.google.com
```

#### Commande dig (Linux/Mac)

Outil plus avancé pour diagnostiquer DNS.

**Utilisation basique :**

```
dig www.google.com
```

**Requête courte :**

```
dig www.google.com +short
```

**Interroger un type spécifique :**

```
dig MX google.com
dig NS google.com
dig AAAA www.google.com
```

**Tracer le chemin complet de résolution :**

```
dig www.google.com +trace
```

**Interroger un serveur spécifique :**

```
dig @8.8.8.8 www.google.com
```

#### Commande host

Commande simple pour résolution rapide.

```
host www.google.com
host 142.250.185.78    (résolution inverse)
```

#### Problèmes courants

**1. Serveur DNS ne répond pas**

- Vérifier la connectivité réseau
- Tester avec un autre serveur DNS (ex: 8.8.8.8)
- Vérifier le pare-feu (port 53 UDP/TCP)

**2. Nom de domaine ne résout pas**

- Vérifier que le domaine existe : `nslookup example.com`
- Vider le cache DNS local : `ipconfig /flushdns`
- Vérifier le fichier hosts (`C:\Windows\System32\drivers\etc\hosts`)

**3. Résolution lente**

- DNS primaire inaccessible, timeout avant basculement sur secondaire
- Changer l'ordre des serveurs DNS
- Utiliser des serveurs DNS plus rapides (Cloudflare 1.1.1.1)

**4. Résultats incohérents**

- Cache DNS périmé
- Propagation DNS en cours (après un changement)
- Différents serveurs DNS donnent des résultats différents

#### Fichier hosts

Fichier local qui court-circuite le DNS.

**Emplacement :**

- Windows : `C:\Windows\System32\drivers\etc\hosts`
- Linux/Mac : `/etc/hosts`

**Format :**

```
127.0.0.1       localhost
192.168.1.100   serveur.local
192.168.1.50    imprimante.local
```

**Utilité :**

- Tests locaux avant propagation DNS
- Bloquer des sites (rediriger vers 127.0.0.1)
- Noms locaux pour équipements sans DNS

**Priorité :** Le fichier hosts est consulté **avant** le DNS.

### DHCP et DNS

DHCP et DNS travaillent souvent ensemble.

**DHCP (Dynamic Host Configuration Protocol) :**

- Attribue automatiquement des adresses IP aux clients
- Fournit aussi l'adresse du serveur DNS
- Option 6 (DNS Server)

**DNS dynamique (DDNS) :**

- Met à jour automatiquement le DNS quand DHCP attribue une IP
- Utile pour les équipements dont l'IP change

**Exemple :** Votre ordinateur obtient 192.168.1.50 via DHCP
→ DDNS crée/met à jour l'enregistrement : `pc-jean.entreprise.local → 192.168.1.50`

### Approche pédagogique

Vous découvrirez comment les noms de domaine se transforment en adresses IP, mécanisme invisible mais essentiel à l'expérience utilisateur. Les exercices pratiques vous familiariseront avec les outils d'analyse DNS.

**Exercices pratiques recommandés :**

- Utiliser `nslookup` pour résoudre différents types d'enregistrements (A, MX, NS)
- Comparer les temps de réponse de différents serveurs DNS publics
- Tracer une résolution DNS complète avec `dig +trace`
- Configurer un serveur DNS dans Packet Tracer
- Modifier le fichier hosts pour créer des alias locaux
- Analyser une capture Wireshark d'une requête DNS (port 53 UDP)
- Simuler une panne du DNS primaire et observer le basculement vers le secondaire
- Mesurer l'impact du cache DNS sur les temps de résolution