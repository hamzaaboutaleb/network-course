# Cours Complet : La Couche Liaison de Données (Couche 2 OSI)

---

# Partie 1 — Fondamentaux de la couche Liaison

## Chapitre 1. Introduction à la couche Liaison de données

### 1. Position dans le modèle OSI et modèle TCP/IP
Dans l'architecture réseau normalisée par l'ISO (modèle OSI à 7 couches), la **couche Liaison de données** occupe la **couche 2** (Layer 2 ou L2).

* **Couche 7 :** Application
* **Couche 6 :** Présentation
* **Couche 5 :** Session
* **Couche 4 :** Transport *(ex: TCP, UDP)*
* **Couche 3 :** Réseau *(ex: IP)*
* **Couche 2 : Liaison de données** *(ex: Ethernet, Wi-Fi, PPP)*
* **Couche 1 :** Physique *(ex: Câbles, Fibres, Signal radio)*

Dans le modèle **TCP/IP** (4 ou 5 couches), elle correspond à la **couche Accès Réseau** (lorsqu'on combine les couches 1 et 2 OSI) ou directement à la couche Liaison (dans le modèle TCP/IP hybride à 5 couches).

### 2. Rôle principal de la Couche 2
La couche Liaison a pour mission de **garantir un transfert de données fiable et structuré entre deux équipements directement connectés** (voisins physiques).

Ses fonctions principales sont :
1. **Le Framage (Framing) :** Structurer les suites de bits envoyées par la couche physique sous forme de **trames** (blocs de données avec en-tête et queue).
2. **L'adressage physique (MAC) :** Identifier de manière unique la carte réseau source et la carte réseau destination sur un même segment physique.
3. **Le contrôle d'accès au support (MAC - Media Access Control) :** Gérer qui a le droit de parler sur le support physique pour éviter les collisions (ex: algorithme CSMA/CD en Ethernet).
4. **La détection et correction d'erreurs :** Vérifier si des bits ont été altérés pendant le transport physique grâce à des codes d'erreur comme le **CRC** (*Cyclic Redundancy Check*).
5. **Le contrôle de flux (optionnel) :** Empêcher un émetteur rapide de submerger un récepteur plus lent.

### 3. Différence entre Bit, Trame, Paquet et Segment (Les PDU)
Chaque couche du modèle OSI manipule des unités de données appelées **PDU** (*Protocol Data Unit*). Il est crucial de ne pas les confondre :

| Couche OSI | Nom de la PDU | Contenu / Rôle principal | Adressage utilisé |
| :--- | :--- | :--- | :--- |
| **Couche 4 (Transport)** | **Segment** (ou Datagramme) | Données applicatives + Ports source/destination | Ports (ex: 80, 443) |
| **Couche 3 (Réseau)** | **Paquet** | Segment + En-tête IP (Routage de bout en bout) | Adresses IP (ex: 192.168.1.1) |
| **Couche 2 (Liaison)** | **Trame** (*Frame*) | Paquet + En-tête L2 + Queue L2 (CRC) | Adresses MAC |
| **Couche 1 (Physique)** | **Bit** | Signal électrique, optique ou électromagnétique ($0$ et $1$) | Aucun |

> **Règle d'encapsulation :** Le **Segment** est inséré dans le **Paquet**, qui est lui-même inséré dans la **Trame**, qui est enfin convertie en **Bits** pour voyager sur le câble.

### 4. Communication entre deux équipements voisins
La couche Liaison s'intéresse **uniquement au saut par saut (Hop-by-Hop)**, contrairement à la couche Réseau (IP) qui gère le cheminement global de **bout en bout (End-to-End)**.

Lorsqu'un ordinateur A envoie des données à un serveur B via plusieurs routeurs :
* L'**adresse IP source et destination** ne changent **jamais** tout au long du trajet.
* La **trame (Couche 2)** est **détruite et réécrite à chaque routeur traversé**. Chaque lien physique (Câble Ethernet, Fibre, Wi-Fi) utilise sa propre trame avec les adresses MAC des cartes réseau immédiatement adjacentes.

### 5. Différence entre Couche Physique et Couche Liaison
* **Couche Physique (Couche 1) :**
  * Traite de la transmission brute des bits sur un canal matériel.
  * Définit les normes électriques, la tension, le type de connecteur (RJ45), les fréquences radio.
  * Ne comprend pas la signification des bits transmis.
* **Couche Liaison (Couche 2) :**
  * Donne du **sens** aux bits en les regroupant en trames.
  * Sait où commence et où finit un message.
  * Sait si le message s'adresse à elle (grâce à l'adresse MAC destination).

### 6. Notions de LAN, WAN et Transmission Point-à-Point
* **LAN (*Local Area Network*) :** Réseau local couvrant une zone géographique restreinte (maison, bureau).
  * *Technologies L2 typiques :* Ethernet (IEEE 802.3), Wi-Fi (IEEE 802.11).
  * Utilise un support partagé ou commuté avec adressage multipoint (MAC).
* **WAN (*Wide Area Network*) :** Réseau étendu couvrant de grandes distances (ex: Internet, liaison inter-sites).
  * *Technologies L2 typiques :* PPP, HDLC, Frame Relay, MPLS (couche 2.5).
* **Transmission Point-à-Point :**
  * Liaison directe reliant exactement **deux** équipements sans autre intermédiaire sur le même fil (ex: une liaison série entre 2 routeurs).
  * Dans une liaison point-à-point strict, l'adresse MAC n'est pas toujours nécessaire car tout bit envoyé par un côté est obligatoirement reçu par l'autre.

---

### Questions types de QCM (Chapitre 1)

* **Q1. Quelle couche utilise les adresses MAC ?**
  * *Réponse :* La **Couche 2** (Liaison de données).
* **Q2. Quelle couche est responsable de l'encapsulation des trames ?**
  * *Réponse :* La **Couche 2** (Liaison de données).
* **Q3. Quelle est la PDU de la couche 2 ?**
  * *Réponse :* La **Trame** (ou *Frame*).
* **Q4. Quelle différence entre une trame et un paquet ?**
  * *Réponse :* Le paquet est la PDU de couche 3 (adressage IP global, bout en bout), tandis que la trame est la PDU de couche 2 (adressage MAC local, saut par saut) englobant le paquet.

---

## Chapitre 2. Les deux sous-couches : LLC et MAC

L'organisme IEEE (Institute of Electrical and Electronics Engineers) a divisé la couche Liaison (Couche 2) des réseaux locaux en deux sous-couches distinctes : la sous-couche haute **LLC** et la sous-couche basse **MAC**.

```
+-------------------------------------------------------+
|                Couche 3 : Réseau (IP)                 |
+-------------------------------------------------------+
| Couche 2 : | LLC (Logical Link Control - IEEE 802.2)  |
| Liaison    |------------------------------------------|
|            | MAC (Media Access Control - IEEE 802.3/11)|
+-------------------------------------------------------+
|                Couche 1 : Physique                    |
+-------------------------------------------------------+
```

### 1. LLC — Logical Link Control (IEEE 802.2)
La sous-couche LLC est la partie **indépendante du support physique**.

* **Norme :** IEEE 802.2.
* **Interface avec la couche réseau :** Elle fait le pont entre la couche 3 (Réseau) et le matériel sous-jacent.
* **Identification du protocole supérieur :** Elle indique à quel protocole de couche 3 remettre le paquet une fois décapsulé (ex: IPv4, IPv6, ARP) grâce aux champs **DSAP** (*Destination Service Access Point*) et **SSAP** (*Source Service Access Point*), ou via l'en-tête SNAP.
* **Fonctions optionnelles :** Contrôle de flux et réémission d'erreurs au niveau local.

### 2. MAC — Media Access Control (IEEE 802.x)
La sous-couche MAC est la partie **dépendante du support matériel** (Ethernet, Wi-Fi, Bluetooth).

* **Normes :** IEEE 802.3 (Ethernet), IEEE 802.11 (Wi-Fi), IEEE 802.15 (Bluetooth).
* **Adressage physique :** Gestion et intégration des adresses MAC de source et de destination.
* **Contrôle d'accès au support :** Détermine qui a le droit d'émettre sur le média à un instant $t$ (CSMA/CD pour Ethernet, CSMA/CA pour le Wi-Fi).
* **Construction de la trame :** Assemblage des bits de cadrage, adresses, données et calcul du champ **FCS** (*Frame Check Sequence*) pour la détection d'erreurs.

---

### Questions types de QCM (Chapitre 2)

* **Q1. Quelle sous-couche gère les adresses MAC ?**
  * *Réponse :* La sous-couche **MAC** (*Media Access Control*).
* **Q2. Quelle sous-couche fait l'interface avec la couche réseau ?**
  * *Réponse :* La sous-couche **LLC** (*Logical Link Control*).
* **Q3. Quelle norme définit LLC ?**
  * *Réponse :* La norme **IEEE 802.2**.
* **Q4. Quelle est la différence entre LLC et MAC ?**
  * *Réponse :* LLC est logicielle et indépendante du média (interface avec L3), tandis que MAC est matérielle et dépendante du média (gestion du support et adresses physiques).

---

## Chapitre 3. L'adressage MAC

### 1. Structure d'une adresse MAC
* Une adresse MAC (ou adresse physique) a une taille de **48 bits**, soit **6 octets**.
* Elle est représentée sous forme hexadécimale (ex: `00:1A:2B:3C:4D:5E` ou `00-1A-2B-3C-4D-5E`).
* Les 48 bits sont divisés en deux parties de 24 bits (3 octets) chacune :
  1. **OUI (*Organizationally Unique Identifier*) :** Les 24 premiers bits (3 premiers octets). Attribués par l'IEEE au constructeur de la carte réseau (ex: Cisco, Intel, Realtek).
  2. **Numéro de série / NIC :** Les 24 derniers bits (3 derniers octets). Attribués de manière unique par le fabricant à chaque carte.

```
|<- - - - - - - 24 bits (OUI) - - - - - ->|<- - - - - 24 bits (Extension) - - - - ->|
+-----------------------------------------+-----------------------------------------+
|     Identifiant du Constructeur         |      Numéro de série de la carte        |
+-----------------------------------------+-----------------------------------------+
```

### 2. Bits spécifiques : Bit I/G et Bit U/L
Dans le tout premier octet de l'adresse MAC (octet le plus à gauche) :

* **Bit I/G (Individual / Group - Bit 0 de l'octet 1) :**
  * **$0$ (Individual) :** Adresse **Unicast** (s'adresse à une seule interface spécifique).
  * **$1$ (Group) :** Adresse **Multicast** ou **Broadcast** (s'adresse à un groupe ou à tous).
* **Bit U/L (Universal / Local - Bit 1 de l'octet 1) :**
  * **$0$ (Universal) :** Adresse attribuée globalement par le fabricant (garantie unique au monde).
  * **$1$ (Local) :** Adresse modifiée ou attribuée localement par un administrateur réseau (adresse virtuelle).

### 3. Types d'adresses MAC
1. **Unicast :** Destinée à un seul équipement. Le bit I/G est à `0`. (Ex: `00:1A:2B:3C:4D:5E`)
2. **Multicast :** Destinée à un groupe d'équipements abonnés. Le bit I/G est à `1`. En IPv4 Ethernet, les adresses multicast MAC commencent toujours par `01:00:5E`.
3. **Broadcast (Diffusion) :** Destinée à **TOUS** les équipements du même domaine de broadcast.
   * L'adresse MAC de broadcast est composée de tous les bits à 1 : **`FF:FF:FF:FF:FF:FF`**.

---

### Questions types de QCM (Chapitre 3)

* **Q1. Combien de bits contient une adresse MAC ?**
  * *Réponse :* **48 bits** (soit 6 octets).
* **Q2. Que signifie I/G = 1 ?**
  * *Réponse :* Il s'agit d'une adresse de **Groupe** (Multicast ou Broadcast).
* **Q3. Que signifie U/L = 1 ?**
  * *Réponse :* L'adresse est gérée **Localement** (adresse administrée localement).
* **Q4. Quelle est l'adresse MAC de broadcast ?**
  * *Réponse :* **`FF:FF:FF:FF:FF:FF`**.
* **Q5. Quelle différence entre unicast et multicast ?**
  * *Réponse :* Unicast envoie un message à **un seul récepteur précis**, tandis que Multicast l'envoie à un **groupe sélectionné de récepteurs**.

---

## Chapitre 4. La trame Ethernet

Le format de trame de couche 2 le plus répandu au monde est le format **Ethernet II** (ou DIX Ethernet).

### 1. Format détaillé d'une trame Ethernet II

```
+------------+-----+-----------------+---------------+-----------+---------------+-----+
| Préambule  | SFD | MAC Destination |  MAC Source   | EtherType |    Données    | FCS |
|  7 octets  | 1 o |    6 octets     |   6 octets    | 2 octets  | 46-1500 octets| 4 o |
+------------+-----+-----------------+---------------+-----------+---------------+-----+
```

* **Préambule (7 octets) :** Séquence de bits alternés `10101010` permettant d'harmoniser l'horloge de transmission entre l'émetteur et le récepteur.
* **SFD (*Start Frame Delimiter*, 1 octet) :** Contient le motif `10101011`. Il alerte le récepteur que l'en-tête de la trame commence immédiatement au bit suivant.
* **MAC Destination (6 octets) :** Adresse physique de l'interface qui doit recevoir la trame.
* **MAC Source (6 octets) :** Adresse physique de l'interface qui a émis la trame.
* **EtherType (2 octets) :** Identifie le protocole de couche 3 transporté dans le champ Données (ex: `0x0800` pour IPv4, `0x86DD` pour IPv6, `0x0806` pour ARP).
* **Données et Bourrage / Padding (46 à 1500 octets) :** Le paquet réseau (PDU L3). Si le paquet fait moins de 46 octets, des bits de bourrage (*padding*) sont ajoutés pour atteindre la taille minimale imposée.
* **FCS (*Frame Check Sequence*, 4 octets) :** Valeur calculée par l'émetteur via l'algorithme **CRC-32**. Permet au récepteur de vérifier l'intégrité de la trame.

### 2. Tailles limites d'une trame Ethernet
* **Taille minimale d'une trame : 64 octets** (comprenant l'en-tête MAC, l'EtherType, 46 octets de données minimum et le FCS). *Note : le préambule et le SFD ne sont pas comptés dans cette taille.*
  * Une trame plus courte que 64 octets est appelée un **Runt frame** (souvent due à une collision).
* **Taille maximale d'une trame standard : 1518 octets** (64 octets d'en-tête/FCS + 1500 octets de données MTU).
  * Avec le marquage VLAN IEEE 802.1Q (4 octets supplémentaires), la taille maximale passe à **1522 octets**.
  * Une trame dépassant cette limite est appelée un **Giant frame**.

### 3. Différence Ethernet II vs IEEE 802.3
* **Ethernet II :** Utilise le champ **EtherType** (valeur $\ge 0x0600$ ou $1536$ en décimal) pour indiquer le protocole supérieur.
* **IEEE 802.3 :** Remplace l'EtherType par un champ **Longueur / Length** (valeur $\le 1500$). La détermination du protocole de couche supérieure est alors déléguée à l'en-tête LLC/SNAP.

---

### Questions types de QCM (Chapitre 4)

* **Q1. Quelle est la taille minimale d'une trame Ethernet ?**
  * *Réponse :* **64 octets**.
* **Q2. Quel champ permet de détecter les erreurs ?**
  * *Réponse :* Le champ **FCS** (*Frame Check Sequence*), utilisant l'algorithme CRC.
* **Q3. Quel est le rôle de l'EtherType ?**
  * *Réponse :* Identifier le protocole de couche 3 encapsulé dans le champ données (ex: IPv4, IPv6).
* **Q4. Quelle différence entre préambule et SFD ?**
  * *Réponse :* Le préambule (7 octets) synchronise l'horloge ; le SFD (1 octet, se terminant par `11`) signale le début exact de la trame.
* **Q5. Quelle est la taille maximale d'une trame Ethernet classique ?**
  * *Réponse :* **1518 octets** (sans Tag VLAN) ou **1522 octets** (avec Tag 802.1Q).

---

# Partie 2 — Transmission et fiabilité

## Chapitre 5. Détection et correction des erreurs

### 1. Le problème des erreurs de transmission
Pendant la transmission physique, le bruit électromagnétique ou les interférences peuvent inverser des bits ($0 \to 1$ ou $1 \to 0$).
* **Erreur simple :** Un seul bit est altéré dans tout le bloc.
* **Erreur en rafale (*Burst error*) :** Plusieurs bits consécutifs sont altérés.

### 2. Mécanismes de contrôle
* **Bit de parité :** Un bit supplémentaire est ajouté à un bloc de données.
  * **Parité paire :** Le bit est positionné de sorte que le nombre total de $1$ soit **pair**.
  * **Parité impaire :** Le bit est positionné de sorte que le nombre total de $1$ soit **impair**.
  * *Limite :* Ne détecte que les erreurs portant sur un nombre impair de bits.
* **Checksum (Somme de contrôle) :** Addition de mots de données (utilisé principalement en L3/L4 comme dans l'en-tête IP/TCP).
* **CRC (*Cyclic Redundancy Check*) :** Calcul polynomial binaire effectué sur les bits de la trame. Le résultat est inséré dans le champ **FCS**. C'est le système le plus puissant pour détecter les erreurs en couche 2.

### 3. Distance de Hamming et Formules Indispensables
La **distance de Hamming** ($d$) entre deux mots de code est le nombre de positions de bits pour lesquelles les deux mots diffèrent. La distance de Hamming minimale ($d_{\min}$) d'un code détermine ses capacités de détection et de correction :

1. **Nombre d'erreurs décelables / détectables ($E_{\text{détection}}$) :**
$$E_{\text{détection}} = d_{\min} - 1$$

2. **Nombre d'erreurs corrigeables ($E_{\text{correction}}$) :**
$$E_{\text{correction}} = \left\lfloor \frac{d_{\min} - 1}{2} \right\rfloor$$

#### Exemple d'application :
Si $d_{\min} = 5$ :
* $E_{\text{détection}} = 5 - 1 = 4$ (on peut détecter jusqu'à 4 bits altérés).
* $E_{\text{correction}} = \left\lfloor \frac{5 - 1}{2} \right\rfloor = \left\lfloor 2 \right\rfloor = 2$ (on peut corriger jusqu'à 2 bits altérés).

---

### Questions types de QCM (Chapitre 5)

* **Q1. Quelle différence entre CRC et checksum ?**
  * *Réponse :* Le CRC utilise une division polynomiale binaire (très robuste contre les erreurs en rafale, idéal en L2), alors que le checksum fait une somme arithmétique d'octets.
* **Q2. Combien d'erreurs peut-on détecter avec $d_{\min}=4$ ?**
  * *Réponse :* $E_{\text{détection}} = 4 - 1 = \mathbf{3}$ **erreurs**.
* **Q3. Combien d'erreurs peut-on corriger avec $d_{\min}=5$ ?**
  * *Réponse :* $E_{\text{correction}} = \lfloor (5 - 1) / 2 \rfloor = \mathbf{2}$ **erreurs**.
* **Q4. Quel mécanisme utilise le champ FCS ?**
  * *Réponse :* Le calcul polynomial **CRC** (*Cyclic Redundancy Check*).

---

## Chapitre 6. Contrôle de flux et contrôle d'erreurs

### 1. Contrôle de flux vs Contrôle d'erreurs
* **Contrôle de flux :** Empêche l'émetteur de soumettre plus de données que le récepteur n'est capable d'en traiter ou d'en stocker dans sa mémoire tampon (Buffer).
* **Contrôle d'erreurs :** Assure que toutes les trames sont livrées sans erreur et dans l'ordre. Repose sur le mécanisme **ARQ** (*Automatic Repeat reQuest*) combinant des accusés de réception (**ACK**), des accusés négatifs (**NACK**) et des temporisateurs (*Timeouts*).

### 2. Les différents protocoles ARQ
1. **Stop-and-Wait (Arrêt et Attente) :**
   * L'émetteur envoie 1 trame puis s'arrête en attendant l'ACK du récepteur.
   * Si la trame ou l'ACK est perdu, après expiration du *timeout*, la trame est réémise.
   * *Inconvénient :* Très inefficace, mauvaise utilisation de la bande passante.
2. **Go-Back-N (Rejet d'ensemble) :**
   * L'émetteur peut envoyer plusieurs trames (taille de la fenêtre $W > 1$) sans attendre ACK.
   * Le récepteur n'accepte les trames que **dans l'ordre strict**.
   * Si la trame $N$ est perdue, toutes les trames suivantes ($N+1, N+2, \dots$) sont rejetées. L'émetteur doit retransmettre **toutes** les trames à partir de la trame $N$.
3. **Selective Repeat (Rejet sélectif) :**
   * Le récepteur dispose d'un buffer et accepte les trames arrivées hors ordre.
   * Seule la trame manquante ou erronée est réémise par l'émetteur.
   * Plus efficace mais nécessite plus de mémoire sur le récepteur.

---

### Questions types de QCM (Chapitre 6)

* **Q1. Quelle différence entre contrôle de flux et contrôle d'erreurs ?**
  * *Réponse :* Le contrôle de flux régule la vitesse d'émission pour éviter de submerger le récepteur. Le contrôle d'erreurs garantit la réémission des données perdues ou corrompues.
* **Q2. Quel mécanisme retransmet toutes les trames à partir de celle qui est perdue ?**
  * *Réponse :* **Go-Back-N**.
* **Q3. Quelle méthode retransmet uniquement les trames erronées ?**
  * *Réponse :* **Selective Repeat** (Rejet sélectif).
* **Q4. À quoi sert un ACK ?**
  * *Réponse :* À confirmer au récepteur la bonne réception d'une ou plusieurs trames.

---

## Chapitre 7. Les méthodes d'accès au support

Sur un support de transmission partagé (ex: câble coaxial, Wi-Fi, concentrateur/hub), deux émissions simultanées provoquent une **collision** qui rend les signaux inaudibles.

### 1. CSMA/CD (*Carrier Sense Multiple Access with Collision Detection*)
* Utilisé dans les réseaux **Ethernet filaires partagés (Half-Duplex)**.
* **Principe :**
  1. *Carrier Sense :* L'équipement écoute le support. S'il est libre, il émet.
  2. *Collision Detection :* Pendant l'émission, il continue d'écouter. S'il détecte un changement de tension (collision) :
  3. Il stoppe immédiatement son émission et envoie un signal de bourrage (*Jam Signal*).
  4. Il attend un temps aléatoire calculé par l'algorithme **BEB** (*Binary Exponential Backoff*) avant de réessayer.

### 2. CSMA/CA (*Carrier Sense Multiple Access with Collision Avoidance*)
* Utilisé dans les réseaux sans fil **Wi-Fi (IEEE 802.11)** car une carte Wi-Fi ne peut pas écouter et émettre en même temps (détection de collision impossible).
* **Principe :**
  * Écoute du canal. S'il est libre, il attend un temps supplémentaire fixé (**IFS** / **DIFS**) puis envoie une demande d'émission (**RTS** - *Request to Send*).
  * Si le point d'accès répond par un **CTS** (*Clear to Send*), la transmission démarre.

### 3. Autres méthodes d'accès
* **ALOHA / Slotted ALOHA :** Protocoles historiques d'accès aléatoire. Slotted ALOHA divise le temps en créneaux (*slots*).
* **Token Passing (Jeton test) :** Utilisé dans Token Ring (IEEE 802.5). Un jeton circule sur le réseau. Seul l'équipement possédant le jeton a le droit d'émettre. **Garanti sans collision.**

### 4. Modes de transmission et domaines
* **Half-Duplex :** Transmission bidirectionnelle mais **non simultanée** (ex: Walkie-talkie, Ethernet avec Hub). Collisions possibles.
* **Full-Duplex :** Transmission bidirectionnelle **simultanée** sur des canaux séparés (émission et réception). **Collisions impossibles.**
* **Domaine de collision :** Zone du réseau dans laquelle des trames émises simultanément peuvent entrer en collision. Un **Switch** ou un **Routeur** isole les domaines de collision sur chaque port. Un **Hub** regroupe tous ses ports dans un seul domaine de collision.

---

### Questions types de QCM (Chapitre 7)

* **Q1. Quel mécanisme est utilisé dans Ethernet partagé traditionnel ?**
  * *Réponse :* **CSMA/CD**.
* **Q2. Quel mécanisme est utilisé par le Wi-Fi pour éviter les collisions ?**
  * *Réponse :* **CSMA/CA**.
* **Q3. Quelle différence entre CSMA/CD et CSMA/CA ?**
  * *Réponse :* CSMA/CD **détecte** les collisions *pendant* l'émission, alors que CSMA/CA tente de les **éviter** *avant* l'émission.
* **Q4. En Full-Duplex, peut-on avoir des collisions Ethernet ?**
  * *Réponse :* **Non**, car les lignes d'émission et de réception sont physiquement séparées.

---

# Partie 3 — Les protocoles de liaison

## Chapitre 8. HDLC (High-Level Data Link Control)

HDLC est un protocole de couche 2 **orienté bit**, synchrone, principalement utilisé sur des liaisons point-à-point WAN.

### 1. Structure de la trame HDLC

```
+------------+------------+------------+------------------+------------+------------+
|    Flag    |  Address   |  Control   | Data / Payload   |    FCS     |    Flag    |
|  8 bits    |   8 bits   | 8/16 bits  | Variable         | 16/32 bits |   8 bits   |
+------------+------------+------------+------------------+------------+------------+
```

* **Flag (Fanion) :** Motif binaire fixe d'ouverture et de fermeture : **`01111110`** (ou `0x7E`).

### 2. Le mécanisme de Bit Stuffing (Remplissage de bit)
Pour éviter qu'une suite de données utilisateurs ne soit confondue avec le Flag `01111110` :
* **Émission (Stuffing) :** L'émetteur insère automatiquement un **`0`** après toute séquence de **5 bits `1` consécutifs** dans le corps de la trame.
* **Réception (Destuffing) :** Le récepteur supprime tout bit `0` situé immédiatement après 5 bits `1` consécutifs.

### 3. Les trois types de trames HDLC (Champ Control)
1. **Trame I (Information) :** Transporte les données de l'utilisateur (couche supérieure) et gère l'acquittement des trames.
2. **Trame S (Supervisory / Surveillance) :** Gère le contrôle de flux et d'erreurs (ACK, NACK, Ready, Reject). Ne transporte **pas** de données.
3. **Trame U (Unnumbered / Non numérotée) :** Gère l'établissement, la négociation et la fermeture de la liaison réseau.

---

### Questions types de QCM (Chapitre 8)

* **Q1. Quelle est la valeur du Flag HDLC ?**
  * *Réponse :* **`01111110`** (`0x7E`).
* **Q2. Après combien de bits 1 insère-t-on un 0 lors du bit stuffing ?**
  * *Réponse :* Après **5 bits `1` consécutifs**.
* **Q3. Combien existe-t-il de types de trames HDLC ?**
  * *Réponse :* **3 types** (I-Frame, S-Frame, U-Frame).
* **Q4. Quel est le rôle d'une trame S ?**
  * *Réponse :* Assurer la surveillance, le contrôle de flux et le contrôle d'erreurs (ACK/NACK).
* **Q5. Quelle trame transporte les données utilisateur ?**
  * *Réponse :* La **Trame I** (*Information Frame*).

---

## Chapitre 9. PPP (Point-to-Point Protocol)

PPP est le protocole standard le plus utilisé pour établir une liaison point-à-point (WAN, connexions modems, xDSL via PPPoE).

### 1. Composants majeurs de PPP
PPP repose sur trois piliers :
1. **Encapsulation de données :** Format de trame semblable à HDLC.
2. **LCP (*Link Control Protocol*) :** Établit, configure, teste et ferme la liaison de couche 2.
3. **NCP (*Network Control Protocol*) :** Famille de sous-protocoles permettant d'établir et de configurer les protocoles de couche 3 (ex: IPCP pour attribuer une IP).

### 2. Authentification sous PPP
PPP prend en charge l'authentification native du client via 2 protocoles :
* **PAP (*Password Authentication Protocol*) :**
  * Authentification basique en 2 étapes.
  * Mot de passe transmis **en texte clair** sur la ligne (non sécurisé).
* **CHAP (*Challenge Handshake Authentication Protocol*) :**
  * Authentification sécurisée en 3 étapes (Challenge, Response, Success).
  * Le mot de passe n'est **jamais transmis sur le réseau** (utilisation du hachage MD5).

### 3. PPPoE (*PPP over Ethernet*)
Permet de kapsuler des trames PPP à l'intérieur de trames Ethernet (courant pour les abonnements Internet FAI).

---

### Questions types de QCM (Chapitre 9)

* **Q1. PPP appartient à quelle couche ?**
  * *Réponse :* La **Couche 2** (Liaison de données).
* **Q2. Quel protocole établit et configure la liaison physique/liaison dans PPP ?**
  * *Réponse :* **LCP** (*Link Control Protocol*).
* **Q3. Quel protocole configure les protocoles réseau (L3) ?**
  * *Réponse :* **NCP** (*Network Control Protocol*).
* **Q4. Quelle différence entre PAP et CHAP ?**
  * *Réponse :* PAP transmet le mot de passe en clair ; CHAP est sécurisé et valide l'identité via un mécanisme de challenge-réponse cryptographique.
* **Q5. PPP utilise-t-il les adresses MAC ?**
  * *Réponse :* **Non**, sur une liaison point-à-point pure PPP, l'adresse physique est inutile car il n'y a qu'un seul destinataire possible au bout du fil.

---

# Partie 4 — Commutation et réseaux locaux

## Chapitre 10. Commutation Ethernet (Switching)

### 1. Rôle du Switch et comparaison des équipements
* **Hub (Concentrateur - Couche 1) :** Répète aveuglément tous les signaux reçus sur tous ses ports. 1 seul domaine de collision, 1 seul domaine de broadcast.
* **Switch (Commutateur - Couche 2) :** Analyse l'adresse MAC destination de la trame et l'oriente vers le port précis. **Sépare les domaines de collision** (1 par port).
* **Routeur (Couche 3) :** Interconnecte des réseaux différents basés sur les adresses IP. **Sépare les domaines de broadcast**.

### 2. Fonctionnement du Switch et Table MAC (CAM Table)
Un switch construit dynamiquement une table d'association entre les adresses MAC et ses ports physiques :
1. **Apprentissage (*Learning*) :** Le switch lit l'**adresse MAC Source** de chaque trame arrivante et l'associe dans sa table CAM au port sur lequel elle est arrivée.
2. **Commutation (*Forwarding / Filtering*) :** Le switch lit l'**adresse MAC Destination** :
   * Si l'adresse est connue dans la table CAM sur un port différent $\to$ Transmise uniquement sur ce port (**Forwarding**).
   * Si l'adresse destination est sur le même port $\to$ Trame ignorée (**Filtering**).
3. **Inondation (*Flooding*) :** Si l'adresse MAC Destination est **inconnue** (ou s'il s'agit d'une adresse de Broadcast `FF:FF:FF:FF:FF:FF`), le switch duplicate et renvoie la trame sur **tous les ports sauf le port d'entrée**.

### 3. Modes de commutation (*Switching Modes*)
* **Store-and-Forward :** Reçoit la trame **entièrement**, vérifie le CRC (FCS). Si la trame est valide, il la retransmet. *Sécurisé mais ajoute de la latence.*
* **Cut-Through :** Lit uniquement les 6 premiers octets (MAC Destination) et commence à retransmettre **immédiatement**. *Très rapide mais retransmet les trames corrompues.*
* **Fragment-Free :** Lit les 64 premiers octets avant de commuer (évite de retransmettre les *Runt frames* causées par les collisions).

---

### Questions types de QCM (Chapitre 10)

* **Q1. Comment un switch apprend-il les adresses MAC ?**
  * *Réponse :* En examinant l'**adresse MAC Source** des trames arrivant sur ses ports.
* **Q2. Que fait un switch lorsqu'il ne connaît pas l'adresse MAC destination ?**
  * *Réponse :* Il effectue une inondation (**Flooding**) sur tous les ports sauf le port source.
* **Q3. Quelle différence entre hub et switch ?**
  * *Réponse :* Le hub travaille en L1 et diffuse tout le trafic à tout le monde ; le switch travaille en L2 et achemine le trafic spécifiquement vers le port de destination.
* **Q4. Un switch sépare-t-il les domaines de collision ?**
  * *Réponse :* **Oui**, chaque port d'un switch constitue un domaine de collision propre.
* **Q5. Un routeur sépare-t-il les domaines de broadcast ?**
  * *Réponse :* **Oui**, un routeur ne transfère pas les broadcasts de couche 2 par défaut.

---

## Chapitre 11. VLAN, STP et agrégation de liens

### A. VLAN (*Virtual Local Area Network*)
Un VLAN est un réseau local **logique** indépendant configuré sur un même switch physique.
* **Rôle :** Séparer logiquement le trafic, augmenter la sécurité et **réduire la taille des domaines de broadcast**.
* **Norme IEEE 802.1Q :** Insère un champ de **Tagging** de 4 octets dans l'en-tête de la trame Ethernet.
  * Contient le **VLAN ID** codé sur **12 bits** (soit $2^{12} = 4096$ VLANs théoriques, de 0 à 4095).
* **Ports Access vs Trunk :**
  * **Access Port :** Transport le trafic d'un **seul** VLAN (trames non taguées/untagged pour l'équipement final).
  * **Trunk Port :** Transporte le trafic de **plusieurs** VLANs entre switchs (trames taguées/tagged).
* **VLAN Naïf (*Native VLAN*) :** Sur un lien Trunk, le trafic du VLAN natif transite **sans marquage/tag 802.1Q**.

### B. STP (*Spanning Tree Protocol*)
* **Rôle :** Éviter les **boucles physiques de Niveau 2** dans un réseau redondant (qui provoquent des tempêtes de broadcast / *Broadcast Storms* et gèlent le réseau).
* **Norme :** IEEE 802.1D (STP classique) / IEEE 802.1w (RSTP - Rapid STP).
* **Fonctionnement :**
  1. Élection d'un **Root Bridge** (Commutateur Racine) possédant le **Bridge ID** le plus faible (Priorité + Adresse MAC).
  2. Sélection des ports racine (**Root Ports**) et ports désignés (**Designated Ports**).
  3. Blocage des ports redondants (**Blocking State**).

### C. Agrégation de liens (EtherChannel / LACP)
* **Rôle :** Associer plusieurs liaisons physiques en une seule liaison logique pour **augmenter la bande passante** et offrir de la **redondance**.
* **Normes :**
  * **LACP (IEEE 802.1AX / 802.3ad) :** Protocole ouvert / standard.
  * **PAgP :** Protocole propriétaire Cisco.

---

### Questions types de QCM (Chapitre 11)

* **Q1. Quelle norme définit les VLAN ?**
  * *Réponse :* **IEEE 802.1Q**.
* **Q2. Quelle est la taille du champ VLAN ID ?**
  * *Réponse :* **12 bits**.
* **Q3. Combien de VLAN IDs sont disponibles théoriquement dans l'espace 12 bits ?**
  * *Réponse :* **4096** (valeurs de 0 à 4095).
* **Q4. Quel est le rôle du Root Bridge dans STP ?**
  * *Réponse :* Servir de point de référence logique central pour le calcul de l'arbre Spanning Tree sans boucle.
* **Q5. Pourquoi utilise-t-on STP ?**
  * *Réponse :* Pour **éliminer les boucles de couche 2** dans les topologies de switchs redondantes.
* **Q6. Quelle différence entre LACP et STP ?**
  * *Réponse :* LACP agrège plusieurs liens pour cumuler leur débit ; STP bloque les liens redondants pour éviter les boucles.

---

## Chapitre 12. Les normes IEEE 802 à connaître

Tableau récapitulatif des normes indispensables à mémoriser pour les QCM :

| Norme IEEE | Domaine / Fonction principale |
| :--- | :--- |
| **IEEE 802.1** | Architecture et gestion des réseaux locaux LAN |
| **IEEE 802.1D** | STP classique (*Spanning Tree Protocol*) |
| **IEEE 802.1Q** | Tagging des VLAN |
| **IEEE 802.1w** | RSTP (*Rapid Spanning Tree Protocol*) |
| **IEEE 802.1X** | Contrôle d'accès réseau basé sur les ports (Authentification) |
| **IEEE 802.1AX** | Agrégation de liens (LACP) |
| **IEEE 802.2** | Sous-couche LLC (*Logical Link Control*) |
| **IEEE 802.3** | Ethernet filaire |
| **IEEE 802.3u** | Fast Ethernet (100 Mbit/s) |
| **IEEE 802.3ab** | Gigabit Ethernet sur câble cuivre (1000BASE-T) |
| **IEEE 802.3z** | Gigabit Ethernet sur fibre optique |
| **IEEE 802.3ae** | 10 Gigabit Ethernet |
| **IEEE 802.11** | Réseaux locaux sans fil (Wi-Fi) |
| **IEEE 802.15** | Réseaux personnels sans fil (WPAN - ex: Bluetooth) |

---

# Partie 5 — Les notions transversales et les pièges des QCM

| Notion | Définition / Point clé à mémoriser |
| :--- | :--- |
| **Encapsulation** | Processus d'ajout des en-têtes/queues de contrôle lors de la descente des données de L7 vers L1. |
| **Décapsulation** | Retrait des en-têtes au niveau du récepteur lors de la remontée de L1 vers L7. |
| **MTU (*Maximum Transmission Unit*)** | Taille maximale du paquet de couche 3 (ex: 1500 octets pour IP sur Ethernet). |
| **CRC (*Cyclic Redundancy Check*)** | Algorithme mathématique de contrôle par division polynomiale. |
| **FCS (*Frame Check Sequence*)** | Le champ à la fin de la trame L2 qui contient le résultat du calcul du CRC. |
| **PDU (*Protocol Data Unit*)** | Nom générique du bloc de données à une couche donnée (Bit, Trame, Paquet, Segment). |
| **Unicast** | Envoi à un seul destinataire unique. |
| **Multicast** | Envoi à un groupe ciblé d'équipements abonnés. |
| **Broadcast** | Diffusion générale à tous les équipements du domaine de broadcast (`FF:FF:FF:FF:FF:FF`). |
| **MAC** | Identifiant physique unique de 48 bits gravé en carte réseau. |
| **ARP (*Address Resolution Protocol*)** | Protocole qui résout une adresse IPv4 connue en une adresse MAC inconnue. |
| **Collision** | Événement destructeur se produisant quand deux cartes émettent en même temps sur un média partagé. |
| **Duplex** | Mode de communication : **Half-Duplex** (un à la fois) ou **Full-Duplex** (simultané). |

---

# Partie 6 — Formules, valeurs et chiffres à mémoriser

Fiche synthétique de révision rapide :

```
======================================================================
               FICHE DE MÉMORISATION EXPRESS POUR QCM
======================================================================
• Taille adresse MAC                    : 48 bits (6 octets)
• Taille adresse IPv4                   : 32 bits (4 octets)
• Taille adresse IPv6                   : 128 bits (16 octets)
----------------------------------------------------------------------
• Fanion / Flag HDLC                    : 8 bits (Valeur : 01111110 ou 0x7E)
• Insertion de zéro HDLC (Bit Stuffing) : Après 5 bits '1' consécutifs
----------------------------------------------------------------------
• Taille Trame Ethernet minimale        : 64 octets
• Taille Trame Ethernet maximale std    : 1518 octets (1522 octets avec Tag 802.1Q)
• Taille minimale des données (Padding) : 46 octets
• MTU Ethernet classique                : 1500 octets
----------------------------------------------------------------------
• Champ VLAN ID (IEEE 802.1Q)           : 12 bits
• Nombre de VLAN IDs théoriques         : 4096 (0 à 4095)
----------------------------------------------------------------------
• Nombre d'erreurs décelables (Hamming) : E_détection = d_min - 1
• Nombre d'erreurs corrigeables         : E_correction = floor((d_min - 1) / 2)
======================================================================
```