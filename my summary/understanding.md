# RESEAU PREPARATIONS 

# Introduction et fondamentaux de Reseaux :
## 1.1. Definitions et concepts de base : 

### Qu'est un reseau information : 

* **Réseau** : ensemble d’entités ou de nœuds interconnectés afin de permettre des échanges ou des interactions entre eux.

* **Réseau informatique** : ensemble de dispositifs informatiques (ordinateurs, serveurs, smartphones, imprimantes, etc.) interconnectés par des moyens de communication, permettant d’échanger des données et de partager des ressources.

### Topologies physiques et logiques (Etoile,Bus,Anneau,Maille) : 
![alt text](images/image.png)
- topologie physique : decrit la maniere dontt les equipements d'un reseau sont physiquement connectes entre eux(cables,commutateurs,etc..) 
- topologie logique : decrit la maniere dont les donnees circulent entre les equipements du reseau,independamment de leur position physique.
<br>

***Principales topologies** : 
- Etoile  : tous les equipements sont relies a un equipement central, generalement un switch ou un hub 
- Bus : tous les equipements sont connectes a un meme cable principal, appele bus, qui sert de support de transmission partage 
- Anneau: chaque equipement est connecte a deux equipements voisins, formant une boucle fermee dans laquelle les donnees circulent 
- maillee(mesh) : les equipements sont relie entre eux par plusieurs liaisons, offrant plusieurs chemins possibles pour transmettre les donnees. 

### Typologies selon la couverture geographique : 
- PAN (Personal area network) : reseau de tres courte portee, generalement autour d'une personne, permetant de connecter des appareils personnels 
- LAN (Local Area Network) : reseau couvrant une zone geographique limitee, comme une maison un bureau un laboratoire ou un batiment. 
- MAN(Metropolitan Area Network) : reseau couvrantt une zone geographique plus etendue qu'un LAN, generalement a l'echelle d'une ville ou d'une agglomeration. 
- WAN(Wide Area Network) : reseau couvrant une tres grande zone geographique,pouvant relier des reseaux situes dans differentes villes, regions ou pays 
### Modes de transmission : Simplex, Half-Duplex, Full-Duplex. 
- Simplex : La transmission des donnees se fait dans un seul sens. Un equipement emet et l'autre recoit, sans possibilite de reponse sur le meme canal. 
- Half-Duplex : la transmission peut se faire dans les deux sens mais pas simultanement. Les equipements doivent alterner entre emission et reception 
- Full Duplex : la transmission peut se faire dans les deux sens simultanement. Les deux equipements peuvent emettre et recevoir en meme temps
### Modes de diffusion : Unicast, Broadcast, Multicast, Anycast. 
- Unicast : un emetteur envoie des donnees a un seul destinataire 
- Broadcast : un emetteur envoie des donnees a tous les equipements du reseau local 
- Multicast : un emetteur envoie des donnees a un groupe specifique de destinataires qui ont rejoint le groupe multicast 
- Anycast : un emetteur envoie des donnees a un seul destinataire parmi plusieurs equipements partageant la meme adresse Anycast, generalement celui qui est considere comme le plus proche selon le protocole de routage.
 
 ## 1.2 Architecture et materiels d'interconnexion : 
### Équipements de couche 1 : Répéteur, Hub (Concentrateur).
les equipements de couche 1 (physique) du modele OSI agissent principalement sur la transmission des signaux electriques, optiques ou radio, sans analuser les adresses reseau ou les trames. 
- Repeteur(Repeater) : equipement qui regenere et retransmet un signal afin d'augmenter la distance de transmission et de compenser son affaiblissement. Il ne filtre pas les donnees et ne prend pas de decision sur leur destination 
- Hub(Concentrateur) : equipement qui recoit un signal sur un portt et le repere sur tous les autres ports. Tous les equioements connectes partagent donc le meme domaine de collision. Le hub fonctionne au niveau physique(couche 1). 

### Équipements de couche 2 : Commutateur (Switch), Pont (Bridge).
Les equipements de couche 2(liaison de donnees) du modele OSI utilisent principalement les adresses MAC pour acheminer les trames au sein d'un reseau local. 
- commutateur (Switch) : equipement qui recoit les trames et les transmet uniquement vers le port correspondant au destinataire, en utilisant sa table d'adresses MAC, Il permet de reduire les collisions et de segmenter le reseau
- Pont(Bridges) : equipement qui relie deux segments de reseau et filtre les trames en fonction des adresses MAC. Il permet de determiner si une trame doit etre transferee d'un segmentt a l'autre. 

### Équipements de couche 3 : Routeur, Switch Niveau 3.
les equipements de couche 3 (reseau) du modele OSI utilisent principalement les adresses IP pour acheminer les paquets entre differents reseaux.
- Routeur : equipement qui relie plusieurs reseaux differents et achemine les paquets IP vers leur reseau de destination. Il utilise une table de routage pour determiner le meilleur chemin. 
- Switch de niveau 3(layer 3 switch) : commutateur capable d'effectuer des fonctions de routage IP, en plus de ses fonctions classiques de commutation de couche 2. Il permet notamment permettre la communication entre differents VLANs.

### Notions de Domaine de collision et Domaine de diffusion (Broadcast). 

- Domaine de collision (Collision Domain) : partie d'un reseau dans laquelle plusieurs equipements peuvent emettre des donnees simultanement, ce qui peut provoquer une collision lorsque le reseau utilise un mecanisme de partage du support comme l'Ethernet half-duplex.
    - Hub : tous les ports appartiennet au meme domaine de collision
    - switch : chaque port constitue generalementt un domaine de collision distinct 

- Domaine de diffusion(Broadcast domain) : ensemble des equipements qui recoivent une trame de broadcast envoyee sur le reseau 
    - Hub/Switch : un broadcast est generalement transmis a tous les equipements du meme reseau local/VLAN
    - routeur: separe les domaines de broadcast et ne transmet generalement pas les broadcasts d'un reseau IP a un autre. 
- A retenir : 
    - Hub - meme domaine de collision 
    - Switch - separe les domaines de collision  
    - Routeur - separe les domaines de broadcast 

# 2. Les Modèles d'Architecture (OSI et TCP/IP) 
## 2.1. Le modèle théorique OSI (7 couches)
### 2.1.1. Couche 1 : Physique (Bits, signaux, câblage) : 

la couche physique est la premiere couche d modele OSI. Elle assure la transmission des bits(0 et 1) sous forme de signaux a travers un support de communication 
- unite de donnees : bit 
- role : transmettre les bits d'un equipement a un autre 
- elements concernes : signaux electriques, optiques ou radio,cables,connecteurs,frequences et niveaux de signal. 
- exemples de supports : cable ethernet,fibre optique, ondes radio 
- equipements associes: repeteur  et hub 

<br> 
A retenir : la couche physique s'occupe de la maniere dont les bits sont transmis, mais ne s'occupe pas de leur signification ni de leur destination 

### 2.1.2. Couche 2 : Liaison de données (Trames, adresses MAC). 
La couche liaison de donnees assure la communication entre deux equipements directement connectes su un meme reseau. Elle organise les bits recus de la couche physique en trames et utilise les adresses MAC pour identifier les equipements
- Unite de donnees : trames(frames) 
- Role : assurer une transmission fiable des trames entre equipements directement connectes et controler l'acces au support de transmission
- adressage : adresse MAC
- fonctions principales : 
    - encapsulation des donees en trames
    - identification des equipements avec les adresses MAC
    - detection des erreurs de transmission
    - controle de l'acces au support 
- equipements associes : switch(commutateur) et bridge(pont) 

- a retenit : la couche 2 s'occupe principalement de la communication locale entre equipements en utilisant les trames et les adresses MAC

###  2.1.3. Couche 3 : Réseau (Paquets, adresses IP, routage).
la couche reseau assure l'acheminement des donnees entre differents reseaux. Elle utilise les adresses IP pour identifier les reseaux et les equipements, puis determine le chemin que les paquets doivent suivre jusqu'a leur destination. 
- unite de donnees: paquet 
- role : acheminer les paquets d'un reseau source vers un reseau de destination 
- adressage : adresse IP(IPv4 ou IPv6) 
- fonctions principales : 
    - attribution et utilisation des adresses IP 
    - Routage des paquets entre differents reseaux 
    - Determination du chemin vers la destination
    - transmission des paquets d'un routeur a un autre
- Equipement principal : routeur(Router) 

- A retenir : la couche 3 s'occupe principalement de l'adressage IP et du routage des paquets entre les reseaux. 

###  2.1.4. Couche 4 : Transport

La **couche transport** assure la communication **de bout en bout entre les applications** exécutées sur deux équipements. Elle contrôle la transmission des données et peut assurer leur fiabilité selon le protocole utilisé.

* **Unité de données :** segment pour **TCP** ; datagramme pour **UDP**.

* **Rôle :** assurer la transmission des données entre les applications source et destination.

* **Adressage :** **numéros de port**, qui permettent d’identifier les applications ou services.

* **Principales fonctions :**

  * **Segmentation** des données et réassemblage à la destination.
  * Identification des applications grâce aux **ports**.
  * **Contrôle de flux** pour éviter qu’un émetteur n’envoie des données plus rapidement que le récepteur ne peut les traiter.
  * **Contrôle des erreurs et retransmission** avec TCP.
  * Gestion de la connexion avec TCP ; UDP fonctionne sans connexion.

* **Protocoles principaux :** **TCP** et **UDP**.

**À retenir :** la couche 4 s’occupe de la communication **entre les applications**, en utilisant notamment les **ports**, la segmentation et le contrôle de la transmission.

### 2.1.5. Couche 5 : Session

La **couche session** assure l’**établissement, la gestion et la terminaison des sessions de communication** entre deux applications. Elle permet de maintenir et de contrôler le dialogue pendant l’échange de données.

* **Rôle :** gérer les sessions de communication entre les applications.
* **Fonctions principales :**

  * **Établissement** d’une session.
  * **Maintien et gestion** du dialogue entre les applications.
  * **Synchronisation** des échanges de données.
  * **Terminaison** de la session.
  * Possibilité de définir des **points de reprise** en cas d’interruption.

**À retenir :** la couche 5 s’occupe de **la gestion du dialogue entre les applications**, du début jusqu’à la fin de la session.

### 2.1.6. Couche 6 : Présentation

La **couche présentation** assure la représentation et la transformation des données afin que les applications puissent les comprendre et les échanger dans un format compatible.

* **Rôle :** assurer la compatibilité des formats de données entre les applications.
* **Fonctions principales :**

  * **Formatage et conversion** des données entre différents formats.
  * **Chiffrement et déchiffrement** des données.
  * **Compression et décompression** des données.
  * Gestion de la représentation des caractères, par exemple ASCII et Unicode.

**À retenir :** la couche 6 s’occupe de la **représentation, du chiffrement et de la compression des données** pour permettre leur échange entre les applications.

### 2.1.7. Couche 7 : Application

La **couche application** est la couche la plus proche de l’utilisateur. Elle fournit aux applications les **services réseau** nécessaires pour communiquer avec d’autres applications ou systèmes.

* **Rôle :** fournir des services réseau directement utilisés par les applications.
* **Fonctions principales :**

  * Permettre aux applications d’accéder aux **services réseau**.
  * Gérer les échanges entre les applications et les services du réseau.
  * Fournir des protocoles adaptés aux différents besoins de communication.
* **Exemples de protocoles :**

  * **HTTP / HTTPS** : navigation Web.
  * **DNS** : résolution des noms de domaine.
  * **FTP** : transfert de fichiers.
  * **SMTP** : envoi d’e-mails.
  * **SSH** : accès distant sécurisé.

**À retenir :** la couche 7 fournit les **services réseau utilisés par les applications**, comme le Web, le DNS, le transfert de fichiers ou la messagerie.

## 2.2. Le modèle pratique TCP/IP (4 ou 5 couches)

### 2.2.1. Couche Accès Réseau

La **couche Accès Réseau** est la couche la plus basse du modèle TCP/IP. Elle regroupe les fonctions des **couches Physique et Liaison de données du modèle OSI**. Elle permet la transmission des données sur le réseau local en utilisant les supports et technologies d’accès au réseau.

* **Correspondance OSI :** couches **1 (Physique) + 2 (Liaison de données)**.
* **Unité de données :** trame au niveau liaison, puis **bits** au niveau physique.
* **Rôle :** assurer la transmission des données sur le **support physique** et leur acheminement sur le réseau local.
* **Fonctions principales :**

  * Transmission des **bits** sous forme de signaux.
  * Encapsulation des données en **trames**.
  * Utilisation des **adresses MAC**.
  * Contrôle de l’accès au support de transmission.
  * Détection de certaines erreurs de transmission.
* **Exemples de technologies :** Ethernet, Wi-Fi.
* **Équipements associés :** switch, hub, répéteur, carte réseau.

**À retenir :** la couche Accès Réseau regroupe les fonctions des couches **1 et 2 du modèle OSI** et permet aux données de circuler sur le **réseau local et le support physique**.

### 2.2.2. Couche Internet

La **couche Internet** du modèle TCP/IP assure l’**adressage logique** et l’**acheminement des paquets entre différents réseaux**. Elle correspond principalement à la **couche Réseau (couche 3) du modèle OSI**.

* **Correspondance OSI :** couche **3 (Réseau)**.
* **Unité de données :** **paquet (Packet)**.
* **Rôle :** permettre aux paquets de circuler d’un réseau source vers un réseau de destination.
* **Adressage :** **adresses IP** (IPv4 ou IPv6).
* **Fonctions principales :**

  * Attribution et utilisation des **adresses IP**.
  * **Routage** des paquets entre les réseaux.
  * Détermination du chemin vers la destination.
  * Transmission des paquets entre les différents routeurs.
* **Protocoles principaux :** **IP (IPv4/IPv6), ICMP**.

**À retenir :** la couche Internet s’occupe principalement de **l’adressage IP et du routage des paquets entre les réseaux**.

### 2.2.3. Couche Transport

La **couche Transport** assure la communication **de bout en bout entre les applications** exécutées sur deux équipements. Elle contrôle la transmission des données et utilise les **numéros de port** pour identifier les applications concernées.

* **Correspondance OSI :** couche **4 (Transport)**.
* **Unité de données :** **segment** pour TCP ; **datagramme** pour UDP.
* **Rôle :** assurer la communication entre les applications source et destination.
* **Adressage :** **numéros de port**.
* **Fonctions principales :**

  * **Segmentation** et réassemblage des données.
  * Identification des applications grâce aux **ports**.
  * **Contrôle de flux**.
  * **Contrôle des erreurs et retransmission** avec TCP.
  * Gestion d’une communication **avec connexion (TCP)** ou **sans connexion (UDP)**.
* **Protocoles principaux :** **TCP** et **UDP**.

**À retenir :** la couche Transport assure la communication **de bout en bout entre les applications**, notamment grâce aux **ports, à la segmentation et au contrôle de la transmission**.

### 2.2.4. Couche Application

La **couche Application** est la couche la plus proche de l’utilisateur dans le modèle TCP/IP. Elle regroupe les fonctions des **couches Session, Présentation et Application du modèle OSI** et fournit les services réseau directement utilisés par les applications.

* **Correspondance OSI :** couches **5 (Session) + 6 (Présentation) + 7 (Application)**.
* **Rôle :** fournir aux applications les **services et protocoles nécessaires à la communication sur le réseau**.
* **Fonctions principales :**

  * Établissement et gestion des échanges entre les applications.
  * **Formatage, chiffrement et compression** des données selon les protocoles utilisés.
  * Accès aux différents **services réseau**.
* **Protocoles principaux :**

  * **HTTP / HTTPS** : communication Web.
  * **DNS** : résolution des noms de domaine.
  * **FTP** : transfert de fichiers.
  * **SMTP** : envoi d’e-mails.
  * **SSH** : accès distant sécurisé.

**À retenir :** la couche Application regroupe les fonctions des **couches 5, 6 et 7 du modèle OSI** et fournit les **services réseau directement utilisés par les applications**.
## 2.3. Mécanisme fondamental : Encapsulation et Désencapsulation

L’**encapsulation** est le processus par lequel chaque couche du modèle réseau **ajoute ses propres informations de contrôle**, généralement sous forme d’**en-tête (header)**, aux données reçues de la couche supérieure.

La **désencapsulation** est le processus inverse : à la réception, chaque couche **analyse puis retire les informations qui lui sont destinées** avant de transmettre les données à la couche supérieure.

### Encapsulation

Lorsqu’une application envoie des données, celles-ci descendent à travers les couches du modèle :

**Donnée → Segment → Paquet → Trame → Bits**

* **Couche Application :** données.
* **Couche Transport :** ajout de l’en-tête TCP ou UDP → **segment** (TCP) / **datagramme** (UDP).
* **Couche Réseau :** ajout de l’en-tête IP → **paquet**.
* **Couche Liaison :** ajout d’un en-tête et généralement d’une remorque (*trailer*) → **trame**.
* **Couche Physique :** transformation de la trame en **bits** transmis sous forme de signaux.

### Désencapsulation

À la réception, le processus s’effectue dans le sens inverse :

**Bits → Trame → Paquet → Segment → Donnée**

Chaque couche traite les informations qui lui sont destinées, puis transmet le contenu restant à la couche supérieure.

**À retenir :**

> **Encapsulation :** on ajoute des informations en descendant les couches.
> **Désencapsulation :** on retire ces informations en remontant les couches.

**PDU (Protocol Data Unit)** désigne l’unité de données traitée par une couche donnée :

* **Application → Données**
* **Transport → Segment / Datagramme**
* **Réseau → Paquet**
* **Liaison → Trame**
* **Physique → Bits**

# 3. La Couche Liaison de Données (Couche 2)

La **couche Liaison de données** est la **couche 2 du modèle OSI**.

Elle assure principalement la transmission des données entre des équipements directement connectés sur un même réseau local.

Ses principales fonctions sont :

* l'encapsulation des données en **trames (Frames)** ;
* l'adressage physique avec les **adresses MAC** ;
* le contrôle d'accès au support ;
* la détection de certaines erreurs de transmission ;
* la commutation des trames par les switches ;
* la segmentation logique du réseau avec les VLANs.

---

# 3.1. Normes et protocole Ethernet (IEEE 802.3)

**Ethernet** est une technologie de réseau local (LAN) largement utilisée pour les réseaux filaires.

La norme Ethernet est définie principalement par la famille **IEEE 802.3**.

Lorsqu'un paquet provenant de la couche réseau arrive à la couche liaison, Ethernet l'encapsule dans une **trame Ethernet**.

## Format d'une trame Ethernet

Une trame Ethernet classique contient notamment :

```text
+----------+----------+----------+------+-------------+------+
| Préambule| MAC Dest.| MAC Source| Type |   Données   | FCS  |
+----------+----------+----------+------+-------------+------+
```

### Principaux champs

| Champ               | Rôle                                                     |
| ------------------- | -------------------------------------------------------- |
| **Préambule**       | Synchronisation entre l'émetteur et le récepteur         |
| **MAC Destination** | Adresse MAC du destinataire                              |
| **MAC Source**      | Adresse MAC de l'émetteur                                |
| **EtherType**       | Indique le protocole encapsulé, par exemple IPv4 ou IPv6 |
| **Données**         | Données transportées par la trame                        |
| **FCS**             | Détection d'erreurs à l'aide d'un contrôle d'intégrité   |

Dans une trame Ethernet II, le champ **EtherType** permet par exemple d'identifier :

```text
0x0800 → IPv4
0x86DD → IPv6
0x0806 → ARP
```

### Taille de la trame Ethernet

Une trame Ethernet classique possède généralement :

* une taille minimale de **64 octets** ;
* une taille maximale de **1518 octets**, hors préambule et SFD, pour une trame Ethernet II sans VLAN.

Avec un tag **802.1Q**, la taille maximale augmente de 4 octets.

---

## Mécanisme d'accès au support

Lorsque plusieurs équipements partagent le même support physique, il faut définir comment ils peuvent accéder au réseau.

### CSMA/CD

**CSMA/CD** signifie :

> **Carrier Sense Multiple Access with Collision Detection**

Le principe est :

1. l'équipement écoute le support ;
2. s'il semble libre, il transmet ;
3. si deux équipements transmettent simultanément, une **collision** peut se produire ;
4. les équipements détectent la collision ;
5. ils arrêtent leur transmission et attendent un délai aléatoire avant de réessayer.

Ce mécanisme était utilisé avec les réseaux Ethernet partagés et les connexions **half-duplex**.

### Important

Dans les réseaux Ethernet modernes utilisant des **switches en full-duplex**, les collisions ne se produisent normalement pas.

**CSMA/CD n'est donc plus utilisé dans le fonctionnement normal d'un réseau Ethernet commuté full-duplex.**

---

### CSMA/CA

**CSMA/CA** signifie :

> **Carrier Sense Multiple Access with Collision Avoidance**

Il est principalement associé aux réseaux **Wi-Fi IEEE 802.11**.

Le principe consiste à essayer d'**éviter les collisions** plutôt que de les détecter après transmission.

De manière simplifiée :

1. la station écoute le canal ;
2. si le canal est libre, elle peut transmettre selon les mécanismes définis par 802.11 ;
3. elle utilise notamment des mécanismes d'attente aléatoire ;
4. une confirmation (**ACK**) permet généralement de confirmer la réception.

Le Wi-Fi utilise l'évitement des collisions car une station sans fil ne peut pas toujours détecter une collision pendant qu'elle transmet.

---

# 3.2. Adressage Physique (Adresse MAC)

Une **adresse MAC (Media Access Control)** identifie une interface réseau au niveau de la couche liaison.

Une adresse MAC classique possède **48 bits**, soit **6 octets**.

Elle est généralement représentée sous forme hexadécimale :

```text
00:1A:2B:3C:4D:5E
```

## Structure d'une adresse MAC

Traditionnellement, les 24 premiers bits correspondent à l'identifiant attribué au fabricant (**OUI — Organizationally Unique Identifier**).

Les 24 bits suivants identifient l'interface dans l'espace attribué.

```text
48 bits
+------------------------+------------------------+
|          OUI           | Identifiant interface |
|        24 bits         |       24 bits         |
+------------------------+------------------------+
```

Cependant, toutes les adresses MAC ne doivent pas être interprétées simplement comme « fabricant + numéro de carte » : certaines adresses peuvent être **localement administrées** ou utilisées pour des besoins particuliers.

---

## Adresse MAC unicast, multicast et broadcast

Une adresse MAC peut notamment être utilisée pour :

### Unicast

Communication vers une interface précise :

```text
00:1A:2B:3C:4D:5E
```

### Broadcast

Communication vers tous les équipements du réseau local :

```text
FF:FF:FF:FF:FF:FF
```

### Multicast

Communication vers un groupe d'équipements.

---

# Table MAC d'un switch

Un **switch** utilise une table MAC pour savoir sur quel port envoyer une trame.

Exemple :

```text
+-------------------+------+
| Adresse MAC       | Port |
+-------------------+------+
| AA:AA:AA:AA:AA:AA |  1   |
| BB:BB:BB:BB:BB:BB |  2   |
| CC:CC:CC:CC:CC:CC |  3   |
+-------------------+------+
```

Cette table est construite dynamiquement grâce au processus d'apprentissage.

## 1. Learning — Apprentissage

Lorsqu'un switch reçoit une trame, il examine principalement **l'adresse MAC source**.

Exemple :

```text
MAC source = AA:AA:AA:AA:AA:AA
Port = 1
```

Le switch apprend :

```text
AA:AA:AA:AA:AA:AA → Port 1
```

La table MAC est donc construite progressivement.

---

## 2. Forwarding — Commutation

Supposons que le switch reçoive une trame :

```text
Source      : AA:AA:AA:AA:AA:AA
Destination : BB:BB:BB:BB:BB:BB
```

Si sa table contient :

```text
BB:BB:BB:BB:BB:BB → Port 2
```

le switch transmet la trame uniquement vers le **port 2**.

Cela évite d'envoyer inutilement la trame sur les autres ports.

---

## 3. Flooding — Inondation

Si l'adresse MAC de destination est inconnue du switch, celui-ci peut transmettre la trame sur plusieurs ports du même domaine de broadcast, à l'exception du port sur lequel la trame a été reçue.

```text
             +---------+
             |  Switch |
             +---------+
              /   |   \
             /    |    \
            PC1   PC2   PC3
```

Si le switch ne connaît pas la destination, il effectue un **flooding**.

Lorsque le destinataire répond, le switch peut apprendre son adresse MAC et son port.

---

# 3.3. Protocole ARP (Address Resolution Protocol)

**ARP (Address Resolution Protocol)** permet d'obtenir l'adresse **MAC correspondant à une adresse IPv4** sur un réseau local.

Il réalise donc une résolution :

```text
Adresse IPv4 → Adresse MAC
```

Exemple :

```text
IP : 192.168.1.20
          ↓ ARP
MAC : AA:BB:CC:DD:EE:FF
```

ARP est utilisé avec **IPv4**. IPv6 utilise principalement **Neighbor Discovery Protocol (NDP)** à la place d'ARP.

---

## Fonctionnement d'ARP

Supposons que PC1 souhaite communiquer avec :

```text
IP destination = 192.168.1.20
```

mais qu'il ne connaisse pas encore la MAC correspondante.

### Étape 1 — Consultation de la table ARP

PC1 vérifie d'abord son cache/table ARP.

```text
IP                  MAC
---------------------------------
192.168.1.10        AA:AA:AA:AA:AA:AA
192.168.1.20        ?
```

Si aucune entrée n'existe, PC1 doit envoyer une requête ARP.

---

### Étape 2 — ARP Request

PC1 envoie une requête ARP en **broadcast** :

```text
Qui possède 192.168.1.20 ?
Répondez à 192.168.1.10.
```

La trame Ethernet est envoyée vers :

```text
FF:FF:FF:FF:FF:FF
```

Tous les équipements du même domaine de broadcast reçoivent la requête.

---

### Étape 3 — ARP Reply

L'équipement possédant l'adresse :

```text
192.168.1.20
```

répond avec sa MAC.

La réponse ARP est généralement envoyée en **unicast** vers l'émetteur de la requête.

```text
192.168.1.20
      ↓
MAC = BB:BB:BB:BB:BB:BB
```

---

### Étape 4 — Mise à jour de la table ARP

PC1 enregistre l'association :

```text
192.168.1.20 → BB:BB:BB:BB:BB:BB
```

Il peut ensuite construire une trame Ethernet destinée à cette adresse MAC.

### Résumé

```text
PC1
 |
 | ARP Request
 | "Qui possède 192.168.1.20 ?"
 |          Broadcast
 ↓
Switch
 |
 +-------> PC2
           |
           | ARP Reply
           | "192.168.1.20 = BB:BB:BB:..."
           |          Unicast
           ↓
          PC1
```

### Attention : ARP ne traverse pas les routeurs

ARP fonctionne sur le **réseau local**.

Lorsqu'un ordinateur veut communiquer avec une machine située sur un autre réseau IP, il ne cherche généralement pas la MAC de la machine distante. Il cherche la MAC de sa **passerelle par défaut**.

Exemple :

```text
PC
 |
 | Destination : réseau distant
 ↓
Routeur / Passerelle
 |
 ↓
Réseau distant
```

---

# 3.4. Commutation avancée

## 3.4.1. VLANs (IEEE 802.1Q)

Un **VLAN (Virtual Local Area Network)** permet de créer plusieurs réseaux logiques indépendants sur une même infrastructure physique de commutation.

Sans VLAN :

```text
              Switch
          /      |      \
        PC1     PC2     PC3
```

Avec des VLANs :

```text
              Switch
          /      |      \
        PC1     PC2     PC3
        VLAN 10 VLAN 20 VLAN 10
```

PC1 et PC3 appartiennent au même VLAN logique même s'ils ne sont pas nécessairement connectés à des ports physiquement adjacents.

### Pourquoi utiliser des VLANs ?

Les VLANs permettent notamment :

* de segmenter un réseau ;
* de séparer différents services ;
* de réduire les domaines de broadcast ;
* d'améliorer l'organisation et l'isolation du réseau ;
* de faciliter l'administration.

Exemple :

```text
VLAN 10 → Administration
VLAN 20 → Développement
VLAN 30 → Invités
```

---

## Ports Access

Un **port Access** appartient généralement à **un seul VLAN**.

Il est utilisé pour connecter des équipements terminaux tels que :

* ordinateurs ;
* imprimantes ;
* téléphones IP selon la configuration ;
* certains serveurs.

Exemple :

```text
PC1
 |
 | VLAN 10
 |
Port Access
 |
Switch
```

La trame envoyée par le PC n'a généralement pas de tag VLAN 802.1Q sur ce lien terminal.

---

## Ports Trunk

Un **port Trunk** permet de transporter le trafic de **plusieurs VLANs** sur une même liaison.

Il est notamment utilisé entre :

* deux switches ;
* un switch et un routeur ;
* un switch et certains équipements réseau.

Exemple :

```text
Switch A                         Switch B
+---------+                    +---------+
| VLAN 10 |====================| VLAN 10 |
| VLAN 20 |   Port Trunk       | VLAN 20 |
| VLAN 30 |====================| VLAN 30 |
+---------+                    +---------+
```

---

## Tagging IEEE 802.1Q

Le standard **IEEE 802.1Q** permet d'ajouter une information de VLAN dans la trame Ethernet.

Le tag contient notamment le **VLAN ID**.

Conceptuellement :

```text
+------+--------+--------+---------+------+
| MAC  | MAC    | 802.1Q | Données | FCS  |
| Dest.| Source |  Tag   |         |      |
+------+--------+--------+---------+------+
```

Le **VLAN ID** permet au switch de savoir à quel VLAN appartient la trame.

### Exemple

```text
VLAN 10 → VLAN ID = 10
VLAN 20 → VLAN ID = 20
VLAN 30 → VLAN ID = 30
```

---

# 3.4.2. STP — Spanning Tree Protocol

**STP (Spanning Tree Protocol)** est un protocole permettant d'éviter les **boucles de niveau 2** dans un réseau commuté.

Il est historiquement défini par **IEEE 802.1D**.

## Pourquoi les boucles sont-elles problématiques ?

Supposons trois switches connectés de manière redondante :

```text
       Switch A
       /      \
      /        \
 Switch B ---- Switch C
```

Cette architecture fournit de la redondance, mais elle crée également une boucle de niveau 2.

Une trame broadcast pourrait circuler indéfiniment :

```text
A → B → C → A → B → C → ...
```

Les conséquences peuvent être importantes :

* multiplication des trames ;
* instabilité des tables MAC ;
* saturation du réseau ;
* **broadcast storm**.

---

## Principe de STP

STP construit une **topologie logique sans boucle**, tout en conservant physiquement les liens redondants.

Il élit un **Root Bridge** puis détermine quels ports doivent transmettre et lesquels doivent être bloqués afin d'éviter les boucles.

Conceptuellement :

```text
       Switch A
      Root Bridge
       /      \
      /        \
     ↓          ↓
 Switch B ---- Switch C
              X
          lien bloqué
```

Le lien physique existe toujours, mais STP empêche son utilisation normale tant qu'il n'est pas nécessaire.

Si un autre lien tombe, STP peut permettre à la topologie de se réorganiser.

---

## Élection du Root Bridge

Les switches échangent des **BPDU (Bridge Protocol Data Units)**.

Le Root Bridge est élu sur la base du **Bridge ID**, qui comprend notamment :

* une priorité ;
* une adresse MAC.

Le switch possédant le **Bridge ID le plus faible** est élu Root Bridge.

---

## États des ports dans STP classique

Dans le STP IEEE 802.1D traditionnel, un port peut passer par plusieurs états :

```text
Blocking
   ↓
Listening
   ↓
Learning
   ↓
Forwarding
```

Il existe également l'état :

```text
Disabled
```

### Blocking

Le port ne transmet pas normalement les trames de données afin d'éviter les boucles, mais participe aux mécanismes STP.

### Listening

Le switch détermine la topologie et participe aux calculs STP.

### Learning

Le switch commence à apprendre les adresses MAC, sans encore transmettre normalement les trames de données.

### Forwarding

Le port transmet normalement les trames et apprend les adresses MAC.

### Versions modernes

Le STP classique peut converger relativement lentement. Des variantes ont donc été développées, notamment :

* **RSTP (Rapid Spanning Tree Protocol)** — IEEE 802.1w ;
* **MSTP (Multiple Spanning Tree Protocol)** — IEEE 802.1s.

Elles permettent notamment une convergence plus rapide ou une gestion plus efficace de plusieurs VLANs selon l'architecture.

---

## À retenir

| Concept         | Rôle                                                                 |
| --------------- | -------------------------------------------------------------------- |
| **Ethernet**    | Technologie de réseau local filaire                                  |
| **Trame**       | Unité de données de la couche 2                                      |
| **MAC**         | Adresse physique/logique de niveau 2 d'une interface                 |
| **Switch**      | Transmet les trames en fonction des adresses MAC                     |
| **Learning**    | Apprentissage MAC à partir de l'adresse source                       |
| **Forwarding**  | Transmission vers le port connu du destinataire                      |
| **Flooding**    | Diffusion lorsque la destination est inconnue ou en broadcast        |
| **ARP**         | Résolution IPv4 → MAC sur le réseau local                            |
| **VLAN**        | Segmentation logique d'un réseau                                     |
| **Access**      | Port associé à un VLAN pour un équipement terminal                   |
| **Trunk**       | Liaison transportant plusieurs VLANs                                 |
| **802.1Q**      | Standard de tagging VLAN                                             |
| **STP**         | Prévention des boucles de niveau 2                                   |
| **Root Bridge** | Switch de référence dans la topologie STP                            |
| **BPDU**        | Trames utilisées par STP pour échanger des informations de topologie |

### Points essentiels

* La couche 2 travaille principalement avec les **trames** et les **adresses MAC**.
* Un switch apprend les adresses MAC en observant les **adresses source** des trames reçues.
* **ARP** permet de trouver la MAC associée à une IPv4 sur le réseau local.
* **VLAN** permet de segmenter logiquement un réseau physique.
* Un port **Access** transporte généralement un seul VLAN, tandis qu'un **Trunk** peut en transporter plusieurs.
* **STP** empêche les boucles de niveau 2 en bloquant certains chemins redondants.
* **CSMA/CD** est associé aux anciens réseaux Ethernet partagés/half-duplex ; l'Ethernet moderne commuté en full-duplex n'en a normalement plus besoin.
* **CSMA/CA** est utilisé par les réseaux Wi-Fi pour réduire le risque de collisions.
# 4. La Couche Réseau (Couche 3) - Adressage et Routage

La **couche Réseau** est la **couche 3 du modèle OSI**.

Elle permet principalement :

* l'adressage logique des équipements ;
* l'acheminement des paquets entre différents réseaux ;
* la sélection des chemins ;
* le routage ;
* la fragmentation dans certains cas avec IPv4.

Les principaux protocoles associés sont notamment **IPv4, IPv6, ICMP** et les protocoles de routage tels que **RIP, OSPF et BGP**.

---

# 4.1. Adressage IPv4

## 4.1.1. Structure d'une adresse IPv4

Une adresse **IPv4** est codée sur **32 bits**, soit **4 octets**.

Elle est généralement représentée sous forme décimale pointée :

```text
192.168.1.10
```

Chaque octet peut prendre une valeur comprise entre :

```text
0 et 255
```

Exemple :

```text
192     .     168     .     1     .     10
 ↓            ↓             ↓          ↓
8 bits       8 bits        8 bits     8 bits

              = 32 bits
```

Une adresse IPv4 contient conceptuellement deux parties :

```text
+----------------------+----------------+
| Partie réseau        | Partie hôte    |
+----------------------+----------------+
```

La séparation entre ces deux parties est déterminée par le **masque de sous-réseau** ou le **préfixe CIDR**.

---

# 4.1.2. Classes historiques et adresses privées

Avant l'utilisation généralisée du **CIDR**, les adresses IPv4 étaient réparties en classes.

## Classes IPv4

| Classe | Premier octet | Plage historique            | Utilisation              |
| ------ | ------------: | --------------------------- | ------------------------ |
| **A**  |         1–126 | 1.0.0.0 → 126.255.255.255   | Très grands réseaux      |
| **B**  |       128–191 | 128.0.0.0 → 191.255.255.255 | Réseaux moyens           |
| **C**  |       192–223 | 192.0.0.0 → 223.255.255.255 | Petits réseaux           |
| **D**  |       224–239 | 224.0.0.0 → 239.255.255.255 | Multicast                |
| **E**  |       240–255 | 240.0.0.0 → 255.255.255.255 | Réservée / expérimentale |

> **Important :** ce système de classes est aujourd'hui principalement **historique**. Les réseaux modernes utilisent le **CIDR**, qui permet de définir des préfixes de longueur variable.

### Adresses privées — RFC 1918

Certaines plages IPv4 sont réservées aux réseaux privés.

| Plage            |              Taille |
| ---------------- | ------------------: |
| `10.0.0.0/8`     | 16 777 216 adresses |
| `172.16.0.0/12`  |  1 048 576 adresses |
| `192.168.0.0/16` |     65 536 adresses |

Exemples :

```text
10.0.0.15
172.16.20.10
192.168.1.100
```

Ces adresses sont utilisées dans les réseaux internes et ne sont pas directement routées sur Internet.

---

# 4.1.3. Adresse réseau, broadcast et adresses utiles

Considérons le réseau :

```text
192.168.1.0/24
```

Le `/24` signifie que les **24 premiers bits** représentent le réseau.

Le masque correspondant est :

```text
255.255.255.0
```

On obtient :

```text
Réseau : 192.168.1.0
```

L'adresse de broadcast est :

```text
192.168.1.255
```

Les adresses généralement attribuables aux hôtes sont :

```text
192.168.1.1
       ↓
192.168.1.254
```

On a donc :

```text
Adresse réseau    : 192.168.1.0
Première adresse  : 192.168.1.1
Dernière adresse  : 192.168.1.254
Broadcast         : 192.168.1.255
```

Pour un sous-réseau IPv4 classique, le nombre d'adresses d'hôtes utilisables est généralement :

```text
2^n - 2
```

où `n` représente le nombre de bits réservés aux hôtes.

Pour `/24` :

```text
32 - 24 = 8 bits hôte

2^8 - 2 = 254 hôtes
```

> Cette règle du `-2` concerne le modèle classique où l'adresse réseau et l'adresse de broadcast ne sont pas attribuées à des hôtes. Certaines configurations particulières utilisent des règles différentes.

---

# 4.1.4. Masques de sous-réseau, CIDR et VLSM

## Masque de sous-réseau

Le **masque de sous-réseau** permet de déterminer quelle partie de l'adresse IPv4 correspond au réseau et quelle partie correspond aux hôtes.

Exemple :

```text
Adresse : 192.168.1.10
Masque  : 255.255.255.0
```

En binaire :

```text
Adresse :
11000000.10101000.00000001.00001010

Masque :
11111111.11111111.11111111.00000000
```

Les `1` représentent la partie réseau et les `0` la partie hôte.

```text
11111111.11111111.11111111.00000000
<---------- réseau --------><hôte>
```

---

## CIDR

**CIDR (Classless Inter-Domain Routing)** permet d'indiquer directement la longueur du préfixe réseau.

Exemple :

```text
192.168.1.0/24
```

Le `/24` signifie :

```text
24 bits réseau
8 bits hôte
```

Quelques exemples :

| CIDR  | Masque          | Bits hôte |   Adresses |
| ----- | --------------- | --------: | ---------: |
| `/8`  | 255.0.0.0       |        24 | 16 777 216 |
| `/16` | 255.255.0.0     |        16 |     65 536 |
| `/24` | 255.255.255.0   |         8 |        256 |
| `/25` | 255.255.255.128 |         7 |        128 |
| `/26` | 255.255.255.192 |         6 |         64 |
| `/27` | 255.255.255.224 |         5 |         32 |
| `/28` | 255.255.255.240 |         4 |         16 |
| `/30` | 255.255.255.252 |         2 |          4 |

Pour un réseau classique, le nombre d'hôtes utilisables est généralement :

```text
Nombre d'hôtes = 2^(bits hôte) - 2
```

---

## Exemple de calcul d'un sous-réseau

Soit :

```text
192.168.10.0/26
```

Le `/26` laisse :

```text
32 - 26 = 6 bits
```

pour les hôtes.

Nombre total d'adresses :

```text
2^6 = 64
```

Masque :

```text
255.255.255.192
```

Les sous-réseaux `/26` avancent par blocs de **64** :

```text
Sous-réseau 1 :
192.168.10.0/26

Réseau    : 192.168.10.0
Hôtes     : 192.168.10.1 → 192.168.10.62
Broadcast : 192.168.10.63
```

Puis :

```text
Sous-réseau 2 :
192.168.10.64/26

Réseau    : 192.168.10.64
Hôtes     : 192.168.10.65 → 192.168.10.126
Broadcast : 192.168.10.127
```

Puis :

```text
192.168.10.128/26
192.168.10.192/26
```

On peut donc découper :

```text
192.168.10.0/24
        ↓
+-------+-------+-------+-------+
| /26   | /26   | /26   | /26   |
+-------+-------+-------+-------+
```

---

## VLSM

**VLSM (Variable Length Subnet Mask)** permet d'utiliser des masques de longueurs différentes dans un même réseau.

Cela permet d'éviter de gaspiller des adresses IP.

Supposons une entreprise ayant besoin de :

```text
Département A → 100 hôtes
Département B → 50 hôtes
Département C → 20 hôtes
```

On peut utiliser :

```text
A → /25 → 126 hôtes utilisables
B → /26 → 62 hôtes utilisables
C → /27 → 30 hôtes utilisables
```

Au lieu d'attribuer `/24` à chaque département, on adapte la taille du sous-réseau au besoin.

---

# 4.2. Adressage IPv6

IPv6 a été développé notamment pour répondre à la limitation du nombre d'adresses IPv4.

Une adresse IPv6 possède **128 bits**, soit **16 octets**.

Elle est représentée en notation hexadécimale.

Exemple :

```text
2001:0db8:0000:0000:0000:ff00:0042:8329
```

Chaque groupe représente 16 bits :

```text
2001 : 0db8 : 0000 : 0000 : 0000 : ff00 : 0042 : 8329
  ↓      ↓      ↓      ↓      ↓      ↓      ↓      ↓
16 bits × 8 = 128 bits
```

---

## Simplification d'une adresse IPv6

Les zéros non significatifs peuvent être supprimés :

```text
2001:0db8:0000:0000:0000:ff00:0042:8329
```

devient :

```text
2001:db8:0:0:0:ff00:42:8329
```

Une suite consécutive de groupes `0000` peut être remplacée par `::`.

```text
2001:db8:0:0:0:ff00:42:8329
```

devient :

```text
2001:db8::ff00:42:8329
```

`::` ne peut être utilisé qu'une seule fois dans une adresse afin d'éviter toute ambiguïté.

---

# 4.2.2. Types d'adresses IPv6

## Global Unicast

Les adresses **Global Unicast** sont utilisées pour l'adressage IPv6 global et peuvent être routées sur Internet.

Elles appartiennent généralement à l'espace :

```text
2000::/3
```

Exemple :

```text
2001:db8::10
```

`2001:db8::/32` est notamment utilisé pour la documentation.

---

## Link-Local

Les adresses **Link-Local** sont utilisées pour la communication sur le lien local.

Elles appartiennent à :

```text
fe80::/10
```

Elles sont automatiquement présentes sur les interfaces IPv6 dans de nombreux cas.

Elles ne sont pas routées au-delà du lien local.

---

## Loopback

L'adresse loopback IPv6 est :

```text
::1
```

Elle joue un rôle similaire à :

```text
127.0.0.1
```

en IPv4.

Elle permet à une machine de communiquer avec elle-même.

---

## Multicast

Les adresses multicast IPv6 commencent par :

```text
ff00::/8
```

Elles permettent d'envoyer des paquets à un groupe de destinataires.

IPv6 n'utilise pas le **broadcast** de la même manière qu'IPv4 ; plusieurs fonctions sont assurées par le multicast.

---

# 4.2.3. SLAAC et NDP

## SLAAC

**SLAAC (Stateless Address Autoconfiguration)** permet à un équipement IPv6 de configurer automatiquement son adresse sans nécessiter nécessairement un serveur DHCPv6.

Le routeur annonce notamment un préfixe IPv6 sur le réseau.

L'hôte peut alors construire une adresse IPv6 à partir des informations reçues et de son identifiant d'interface selon le mécanisme utilisé.

Conceptuellement :

```text
Routeur
   |
   | Router Advertisement
   | Préfixe IPv6
   ↓
PC
   |
   ↓
Configuration automatique
```

---

## NDP

**NDP (Neighbor Discovery Protocol)** est un protocole IPv6 basé sur **ICMPv6**.

Il remplace et étend plusieurs fonctions assurées par ARP en IPv4.

NDP permet notamment :

* la découverte des voisins ;
* la découverte des routeurs ;
* la résolution d'adresse au niveau local ;
* la détection de voisins inaccessibles ;
* certaines fonctions d'autoconfiguration.

Par exemple :

```text
IPv6 → Adresse MAC
```

est réalisé grâce aux mécanismes de **Neighbor Discovery**, et non avec ARP.

---

# 4.3. Protocoles associés à la couche Réseau

## En-tête IPv4

Un paquet IPv4 contient un en-tête comportant notamment :

```text
+-------------------+
| Version           |
| IHL               |
| TOS / DSCP        |
| Total Length      |
| Identification    |
| Flags             |
| Fragment Offset   |
| TTL               |
| Protocol          |
| Header Checksum   |
| Source IP         |
| Destination IP    |
| Options...        |
+-------------------+
```

### TTL

**TTL (Time To Live)** limite le nombre de routeurs qu'un paquet IPv4 peut traverser.

À chaque passage par un routeur :

```text
TTL = TTL - 1
```

Lorsque le TTL atteint zéro, le paquet est généralement supprimé.

Cela permet notamment d'éviter qu'un paquet circule indéfiniment en cas de boucle de routage.

---

## Fragmentation IPv4

Lorsqu'un paquet IPv4 est trop grand pour être transmis sur un lien ayant une certaine **MTU (Maximum Transmission Unit)**, il peut être fragmenté selon les règles IPv4.

Les champs :

* `Identification` ;
* `Flags` ;
* `Fragment Offset`

permettent de gérer la fragmentation et le réassemblage.

> En IPv6, les routeurs ne fragmentent pas les paquets en transit. La fragmentation est effectuée par la source à l'aide de l'extension **Fragment** si nécessaire.

---

## Header Checksum

IPv4 possède un **checksum de l'en-tête** permettant de détecter certaines erreurs dans l'en-tête.

Il est recalculé lorsque certains champs de l'en-tête, notamment le TTL, changent.

> **IPv6 ne possède pas de checksum dans son en-tête principal.** L'intégrité des données repose notamment sur les couches supérieures et, au niveau liaison, sur les mécanismes propres à la technologie utilisée.

---

# ICMP

**ICMP (Internet Control Message Protocol)** est utilisé pour transmettre des messages de contrôle, d'erreur et de diagnostic liés au réseau.

Il ne sert pas principalement à transporter les données applicatives.

---

## Ping

La commande :

```bash
ping 8.8.8.8
```

permet notamment de vérifier si une destination répond et de mesurer le temps aller-retour.

Elle utilise généralement :

```text
ICMP Echo Request
        ↓
    Destination
        ↓
ICMP Echo Reply
```

---

## Traceroute

`traceroute` permet d'identifier les différents routeurs traversés pour atteindre une destination.

Sous Windows :

```cmd
tracert google.com
```

Sous Linux :

```bash
traceroute google.com
```

Le mécanisme exploite notamment la variation du **TTL** et les réponses ICMP générées par les routeurs.

---

# 4.4. Principes et Protocoles de Routage

Le **routage** consiste à déterminer par quel chemin un paquet doit être envoyé pour atteindre un réseau de destination.

Un routeur possède une **table de routage**.

Exemple :

```text
Destination       Masque            Passerelle       Interface    Métrique
192.168.1.0       255.255.255.0    Direct           eth0         0
10.0.0.0          255.0.0.0        192.168.1.1      eth1         10
0.0.0.0           0.0.0.0          192.168.1.1      eth1         20
```

---

# 4.4.1. Fonctionnement d'une table de routage

Une entrée de routage contient généralement :

### Réseau de destination

Le réseau que le routeur cherche à atteindre.

Exemple :

```text
192.168.10.0/24
```

### Masque / Préfixe

Il détermine la taille du réseau.

```text
/24
```

### Passerelle (Next Hop)

Adresse du routeur suivant auquel le paquet doit être transmis.

```text
192.168.1.1
```

### Interface

Interface de sortie utilisée par le routeur.

```text
eth0
```

### Métrique

Valeur utilisée pour comparer différentes routes selon les règles du protocole ou du système.

---

## Longest Prefix Match

Lorsqu'un routeur possède plusieurs routes correspondant à une destination, il sélectionne généralement la route correspondant au **préfixe le plus spécifique**.

Exemple :

```text
10.0.0.0/8
10.10.0.0/16
10.10.10.0/24
```

Pour la destination :

```text
10.10.10.50
```

les trois routes peuvent correspondre, mais :

```text
/24 > /16 > /8
```

La route :

```text
10.10.10.0/24
```

est donc la plus spécifique.

---

# 4.4.2. Routage statique vs routage dynamique

## Routage statique

Une route statique est configurée manuellement par l'administrateur.

Exemple conceptuel :

```text
Réseau destination : 10.10.0.0/16
Next Hop            : 192.168.1.1
```

### Avantages

* simple pour les petits réseaux ;
* comportement prévisible ;
* aucun protocole de routage dynamique nécessaire.

### Inconvénients

* configuration manuelle ;
* difficile à maintenir dans un grand réseau ;
* adaptation limitée aux changements de topologie.

---

## Routage dynamique

Les routeurs utilisent un **protocole de routage** pour échanger des informations et construire automatiquement leurs routes.

Exemples :

```text
RIP
OSPF
BGP
```

### Avantages

* adaptation aux changements de réseau ;
* automatisation ;
* adapté aux infrastructures importantes.

### Inconvénients

* configuration plus complexe ;
* consommation de ressources ;
* nécessite une bonne compréhension du protocole utilisé.

---

# 4.4.3. Protocoles IGP

Un **IGP (Interior Gateway Protocol)** est utilisé pour le routage **à l'intérieur d'un même système autonome (AS)**.

Deux grandes familles sont particulièrement importantes :

* Distance Vector ;
* Link State.

---

## A. Vecteur de distances : RIP

**RIP (Routing Information Protocol)** est un protocole de type **Distance Vector**.

Il utilise principalement le **nombre de sauts (hop count)** comme métrique.

Exemple :

```text
Route A → B → C → D

Nombre de sauts = 3
```

RIP considère qu'une route avec moins de sauts est préférable selon sa métrique.

La limite classique de RIP est :

```text
15 sauts maximum
```

Une distance de :

```text
16
```

est considérée comme inaccessible.

RIP est donc principalement adapté à des réseaux relativement simples et constitue aujourd'hui un protocole surtout étudié pour comprendre le fonctionnement du routage à vecteur de distances.

---

## B. État de liens : OSPF

**OSPF (Open Shortest Path First)** est un protocole de routage de type **Link State**.

Chaque routeur construit une représentation de la topologie du réseau dans sa zone et calcule les meilleurs chemins.

OSPF utilise l'algorithme de **Dijkstra**, également appelé **Shortest Path First (SPF)**.

Conceptuellement :

```text
       B
      / \
     /   \
    A-----C
     \   /
      \ /
       D
```

Le routeur calcule les chemins possibles et sélectionne les chemins correspondant aux meilleurs coûts selon la métrique OSPF.

### Zones OSPF

OSPF permet de diviser un réseau en **zones (Areas)**.

La zone principale est :

```text
Area 0
```

appelée **Backbone Area**.

Une architecture OSPF peut être représentée ainsi :

```text
          Area 1
        /         \
       /           \
   Router -------- Router
        \         /
          Area 0
        Backbone
             |
          Area 2
```

La segmentation en zones permet notamment de réduire la quantité d'informations de topologie à gérer dans les grandes infrastructures.

---

# 4.4.4. Protocoles EGP : BGP

**BGP (Border Gateway Protocol)** est le principal protocole utilisé pour le **routage inter-domaines sur Internet**.

Il permet l'échange d'informations de routage entre différents **systèmes autonomes (Autonomous Systems — AS)**.

Un système autonome représente un ensemble de réseaux administrés sous une politique de routage commune.

Conceptuellement :

```text
AS 64500
   |
   | BGP
   |
AS 64501
   |
   | BGP
   |
AS 64502
```

Contrairement à RIP ou OSPF, BGP ne cherche pas simplement « le chemin ayant le moins de sauts ».

Il utilise des **attributs de routes** et des politiques de routage pour déterminer les routes à annoncer et à sélectionner.

Parmi les attributs BGP importants figurent notamment :

* **AS_PATH** ;
* **NEXT_HOP** ;
* **LOCAL_PREF** ;
* **MED** ;
* **COMMUNITY**.

BGP est donc particulièrement adapté au routage **entre systèmes autonomes** et constitue un élément essentiel du fonctionnement d'Internet.

---

# Comparaison des principaux protocoles de routage

| Protocole | Type            | Utilisation              | Métrique / principe               |
| --------- | --------------- | ------------------------ | --------------------------------- |
| **RIP**   | Distance Vector | Routage interne          | Nombre de sauts                   |
| **OSPF**  | Link State      | Routage interne          | Coût + calcul SPF                 |
| **BGP**   | Inter-domaines  | Entre systèmes autonomes | Attributs + politiques de routage |

---

## À retenir

| Concept               | Rôle                                               |
| --------------------- | -------------------------------------------------- |
| **IPv4**              | Adressage sur 32 bits                              |
| **IPv6**              | Adressage sur 128 bits                             |
| **CIDR**              | Adressage sans classes avec préfixe variable       |
| **VLSM**              | Utilisation de sous-réseaux de tailles différentes |
| **ARP**               | IPv4 → MAC sur le réseau local                     |
| **NDP**               | Découverte et résolution de voisins en IPv6        |
| **TTL**               | Limite le nombre de sauts d'un paquet IPv4         |
| **ICMP**              | Contrôle, erreurs et diagnostics réseau            |
| **Ping**              | Test de connectivité et mesure du RTT              |
| **Traceroute**        | Identification du chemin vers une destination      |
| **Routage statique**  | Routes configurées manuellement                    |
| **Routage dynamique** | Routes apprises automatiquement                    |
| **RIP**               | Distance Vector, métrique en nombre de sauts       |
| **OSPF**              | Link State, algorithme SPF/Dijkstra                |
| **BGP**               | Routage entre systèmes autonomes                   |

### Points essentiels

* La couche 3 assure principalement **l'adressage logique et le routage des paquets**.
* IPv4 utilise **32 bits**, tandis qu'IPv6 utilise **128 bits**.
* Le **CIDR** a remplacé le modèle historique des classes comme méthode moderne de découpage des réseaux.
* Le **VLSM** permet de créer des sous-réseaux de tailles différentes.
* **ARP** résout une adresse IPv4 en adresse MAC ; IPv6 utilise **NDP**.
* Le **TTL** limite la durée de vie d'un paquet IPv4 en nombre de sauts.
* **ICMP** est utilisé notamment par `ping` et `traceroute`.
* Un routeur choisit généralement la route correspondant au **préfixe le plus spécifique**.
* **RIP** utilise le nombre de sauts, **OSPF** calcule des chemins selon l'état des liens, et **BGP** assure principalement le routage inter-domaines.
# 5. La Couche Transport (Couche 4)

La **couche Transport** est la **couche 4 du modèle OSI**.

Elle assure la communication logique entre les applications exécutées sur des machines différentes.

Ses principales fonctions sont :

* l'identification des applications avec les **numéros de port** ;
* le transport de données entre applications ;
* le contrôle de flux ;
* la fiabilité de transmission selon le protocole utilisé ;
* la segmentation et le réassemblage des données.

Les deux principaux protocoles de transport sont :

* **TCP (Transmission Control Protocol)** ;
* **UDP (User Datagram Protocol)**.

---

# 5.1. Notions de ports et de sockets

## Numéro de port

Une adresse IP permet d'identifier une **machine/interface réseau**, mais elle ne permet pas à elle seule d'identifier l'application destinataire.

Le **numéro de port** permet d'identifier le service ou l'application concernée.

On peut donc représenter une communication ainsi :

```text
Adresse IP → Quelle machine ?
Port        → Quelle application ?
```

Exemple :

```text
192.168.1.10:443
```

signifie :

```text
IP   = 192.168.1.10
Port = 443
```

Le port `443` est généralement associé à **HTTPS**.

---

## Catégories de ports

Les ports sont numérotés de :

```text
0 → 65535
```

Ils sont généralement répartis en trois catégories.

### Ports bien connus (Well-Known Ports)

```text
0 → 1023
```

Ils sont associés à des services et protocoles courants.

Exemples :

|  Port | Protocole / Service |
| ----: | ------------------- |
| 20/21 | FTP                 |
|    22 | SSH                 |
|    23 | Telnet              |
|    25 | SMTP                |
|    53 | DNS                 |
|    80 | HTTP                |
|   443 | HTTPS               |

---

### Ports enregistrés (Registered Ports)

```text
1024 → 49151
```

Ils peuvent être utilisés par différentes applications et services enregistrés auprès de l'IANA.

---

### Ports dynamiques / privés

```text
49152 → 65535
```

Ils sont souvent utilisés temporairement comme **ports source** par les clients lorsqu'ils établissent des connexions.

Exemple :

```text
Client                         Serveur
192.168.1.10                   142.250.x.x
Port source : 52000            Port destination : 443

        192.168.1.10:52000
                 ↓
              Internet
                 ↓
        142.250.x.x:443
```

---

# Socket

Un **socket** représente un point d'extrémité d'une communication réseau.

Dans une représentation simplifiée, un socket peut être identifié par :

```text
Adresse IP + Port
```

Exemple :

```text
192.168.1.10:52000
```

Pour identifier complètement une connexion TCP, on considère généralement le quadruplet :

```text
IP source
Port source
IP destination
Port destination
```

Par exemple :

```text
192.168.1.10:52000
        ↓
142.250.72.14:443
```

Deux connexions peuvent donc utiliser le même serveur et le même port de destination tout en étant distinguées grâce à leurs adresses/ports source.

---

# 5.2. Protocole TCP

**TCP (Transmission Control Protocol)** est un protocole de transport **orienté connexion**.

Il fournit notamment :

* une transmission fiable ;
* la remise des données dans l'ordre ;
* la détection de pertes ;
* la retransmission de segments perdus ;
* le contrôle de flux ;
* le contrôle de congestion.

TCP considère les données comme un **flux d'octets** plutôt que comme une succession de messages indépendants.

---

## Établissement d'une connexion TCP

Avant d'échanger les données, TCP établit une connexion à l'aide du **three-way handshake**.

Les trois étapes principales sont :

```text
Client                              Serveur

  | -------- SYN ------------------> |
  |                                  |
  | <------ SYN + ACK -------------- |
  |                                  |
  | -------- ACK ------------------> |
  |                                  |
  |       Connexion établie          |
```

### 1. SYN

Le client envoie un segment avec le flag :

```text
SYN = 1
```

Il indique notamment qu'il souhaite établir une connexion et fournit un numéro de séquence initial.

---

### 2. SYN-ACK

Le serveur répond avec :

```text
SYN = 1
ACK = 1
```

Il confirme la réception du SYN du client et fournit également son propre numéro de séquence initial.

---

### 3. ACK

Le client répond avec :

```text
ACK = 1
```

La connexion TCP est alors établie et les données peuvent être échangées.

---

# Fiabilité de TCP

TCP utilise plusieurs mécanismes pour fournir une transmission fiable.

## Numéros de séquence

Les données sont associées à des **numéros de séquence** permettant notamment de :

* remettre les données dans le bon ordre ;
* identifier les données manquantes ;
* gérer les retransmissions.

---

## Accusés de réception (ACK)

Le récepteur envoie des **ACK (Acknowledgements)** pour indiquer les données reçues.

Conceptuellement :

```text
Client
  |
  | Segment 1
  |-------------------->
  |
  | Segment 2
  |-------------------->
  |
  | <------------------- ACK
  |
```

Si certaines données sont perdues, TCP peut les retransmettre.

---

## Retransmission

Exemple :

```text
Client                         Serveur

Segment 1 -------------------->
Segment 2 -------------------->
Segment 3 ----X               (perdu)

ACK --------------------------->
                ↓
        Détection de la perte
                ↓
Segment 3 -------------------->
```

TCP retransmet alors les données qui n'ont pas été correctement reconnues.

---

# Contrôle de flux et fenêtre glissante

TCP utilise une **fenêtre glissante (Sliding Window)** pour contrôler la quantité de données pouvant être envoyée avant de recevoir les accusés de réception correspondants.

L'objectif est notamment d'éviter qu'un émetteur rapide ne surcharge le récepteur.

Conceptuellement :

```text
Données envoyées
+------+------+------+------+
|  1   |  2   |  3   |  4   |
+------+------+------+------+
   ↑              ↑
ACK reçus       données autorisées
```

Le récepteur annonce une **fenêtre de réception (Receive Window)** indiquant la quantité de données qu'il peut accepter.

Si le récepteur dispose de moins d'espace disponible, il peut réduire cette fenêtre.

---

## Contrôle de flux vs contrôle de congestion

Ces deux mécanismes sont différents.

### Contrôle de flux

Il protège principalement le **récepteur**.

```text
Émetteur rapide
      ↓
Récepteur limité
      ↓
Réduction du débit
```

TCP utilise notamment la **fenêtre de réception (rwnd)**.

### Contrôle de congestion

Il protège principalement le **réseau** contre la saturation.

TCP utilise notamment une **fenêtre de congestion (cwnd)**.

La quantité de données pouvant être envoyée est donc influencée par plusieurs mécanismes, notamment :

```text
Fenêtre effective ≈ min(rwnd, cwnd)
```

---

# Fermeture d'une connexion TCP

Une connexion TCP est généralement fermée avec les flags :

```text
FIN
ACK
```

La fermeture normale est généralement **bidirectionnelle** et implique plusieurs échanges.

Exemple simplifié :

```text
Client                              Serveur

  | -------- FIN -----------------> |
  | <------- ACK ------------------ |
  |                                 |
  | <------- FIN ------------------ |
  | -------- ACK -----------------> |
  |                                 |
  |       Connexion fermée          |
```

Chaque direction du flux TCP peut être fermée indépendamment.

---

# États TCP

Une connexion TCP passe par différents états.

Quelques états importants :

```text
LISTEN
SYN-SENT
SYN-RECEIVED
ESTABLISHED
FIN-WAIT
CLOSE-WAIT
TIME-WAIT
CLOSED
```

L'état :

```text
ESTABLISHED
```

indique qu'une connexion TCP est établie et peut transporter des données.

---

# 5.3. Protocole UDP

**UDP (User Datagram Protocol)** est un protocole de transport **sans connexion**.

Contrairement à TCP, UDP ne réalise pas de handshake avant l'envoi des données.

Il fournit un mécanisme de transport beaucoup plus simple.

UDP ne garantit notamment pas :

* la livraison ;
* l'ordre des datagrammes ;
* la retransmission automatique ;
* le contrôle de flux comme TCP.

---

## Fonctionnement d'UDP

Avec UDP :

```text
Émetteur                    Récepteur

Datagramme 1 -------------------->
Datagramme 2 -------------------->
Datagramme 3 ----X
Datagramme 4 -------------------->
```

Si le datagramme 3 est perdu, UDP ne le retransmet pas automatiquement.

Il appartient à l'application de gérer la perte si elle en a besoin.

---

## Caractéristiques d'UDP

UDP possède un en-tête très simple :

```text
+----------------+----------------+
| Port Source    | Port Destination|
+----------------+----------------+
| Longueur       | Checksum        |
+----------------+----------------+
```

Il introduit donc peu de surcharge par rapport à TCP.

UDP est notamment utilisé lorsque :

* la faible latence est importante ;
* l'application peut gérer elle-même les pertes ;
* un mécanisme de retransmission au niveau TCP serait inadapté ;
* le protocole applicatif possède ses propres mécanismes de contrôle.

Exemples d'utilisation :

* DNS ;
* DHCP ;
* certains flux multimédias ;
* VoIP ;
* certains jeux en réseau ;
* HTTP/3 via **QUIC**, qui utilise UDP comme protocole de transport sous-jacent.

---

# TCP vs UDP

| Caractéristique        | TCP                        | UDP                            |
| ---------------------- | -------------------------- | ------------------------------ |
| Connexion              | Orienté connexion          | Sans connexion                 |
| Handshake              | Oui                        | Non                            |
| Fiabilité              | Oui                        | Non garantie                   |
| Ordre des données      | Garanti                    | Non garanti                    |
| Retransmission         | Oui                        | Non                            |
| Contrôle de flux       | Oui                        | Non                            |
| Contrôle de congestion | Oui                        | Non intégré de la même manière |
| Surcharge              | Plus importante            | Faible                         |
| Latence potentielle    | Plus élevée                | Généralement plus faible       |
| Unité de données       | Flux d'octets              | Datagrammes                    |
| Exemples               | HTTP/1.1, HTTP/2, SSH, FTP | DNS, DHCP, VoIP, QUIC          |

---

## Exemple concret

### TCP — téléchargement d'un fichier

Lorsqu'un fichier doit être transmis correctement :

```text
Fichier
   ↓
TCP
   ↓
Segments
   ↓
Réseau
   ↓
Récepteur
   ↓
Réassemblage
```

Si un segment est perdu :

```text
Segment perdu
      ↓
Détection
      ↓
Retransmission
      ↓
Réception complète
```

TCP est donc adapté aux applications où l'intégrité et l'ordre des données sont importants.

### UDP — communication temps réel

Pour une communication audio/vidéo en temps réel :

```text
Audio → Datagrammes UDP → Réseau → Récepteur
```

Si un paquet audio est perdu, attendre sa retransmission peut être plus problématique que de continuer avec les données suivantes.

Dans certains cas :

```text
Paquet perdu
     ↓
Pas de retransmission TCP
     ↓
On continue avec le suivant
```

Cela peut permettre de privilégier la **latence** plutôt que la fiabilité absolue.

---

## À retenir

* La **couche Transport** assure la communication entre les applications.
* Les **ports** permettent d'identifier les services ou applications.
* Un socket peut être représenté simplement par **IP + port**.
* Une connexion TCP est identifiée notamment par les **IP et ports source/destination**.
* **TCP** est orienté connexion et fournit fiabilité, ordre, retransmission et contrôle de flux.
* Le **three-way handshake** utilise `SYN → SYN-ACK → ACK`.
* TCP utilise une **fenêtre glissante** pour gérer le contrôle de flux et optimiser la transmission.
* Le **contrôle de flux** protège le récepteur, tandis que le **contrôle de congestion** vise à éviter la saturation du réseau.
* **UDP** est sans connexion et ne garantit ni livraison ni ordre.
* UDP possède moins de mécanismes de contrôle et est adapté à de nombreux scénarios où la simplicité ou la faible latence est importante.
* **TCP n'est pas simplement « lent » et UDP « rapide »** : le choix dépend des besoins de l'application et des mécanismes utilisés au-dessus.
# 6. La Couche Application et les Services Réseau (Couches 5, 6, 7)

Dans le modèle **OSI**, les couches 5, 6 et 7 sont :

* **Couche 5 — Session** : gestion des sessions de communication ;
* **Couche 6 — Présentation** : représentation, encodage, chiffrement et compression des données ;
* **Couche 7 — Application** : services réseau directement utilisés par les applications.

Dans le modèle **TCP/IP**, ces trois couches sont généralement regroupées dans une seule **couche Application**.

Cette couche regroupe les protocoles permettant aux applications de communiquer sur le réseau.

---

# 6.1. Services d'infrastructure basiques

## 6.1.1. DNS — Domain Name System

Le **DNS (Domain Name System)** permet principalement de traduire un **nom de domaine** en adresse IP.

Par exemple :

```text
www.example.com
       ↓
DNS
       ↓
93.184.216.34
```

Cela évite aux utilisateurs de devoir mémoriser les adresses IP des serveurs.

DNS utilise principalement le **port 53** :

* **UDP 53** : requêtes DNS classiques dans de nombreux cas ;
* **TCP 53** : utilisé notamment pour certaines réponses importantes, transferts de zone et autres situations nécessitant TCP.

### Hiérarchie DNS

DNS possède une structure hiérarchique :

```text
                         .
                    Root DNS
                        |
              +---------+---------+
              |                   |
             .com                .org
              |
          example.com
              |
        www.example.com
```

Les différents niveaux sont notamment :

1. **Root** (`.`)
2. **TLD** (`.com`, `.org`, `.ma`, etc.)
3. **Domaine**
4. **Sous-domaine / nom d'hôte**

---

## Principaux enregistrements DNS

### A

Associe un nom à une adresse **IPv4**.

```text
example.com → 192.0.2.10
```

### AAAA

Associe un nom à une adresse **IPv6**.

```text
example.com → 2001:db8::10
```

### CNAME

Crée un alias vers un autre nom DNS.

```text
www.example.com → example.com
```

Le CNAME pointe donc vers un **nom**, et non directement vers une adresse IP.

### MX

Indique les serveurs responsables de la réception des emails d'un domaine.

```text
example.com
      ↓
MX
      ↓
mail.example.com
```

### NS

Indique les serveurs DNS faisant autorité pour une zone.

```text
example.com
      ↓
NS
      ↓
ns1.example.com
ns2.example.com
```

### PTR

Utilisé principalement pour la **résolution inverse** :

```text
Adresse IP → Nom
```

Exemple conceptuel :

```text
192.0.2.10
     ↓
PTR
     ↓
server.example.com
```

---

## Résolution DNS

Lorsqu'un utilisateur saisit :

```text
www.example.com
```

le système doit obtenir l'adresse IP correspondante.

De manière simplifiée :

```text
Application
     ↓
Résolveur DNS
     ↓
Serveur DNS
     ↓
Adresse IP
     ↓
Communication avec le serveur
```

Un résolveur peut utiliser son **cache DNS** afin d'éviter de refaire inutilement une résolution complète.

---

# 6.1.2. DHCP — Dynamic Host Configuration Protocol

**DHCP** permet de configurer automatiquement les paramètres réseau d'un équipement.

Il peut notamment fournir :

* une adresse IP ;
* un masque de sous-réseau ;
* une passerelle par défaut ;
* des serveurs DNS ;
* une durée de bail (**lease**).

DHCP utilise principalement :

```text
UDP 67 → Serveur DHCP
UDP 68 → Client DHCP
```

---

## Processus DORA

L'attribution dynamique d'une adresse IPv4 utilise classiquement le processus :

```text
D → Discover
O → Offer
R → Request
A → Acknowledge
```

### 1. DHCP Discover

Le client ne possède pas encore nécessairement d'adresse IP utilisable.

Il diffuse donc une requête :

```text
Client
  |
  | DHCP Discover
  |-------------------->
  |       Broadcast
  |
Serveur DHCP
```

Il cherche un serveur DHCP disponible.

---

### 2. DHCP Offer

Le serveur propose une configuration :

```text
Serveur DHCP
  |
  | DHCP Offer
  |-------------------->
  |
Client
```

Exemple :

```text
IP proposée : 192.168.1.20
Masque       : 255.255.255.0
Passerelle   : 192.168.1.1
DNS          : 192.168.1.1
```

---

### 3. DHCP Request

Le client indique qu'il souhaite utiliser l'offre proposée :

```text
Client
  |
  | DHCP Request
  |-------------------->
  |
Serveur DHCP
```

---

### 4. DHCP ACK

Le serveur confirme l'attribution :

```text
Serveur DHCP
  |
  | DHCP ACK
  |-------------------->
  |
Client
```

Le client peut alors utiliser la configuration reçue.

### Résumé

```text
Client                           Serveur DHCP

   |---- DHCP Discover ---------->|
   |                              |
   |<----- DHCP Offer ------------|
   |                              |
   |---- DHCP Request ----------->|
   |                              |
   |<------ DHCP ACK -------------|
```

---

# 6.2. Protocoles d'application courants

## 6.2.1. Web : HTTP et HTTPS

### HTTP

**HTTP (Hypertext Transfer Protocol)** est le protocole utilisé pour les communications entre clients et serveurs Web.

Le port traditionnel d'HTTP est :

```text
TCP 80
```

Exemple :

```text
Navigateur
    |
    | HTTP Request
    ↓
Serveur Web
    |
    | HTTP Response
    ↓
Navigateur
```

Une requête HTTP peut être par exemple :

```http
GET /index.html HTTP/1.1
Host: example.com
```

Le serveur répond avec une réponse HTTP.

---

## HTTPS

**HTTPS (HTTP Secure)** correspond à HTTP utilisé avec une couche de sécurité **TLS (Transport Layer Security)**.

Le port traditionnel est :

```text
TCP 443
```

Le chiffrement TLS permet notamment d'assurer :

* la confidentialité des données ;
* l'intégrité des communications ;
* l'authentification du serveur via les certificats.

Conceptuellement :

```text
HTTP
  +
 TLS
  ↓
HTTPS
```

> Le terme **SSL** est historiquement utilisé, mais les versions modernes utilisent **TLS**. SSL est aujourd'hui obsolète.

---

# 6.2.2. Transfert de fichiers

## FTP

**FTP (File Transfer Protocol)** est un protocole de transfert de fichiers.

Il utilise traditionnellement :

```text
TCP 21 → connexion de contrôle
TCP 20 → connexion de données en mode actif
```

Le comportement du canal de données peut toutefois varier selon le **mode actif ou passif**.

FTP ne chiffre pas nativement les identifiants et les données.

---

## SFTP

**SFTP (SSH File Transfer Protocol)** permet de transférer des fichiers de manière sécurisée à travers **SSH**.

Il utilise généralement :

```text
TCP 22
```

Il est important de ne pas confondre :

```text
FTP   ≠   SFTP
```

SFTP n'est pas simplement « FTP avec chiffrement » : il s'agit d'un protocole différent fonctionnant au-dessus de SSH.

---

## TFTP

**TFTP (Trivial File Transfer Protocol)** est un protocole de transfert de fichiers très simple.

Il utilise :

```text
UDP 69
```

TFTP possède beaucoup moins de fonctionnalités que FTP et ne fournit notamment pas les mêmes mécanismes d'authentification et de gestion de fichiers.

Il peut être utilisé dans certains environnements réseau, par exemple pour :

* le démarrage réseau ;
* le transfert de configurations ;
* certaines opérations de déploiement de périphériques.

---

# 6.2.3. Messagerie électronique

Plusieurs protocoles interviennent dans le fonctionnement du courrier électronique.

## SMTP

**SMTP (Simple Mail Transfer Protocol)** est principalement utilisé pour **l'envoi et le relais des emails**.

Ports courants :

```text
TCP 25  → relais SMTP, notamment entre serveurs
TCP 587 → soumission de messages par les clients
```

Le port `465` est également utilisé pour la soumission SMTP avec TLS implicite dans de nombreux environnements.

Schéma :

```text
Client mail
     |
     | SMTP
     ↓
Serveur de messagerie
     |
     | SMTP
     ↓
Serveur destinataire
```

---

## POP3

**POP3 (Post Office Protocol version 3)** permet à un client de récupérer les messages depuis un serveur.

Port traditionnel :

```text
TCP 110
```

La version sécurisée utilise généralement :

```text
TCP 995
```

POP3 est historiquement orienté vers le téléchargement des messages vers le client.

---

## IMAP

**IMAP (Internet Message Access Protocol)** permet également d'accéder aux emails stockés sur un serveur.

Port traditionnel :

```text
TCP 143
```

La version sécurisée avec TLS implicite utilise généralement :

```text
TCP 993
```

Contrairement au modèle classique de POP3, IMAP est particulièrement adapté à la **synchronisation des messages et dossiers entre plusieurs appareils**.

Exemple :

```text
              Serveur mail
             /     |      \
            /      |       \
        PC      Smartphone   Webmail
            \      |       /
             \     |      /
              Synchronisation
```

---

# 6.2.4. Administration à distance

## Telnet

**Telnet** permet d'établir une session distante en utilisant :

```text
TCP 23
```

Cependant, Telnet transmet les données, notamment les identifiants, **sans chiffrement**.

Il est donc déconseillé pour l'administration distante moderne sur des réseaux non sécurisés.

---

## SSH

**SSH (Secure Shell)** permet d'administrer une machine à distance de manière sécurisée.

Port :

```text
TCP 22
```

SSH fournit notamment :

* chiffrement de la communication ;
* authentification ;
* intégrité des données ;
* exécution de commandes à distance ;
* transfert sécurisé de fichiers via SFTP ;
* tunneling et redirection de ports.

Exemple :

```bash
ssh user@192.168.1.10
```

Conceptuellement :

```text
PC administrateur
       |
       | SSH - TCP 22
       | Communication chiffrée
       ↓
Serveur distant
```

---

# Tableau récapitulatif

| Service / Protocole | Port(s) courant(s) | Transport    | Fonction                             |
| ------------------- | -----------------: | ------------ | ------------------------------------ |
| **DNS**             |                 53 | UDP / TCP    | Résolution de noms                   |
| **DHCP**            |            67 / 68 | UDP          | Configuration réseau automatique     |
| **HTTP**            |                 80 | TCP          | Communication Web                    |
| **HTTPS**           |                443 | TCP avec TLS | Communication Web sécurisée          |
| **FTP**             |            20 / 21 | TCP          | Transfert de fichiers                |
| **SFTP**            |                 22 | TCP / SSH    | Transfert sécurisé de fichiers       |
| **TFTP**            |                 69 | UDP          | Transfert de fichiers simple         |
| **SMTP**            |           25 / 587 | TCP          | Envoi / soumission d'emails          |
| **POP3**            |                110 | TCP          | Récupération d'emails                |
| **IMAP**            |                143 | TCP          | Accès et synchronisation des emails  |
| **Telnet**          |                 23 | TCP          | Administration distante non chiffrée |
| **SSH**             |                 22 | TCP          | Administration distante sécurisée    |

---

## À retenir

* Le **DNS** traduit principalement les noms de domaine en adresses IP.
* Les enregistrements DNS importants comprennent **A, AAAA, CNAME, MX, NS et PTR**.
* **DHCP** automatise la configuration réseau des clients.
* Le processus DHCP classique est **DORA : Discover → Offer → Request → Acknowledge**.
* **HTTP** utilise traditionnellement le port 80 et **HTTPS** le port 443.
* HTTPS correspond à **HTTP + TLS**, et non à HTTP + SSL dans les versions modernes.
* **FTP** utilise traditionnellement les ports 20/21, tandis que **SFTP** fonctionne au-dessus de SSH sur le port 22.
* **SMTP** est principalement utilisé pour l'envoi et le relais des emails.
* **POP3** et **IMAP** permettent aux clients d'accéder aux emails, avec des modèles de fonctionnement différents.
* **Telnet** transmet les données sans chiffrement, tandis que **SSH** fournit une communication sécurisée.
* Dans le modèle TCP/IP, les fonctions correspondant aux couches **5, 6 et 7 du modèle OSI** sont généralement regroupées dans la **couche Application**.
# 7. Sécurité, Supervision et Services Avancés

Après avoir étudié les différentes couches du réseau et les principaux protocoles, cette section présente plusieurs mécanismes utilisés pour **contrôler les communications, sécuriser les infrastructures et superviser leur fonctionnement**.

---

# 7.1. Translation d'adresses — NAT / PAT

## 7.1.1. NAT — Network Address Translation

Le **NAT (Network Address Translation)** permet de modifier les adresses IP contenues dans les paquets lorsqu'ils traversent un équipement réseau, généralement un routeur ou un pare-feu.

Il est notamment utilisé pour permettre à des machines utilisant des **adresses IP privées** d'accéder à des réseaux externes à travers une ou plusieurs adresses IP publiques.

Exemple :

```text
Réseau privé                     Internet

192.168.1.10 ──┐
192.168.1.11 ──┼── Routeur NAT ──── Internet
192.168.1.12 ──┘       |
                    IP publique
                   203.0.113.10
```

Les plages IPv4 privées courantes sont :

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

Ces adresses ne sont pas directement routées sur Internet.

---

## 7.1.2. NAT statique

Le **NAT statique** établit une correspondance permanente entre une adresse privée et une adresse publique.

```text
192.168.1.10  ↔  203.0.113.10
```

La correspondance est généralement **1:1**.

Il peut être utilisé lorsqu'un équipement interne doit être accessible depuis l'extérieur avec une adresse publique déterminée.

---

## 7.1.3. NAT dynamique

Le **NAT dynamique** associe temporairement des adresses privées à un **pool d'adresses publiques**.

Exemple :

```text
192.168.1.10 ──→ 203.0.113.10
192.168.1.11 ──→ 203.0.113.11
192.168.1.12 ──→ 203.0.113.12
```

Les adresses publiques sont attribuées dynamiquement selon les connexions disponibles.

---

## 7.1.4. PAT — Port Address Translation

Le **PAT (Port Address Translation)**, également appelé **NAT Overload**, permet à plusieurs machines privées de partager **une seule adresse IP publique**.

La distinction entre les différentes connexions est réalisée grâce aux **numéros de port**.

Exemple :

```text
Machine A
192.168.1.10:50000
        |
        | NAT/PAT
        ↓
203.0.113.10:40001
```

et :

```text
Machine B
192.168.1.11:50000
        |
        | NAT/PAT
        ↓
203.0.113.10:40002
```

Le routeur conserve une table de traduction :

| IP privée    | Port privé | IP publique  | Port public |
| ------------ | ---------: | ------------ | ----------: |
| 192.168.1.10 |      50000 | 203.0.113.10 |       40001 |
| 192.168.1.11 |      50000 | 203.0.113.10 |       40002 |

Ainsi, le routeur peut déterminer à quelle machine interne appartient chaque réponse.

### À retenir

```text
NAT statique   → 1 IP privée ↔ 1 IP publique
NAT dynamique  → IP privées ↔ pool d'IP publiques
PAT            → plusieurs IP privées ↔ 1 IP publique grâce aux ports
```

---

# 7.2. Équipements et mécanismes de sécurité

## 7.2.1. Pare-feu — Firewall

Un **pare-feu (Firewall)** est un dispositif matériel ou logiciel qui contrôle les communications réseau selon un ensemble de **règles de sécurité**.

Il peut autoriser ou bloquer le trafic selon différents critères :

* adresse IP source ;
* adresse IP destination ;
* protocole ;
* port source ;
* port destination ;
* état de la connexion ;
* parfois contenu ou informations applicatives.

Exemple de règle :

```text
Source      : 192.168.1.0/24
Destination : serveur Web
Port        : TCP 443
Action      : ALLOW
```

---

## Pare-feu filtrant les paquets

Un pare-feu peut examiner les informations contenues dans les en-têtes réseau et décider si un paquet doit être :

```text
ACCEPT
DROP
REJECT
```

Par exemple :

```text
Internet
   |
   | TCP 22
   ↓
Firewall
   |
   X  BLOQUÉ
```

---

## Pare-feu Stateful

Un **pare-feu Stateful** conserve l'état des connexions et sait notamment si un paquet appartient à une connexion déjà établie.

Exemple :

```text
Client → Serveur
SYN
       ↓
Firewall
       ↓
Serveur

Serveur → Client
SYN-ACK
       ↓
Firewall
       ↓
Client
```

Le pare-feu maintient une **table d'état (state table)** afin de suivre les connexions.

Cela permet de distinguer, par exemple, une réponse légitime à une connexion sortante d'une nouvelle connexion initiée depuis Internet.

---

## Pare-feu applicatif

Un **pare-feu applicatif** analyse des informations situées plus haut dans la pile réseau, notamment au niveau des protocoles applicatifs.

Dans le cas du Web, un **WAF (Web Application Firewall)** peut analyser les requêtes HTTP/HTTPS et bloquer certaines attaques ou requêtes malveillantes.

Exemple conceptuel :

```text
Client
  |
  | HTTP Request
  ↓
WAF
  |
  | Analyse de la requête
  ↓
Serveur Web
```

---

# 7.2.2. ACL — Access Control List

Une **ACL (Access Control List)** est une liste de règles permettant d'autoriser ou de refuser certains flux réseau.

Une ACL peut notamment être configurée sur un routeur ou un équipement de sécurité.

### ACL standard

Une **ACL standard** filtre principalement selon **l'adresse IP source**.

Exemple :

```text
Autoriser 192.168.1.0/24
Refuser le reste
```

### ACL étendue

Une **ACL étendue** permet un filtrage plus précis selon plusieurs paramètres :

* IP source ;
* IP destination ;
* protocole ;
* ports source/destination.

Exemple :

```text
Source      : 192.168.1.0/24
Destination : 10.0.0.10
Protocole   : TCP
Port        : 443
Action      : PERMIT
```

> La distinction « standard vs étendue » est notamment utilisée dans les ACL Cisco IPv4. Les possibilités exactes dépendent de l'équipement et du système réseau.

---

# 7.2.3. Proxy et Reverse Proxy

## Proxy

Un **proxy** agit comme intermédiaire entre les clients et les serveurs externes.

```text
Client
   |
   ↓
Proxy
   |
   ↓
Internet / Serveur
```

Le client communique avec le proxy, qui effectue ensuite la requête vers le serveur distant.

Un proxy peut notamment être utilisé pour :

* contrôler les accès Internet ;
* appliquer des politiques de sécurité ;
* mettre en cache certaines ressources ;
* journaliser les requêtes ;
* masquer l'adresse IP du client vis-à-vis du serveur distant.

---

## Reverse Proxy

Un **reverse proxy** est placé devant un ou plusieurs serveurs.

```text
             ┌── Serveur Web 1
Internet ── Reverse Proxy
             └── Serveur Web 2
```

Le client communique avec le reverse proxy sans nécessairement connaître directement les serveurs internes.

Il peut notamment assurer :

* la distribution du trafic ;
* le **load balancing** ;
* la terminaison TLS ;
* la mise en cache ;
* la protection et le filtrage des requêtes ;
* le routage vers différents serveurs.

Exemples de solutions pouvant fonctionner comme reverse proxy :

```text
Nginx
HAProxy
Apache HTTP Server
```

### Différence

```text
Proxy        → protège / représente les clients
Reverse Proxy → protège / représente les serveurs
```

---

# 7.2.4. VPN — Virtual Private Network

Un **VPN (Virtual Private Network)** permet de créer une communication sécurisée à travers un réseau non fiable, généralement Internet.

Le VPN crée un **tunnel** entre deux extrémités.

```text
Réseau A
   |
VPN Gateway
   |
=== Tunnel VPN chiffré ===
   |
VPN Gateway
   |
Réseau B
```

Le tunnel peut assurer notamment :

* la confidentialité ;
* l'intégrité ;
* l'authentification des parties.

---

## VPN IPsec

**IPsec** est une suite de protocoles permettant de sécuriser les communications IP.

Il peut notamment être utilisé pour créer des VPN :

```text
Site A
   |
Routeur VPN
   |
==== IPsec ====
   |
Routeur VPN
   |
Site B
```

Deux modes importants sont :

* **Transport mode** : protège principalement la charge utile IP ;
* **Tunnel mode** : encapsule le paquet IP original dans un nouveau paquet IP, très utilisé pour les VPN site-à-site.

---

## OpenVPN

**OpenVPN** est une solution VPN utilisant notamment TLS pour l'établissement sécurisé du tunnel.

Elle peut être utilisée pour :

* les connexions d'accès distant ;
* les VPN site-à-site ;
* les environnements professionnels.

---

## SSL VPN

Le terme **SSL VPN** désigne généralement des solutions VPN utilisant **TLS** pour sécuriser l'accès distant.

Elles peuvent permettre à un utilisateur distant d'accéder de manière sécurisée aux ressources internes d'une organisation.

> Comme pour HTTPS, le terme « SSL VPN » est historiquement répandu, mais les implémentations modernes utilisent généralement **TLS**.

---

# 7.3. Supervision et administration

La sécurité ne consiste pas uniquement à bloquer les attaques. Il est également nécessaire de **surveiller l'état du réseau**, détecter les anomalies et diagnostiquer les problèmes.

---

# 7.3.1. SNMP — Simple Network Management Protocol

**SNMP (Simple Network Management Protocol)** est utilisé pour superviser et administrer des équipements réseau.

Il peut notamment permettre de récupérer des informations sur :

* l'utilisation CPU ;
* la mémoire ;
* le trafic des interfaces ;
* l'état des interfaces ;
* les erreurs réseau ;
* certains compteurs de performance.

Architecture simplifiée :

```text
             SNMP
┌─────────────────────────────┐
│                             │
│     Serveur de supervision  │
│        SNMP Manager         │
│              │              │
└──────────────┼──────────────┘
               |
       ┌───────┼────────┐
       ↓       ↓        ↓
    Switch   Routeur   Serveur
    Agent    Agent     Agent
```

Les équipements supervisés exécutent généralement un **SNMP Agent**, tandis que le système de supervision joue le rôle de **Manager**.

### Ports

```text
UDP 161 → requêtes SNMP
UDP 162 → SNMP Trap / notifications
```

Une **Trap** permet notamment à un équipement d'envoyer spontanément une notification au système de supervision lorsqu'un événement se produit.

---

# 7.3.2. Wireshark

**Wireshark** est un analyseur de protocoles réseau permettant de capturer et d'examiner les paquets.

Il permet notamment d'observer :

* les adresses IP ;
* les adresses MAC ;
* les ports ;
* les protocoles ;
* les requêtes DNS ;
* les échanges TCP ;
* les paquets HTTP ;
* les erreurs et retransmissions.

Exemple de filtre Wireshark :

```text
tcp.port == 443
```

Pour afficher les paquets DNS :

```text
dns
```

Pour filtrer une adresse IP :

```text
ip.addr == 192.168.1.10
```

Wireshark est particulièrement utile pour le **diagnostic réseau** et l'analyse des communications.

---

# 7.3.3. tcpdump

**tcpdump** est un outil en ligne de commande permettant de capturer et d'analyser le trafic réseau.

Exemple :

```bash
tcpdump
```

Capturer le trafic d'une interface particulière :

```bash
tcpdump -i eth0
```

Filtrer le trafic TCP :

```bash
tcpdump tcp
```

Filtrer le trafic sur le port 443 :

```bash
tcpdump port 443
```

Wireshark fournit une interface graphique riche, tandis que `tcpdump` est particulièrement pratique sur les serveurs Linux et dans les environnements où seule une console est disponible.

---

# 7.3.4. Commandes réseau indispensables

## ping

`ping` permet principalement de tester l'accessibilité d'une destination et d'observer le temps de réponse.

```bash
ping 8.8.8.8
```

Il utilise généralement **ICMP Echo Request / Echo Reply** pour IPv4.

---

## traceroute / tracert

Permet d'observer les différents sauts traversés par les paquets jusqu'à une destination.

Sous Linux :

```bash
traceroute example.com
```

Sous Windows :

```cmd
tracert example.com
```

Le principe repose notamment sur l'utilisation progressive de valeurs de **TTL** et sur les messages ICMP générés par les routeurs intermédiaires.

---

## netstat

`netstat` permet historiquement d'afficher des informations concernant :

* les connexions réseau ;
* les ports en écoute ;
* les tables de routage ;
* certaines statistiques réseau.

Exemple :

```bash
netstat -an
```

Sur de nombreux systèmes Linux modernes, `ss` est recommandé comme alternative :

```bash
ss -tuln
```

---

## nslookup / dig

Ces commandes permettent d'interroger le système DNS.

### nslookup

Disponible notamment sous Windows :

```cmd
nslookup example.com
```

### dig

Très utilisé sous Linux et dans les environnements d'administration réseau :

```bash
dig example.com
```

Pour demander spécifiquement un enregistrement MX :

```bash
dig example.com MX
```

---

## ipconfig / ifconfig / ip addr

Ces commandes permettent d'afficher ou de gérer la configuration réseau.

### Windows

```cmd
ipconfig
```

Pour obtenir davantage d'informations :

```cmd
ipconfig /all
```

### Linux — commande moderne

```bash
ip addr
```

ou :

```bash
ip a
```

Pour afficher les routes :

```bash
ip route
```

### ifconfig

`ifconfig` est une ancienne commande Unix/Linux historiquement utilisée pour configurer les interfaces.

Elle reste présente sur certains systèmes, mais la commande `ip` est généralement privilégiée sur les distributions Linux modernes.

---

## arp

La commande `arp` permet notamment d'afficher les associations entre adresses **IPv4 et MAC** présentes dans le cache ARP.

Exemple :

```cmd
arp -a
```

On peut obtenir une information de ce type :

```text
Adresse IP       Adresse physique
192.168.1.1      AA-BB-CC-DD-EE-FF
```

Sur les systèmes Linux modernes, les informations de voisinage sont plutôt accessibles avec :

```bash
ip neigh
```

---

# Tableau récapitulatif des commandes

| Commande     | Système / environnement | Fonction principale                  |
| ------------ | ----------------------- | ------------------------------------ |
| `ping`       | Windows / Linux         | Tester l'accessibilité et la latence |
| `traceroute` | Linux / Unix            | Afficher les sauts réseau            |
| `tracert`    | Windows                 | Afficher les sauts réseau            |
| `netstat`    | Windows / Linux         | Connexions, ports et statistiques    |
| `ss`         | Linux                   | Connexions et sockets                |
| `nslookup`   | Windows / Linux         | Interroger DNS                       |
| `dig`        | Linux / Unix            | Analyse DNS détaillée                |
| `ipconfig`   | Windows                 | Configuration IP                     |
| `ip addr`    | Linux                   | Interfaces et adresses IP            |
| `ip route`   | Linux                   | Table de routage                     |
| `ifconfig`   | Ancien Linux/Unix       | Configuration des interfaces         |
| `arp`        | Windows / certains Unix | Cache ARP                            |
| `ip neigh`   | Linux                   | Table de voisinage                   |
| `tcpdump`    | Linux / Unix            | Capture réseau en ligne de commande  |

---

# À retenir

* **NAT** traduit des adresses IP entre différents espaces d'adressage.
* **PAT** permet à plusieurs machines privées de partager une même IP publique en utilisant les **ports** pour différencier les connexions.
* Un **pare-feu** contrôle le trafic selon des règles de sécurité.
* Un pare-feu **Stateful** conserve l'état des connexions.
* Un **WAF** se concentre sur la protection des applications Web.
* Une **ACL** définit des règles permettant d'autoriser ou de refuser certains flux.
* Un **proxy** représente généralement les clients, tandis qu'un **reverse proxy** représente les serveurs.
* Un **VPN** crée un tunnel sécurisé à travers un réseau non fiable.
* **IPsec**, **OpenVPN** et différentes solutions basées sur TLS peuvent être utilisés pour construire des VPN.
* **SNMP** permet de superviser les équipements et de récupérer des informations de fonctionnement.
* **Wireshark** fournit une analyse graphique détaillée des paquets ; `tcpdump` permet une capture efficace en ligne de commande.
* Les commandes `ping`, `traceroute`, `dig`, `ip`, `ss`, `tcpdump`, etc. sont essentielles pour le **diagnostic et l'administration réseau**.
