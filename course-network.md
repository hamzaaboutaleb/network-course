# Reseau 

# Introduction 
### Qu'est ce qu'un reseau ? 
- Un ensemble d'entites(objets,personnes,machines,etc..) interconnectees les unes avec les autres. 
- exemple : reseau de transport , reseau telephonique , reseau de neurones...

### reseau informatique : 
- un ensemble d'ordinateurs reelies entre eux grace a des lignes physiques et echangeant des informations sous forme de donnees numeriques
### interets des reseaux informatique 
- communication
- partage de ressources 
- minimisation des couts 
- ... 

### les topologies 
- En bus : tous les ordinateurs sont relies a une meme ligne de transmission.
- En etoile : tous les ordinateurs sontt relies a un concentrateur(hub)
- En anneau : les ordinateurs sontt situes sur une boucle 
- cablage en maille : chaque machine est reliee a toutes les autres par un cable 
- Question : quels sont les avantages et inc de chaque topologie ? 

### les types de reseaux 
- LAN(Local area network) : meme organisation dans une pretite aire geographique 
- MAN(Metropolitan area network) : interconnexion de plusieurs LAN geographiquement proches
- WAN : Wide area network , interconnexion de plusieurs LAN a travers de grandes distances geographiques 

![alt text](images/image.png)

### Les techniques de transfert : 

- La commutation de circuits 
- le transfertt de paquets 



# Modeles en couches 

![alt text](images/image-1.png)
### protocole : 
- un ensemble de convention preetablies pour realise un echange de donnees entre deux entites 
- il definit le format des donnees et les regles d echanges : syntaxes et semantique de message ...
- En particulier 
1. format des donnees et les regles d'echange 
2. delimitation des blocs de donnees echanges
3. organisation et controle de l'echange
4. controle de la liaison 

## modele de reference OSI : 
- Open systems Interconnection (interconnexion des systemes ouverts)
- Definit par "international standard organisation"
    - organisation non gouvernementale
    - certaine de pays membres 
    - edite des normes dans tous les domaines 
### idee fondamentale : 
- modele en chouches
- une couche : un ensemble homogene destine a accomplir une tache ou rendre un service 
- le decoupage en couche permet de : 
    - dissocier des problemes de natures differentes 
    - rendre l'architecture evolutive 
    - faire de la reutilisation 
![alt text](images/image-2.png)
![alt text](images/image-3.png)
### les couches TCP/IP : 
- Reseau : 
    - acheminement des donnees sur la liaison 
    - coordination de la transmission de donnees(synchronisation)
    - conversion des signaux(analogique/numerique)
- Internet : communication entre machine 
    - adressage IP 
    - acheminement de datagrammes
    - peu de fonctionnalite, pas de garanties 
    - gestion de la fragmentation et assemblage 
    ![alt text](images/image-4.png)
