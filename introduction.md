# Travail en binome

Comme on va faire du multijoueur et que testez la VR multijoueur seul c'est pas simple.   
Je vous propose de travaillez en binome avec Git sur le meme projet.     

Rappel:
- Positionner un objet dans l'espace [->](https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr/blob/main/KISS/ReadMe.md)
- Brush 3D de la piece de Mons [->](https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr/tree/main/3D)

Savoir: 
- Afficher un address publique
- Afficher un address local
  - Retirer les IPV6
  - Retirer les IPV4
- Desactiver les pare feu
  - Ouvrir un port sur votre machine ?
  - Ouvrir un port sur votre modem ?   
- Ajouter un server UDP avec un thread dans Unity 
- Envoyer un text UDP a un ordinateur
- Envoyer un tableau de byte en UDP a un ordinateur
- Creer une liste de joueur baser sur IPV4 (ou la confience)
  - Envoyer du text et des bytes aux joueurs en retour 
- Culture general, UDP vs TCP
- Ajouter un server Websocket dans Unity
- Envoyer un text a un Webscoket
- Envoyer un tableau de byte a un Websocket
- 










--------------

# Planning brouillons

## Day 1

**Matin:** Install ALVR 
- Creer un projet Git a deux
- Creer un projet unity avec le pattern de Mixed Reality 
- Installer
  - ALVR
  - Steam VR
    - Set  Open XR 
- Faire un Hello World
- Build

**Avant-Midi:** Timer et variable
- Ajouter Mirror
- Ajouter un NetworkManager
- Creeons un Timer⌛ pour votre jeu d echec:
  - `[SyncVar]` et `[Command]` Variables synchroniser
  - `[SyncVar(hook=)]` Variable Hook

**Apres-Midi:** Hello Mirror
- Faire un player prefab avec un NetworkIdentity
- Creeons un script "Hello World"
  - [Command] Demander des choses au servers
    - [TargetRPC] Faire un Ping/Pong
    - [ClientRPC] Gandalf Sax

**Fin Journee:** [Transform]
- Attraper un object avec OpenXR
- Transforom Netwrok avec Mirror



## Day 1

Matin: Tag VR
- Creeons des singletons pour savoir 


