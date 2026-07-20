# Travail en binôme

Comme on va faire du multijoueur et que tester la VR multijoueur seul, ce n'est pas simple.  
Je vous propose de travailler en binôme avec Git sur le même projet.

Comme Vincent finira par faire un jeu de plateau en VR sur une table ronde un jour dans le futur.
Le cours va avoir lieu sur son PC et celui de George comme binôme.

_Rappel:_
- Précédemment: https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr/ 
- Positionner un objet dans l'espace [->](https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr/blob/main/KISS/ReadMe.md)
- Brush 3D de la pièce de Mons [->](https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr/tree/main/3D)

**Faire un jeu Steam VR avec ALVR :**

> ALVR tourne bien sur des patates à faire griller.
 
- Installer SteamVR sur Steam. [->](https://github.com/EloiStree/HelloUnityMirror/tree/main/step_by_step/workshop_mons/000_install_steam_vr_on_window)
- Installer ALVR sur Windows. [->](https://github.com/EloiStree/HelloUnityMirror/tree/main/step_by_step/workshop_mons/001_install_alvr_on_window)
- Installer ALVR sur Quest 3 depuis le Store.
  - Installer ALVR et F-Droid depuis SCRCPY [->](https://github.com/EloiStree/HelloUnityMirror/tree/main/step_by_step/workshop_mons/002_install_scrcpy_alvr_fdroid)
- Créer un projet Unity VR sans Meta SDK. [->](https://github.com/EloiStree/HelloUnityMirror/tree/main/step_by_step/workshop_mons/003_create_unity_open_xr_project)
- Bonus : Parlons de Virtual Desktop. [->](https://github.com/EloiStree/HelloUnityMirror/tree/main/step_by_step/workshop_mons/004_use_virtual_desktop) 

**Les bases du réseau multiplateforme et multi-engine :**
- Ajouter la boîte à outils [Tick](https://github.com/EloiStree/2025_06_02_upm_tick_collection) et Mirror [->](https://github.com/EloiStree/HelloUnityMirror/tree/main/step_by_step/workshop_mons/005_empty_project_with_mirror_and_tick)
  - Ajouter un `Awake`, un `Enable` et un `Tick` toutes les N secondes pour les futurs tests.
- Afficher une adresse publique.
- Afficher une adresse locale.
  - Retirer les IPv6.
  - Retirer les IPv4.
- Désactiver les pare-feu.
  - Ouvrir un port sur votre machine ?
  - Ouvrir un port sur votre modem ?
- Ajouter un serveur UDP avec un thread dans Unity.
  - C'est quoi un conflit avec le thread Unity ?
- Envoyer un texte UDP à un ordinateur.
- Envoyer un tableau de bytes en UDP à un ordinateur.
- Créer une liste de joueurs basée sur les IPv4 (ou la confiance).
  - Envoyer du texte et des bytes aux joueurs en retour.
- Culture générale : UDP vs TCP.
- Ajouter un serveur WebSocket dans Unity.
- Envoyer un texte à un WebSocket.
- Envoyer un tableau de bytes à un WebSocket.
- Recevoir du texte depuis un WebSocket.
- Culture générale : différents réseaux client/serveur.
  - WebRTC, WebTransport, MQTT, Socket.IO.
  - Kyber (QUIC et WebTransport).
  - UDP vs TCP.
  - KCP de Mirror Transport.

**Les bases du réseau avec Mirror sous Unity sans XR :**
- Faire un projet à deux avec Git et Mirror installé (sans XR).
- Créer un hotspot Wi-Fi sur un des deux PC et inviter votre collègue sur ce réseau.
- Ajouter vos Quest et vos téléphones.
- Faire une scène avec un `NetworkManager`.
  - Ajouter l'adresse du serveur à la main.
  - Un apprenant fait le serveur et l'autre le client.
- **PlayerPrefab**
  - Créer un prefab de joueur avec un `NetworkIdentity` dans le manager.
  - Créons une messagerie Unicode avec Mirror utilisant `[Command]` et `[ClientRPC]`.
    - Créer une méthode publique qui reçoit un texte.
    - Utiliser `[Command]` pour demander une action au serveur.
    - Utiliser `[ClientRPC]` pour répercuter l'action chez tous les joueurs.
  - Créons une méthode pour demander l'heure du serveur.
    - Créer une méthode publique `[Command]` pour demander l'heure au serveur.
    - Créer une méthode `[TargetRpc]` pour que le serveur réponde uniquement à ce joueur.
  - Permettre au joueur de choisir sa couleur sur le serveur.
    - Créer une méthode qui demande une couleur au serveur.
    - Créer une `[SyncVar]` pour que le serveur synchronise la couleur chez tout le monde.
    - Ajouter un hook à la `[SyncVar]` pour le lier à un `UnityEvent`.
      - Changer la couleur de fond de la caméra et de la montrer.
- **Discovery**
  - Trouver le serveur via le hotspot Wi-Fi.
  - Trouver le serveur via une IP statique.
  - Trouver le serveur via mDNS (hors Quest).
  - Trouver le serveur via un serveur Flask.
  - Laisser Mirror chercher... et croiser les doigts.
- **Spawn `NetworkIdentity`**
  - On passe cette partie, car on veut faire un jeu d'échecs en une journée.
- **Objets de la scène avec un `NetworkIdentity`**
  - Afficher les propriétés du `NetworkIdentity` d'un objet de la scène.
  - `[TransformSync]` si on veut un objet déplaçable.
    - `[RigidBodySync]` si on veut des objets avec une physique mobile.
  - Créer un script qui permet au joueur de `Claim` (prendre l'autorité) sur un objet du réseau.
    - Utiliser un `[Command(authority = false)]` pour demander au serveur, peu importe qui est le joueur.
    - Utiliser ... pour changer le propriétaire de l'objet.

**Un jeu d'échecs en VR ?**

> Comment j'ai fait pour un jeu VR non relocalisé ?

- Step by step pour la VR sur Steam avec ALVR [->](https://github.com/EloiStree/2026_07_23_workshop_hexagonal_chess_xr/blob/main/mirror/setup_mr/ReadMe.md)

> **Note :** J'avais commencé avec le Meta SDK, puis j'ai eu des bugs XR.
> Et comme ma Steam Machine était en route. J'ai donc continué sans.
> _Un petit step by step ,si vous ne vous souvenez plus des étapes avec Meta SDK: [->](https://github.com/EloiStree/2026_07_23_workshop_hexagonal_chess_xr/blob/main/mirror/setup_xr/ReadMe.md)_

**Un jeu d'échecs en XR ?**

> Comment j'ai fait en utilisant le plateau comme point de référence ?

- Relocalisation [->](https://github.com/EloiStree/2026_07_23_workshop_hexagonal_chess_xr/tree/main/mirror/relocation)
- Step by step [->](https://github.com/EloiStree/2026_07_23_workshop_hexagonal_chess_xr/blob/main/local_board_position/ReadMe.md) 
