Je voulais montrer comment utiliser le Meta SDK, mais avec Mirror.

Mais le Meta Launcher était buggé.
Quelques bugs de Meta étaient également présents dans l'exemple fourni par Meta.

Comme le Steam Frame et la Steam Machine sont à portée de main, c'est le bon moment pour parler de SteamVR, Steam Link et d'ALVR.

Étant donné que Steam Link nécessite une bonne connexion Wi-Fi entre votre PC et votre routeur, nous verrons également ALVR. En revanche, si vous êtes chez vous avec un bon Wi-Fi, vous pouvez tout à fait utiliser Steam Link.

ALVR peut aussi être utilisé avec un câble. 😉

Le compromis, c'est que nous ne pourrons pas créer d'applications en réalité mixte (passthrough) sur PC.

---

Allons récupérer la scène de démonstration sous Unity.

Choisissez **MR** si vous voulez faire de la réalité mixte (ou vous orienter vers la réalité augmentée), et **VR** si vous souhaitez faire de la réalité virtuelle sans passthrough.

![alt text](image.png)

On peut faire une petite pause café... 😅

![alt text](image-1.png)

Ou aller lire la documentation de Mixed Reality.

[![alt text](image-81.png)](https://docs.unity3d.com/Packages/com.unity.template.mixed-reality@2.2/manual/index.html)

https://docs.unity3d.com/Packages/com.unity.template.mixed-reality@2.2/manual/index.html

On peut vérifier que notre projet est bien configuré pour la VR et qu'il n'y a rien de validé dans l'auto-correcteur.

![alt text](image-2.png)

Passons ensuite sur Android pour le futur build.

(Apparemment, vous avez aussi maintenant les options **Meta Quest** et **Android XR**.)

![alt text](image-3.png)

-------------------------

Nous pouvons aller télécharger Steam (avec Steam Link) ainsi que SteamVR.

[![alt text](image-4.png)](https://youtu.be/DmDK-F8eoI4?t=41)
https://youtu.be/DmDK-F8eoI4?t=41
Mais il vous faut une connection Wifi entre le PC et une connection cable au mdoels.





Une fois que nous avons installé Steam, nous pouvons télécharger ALVR, qui nous permettra d'utiliser le Quest avec SteamVR.

[![alt text](image-5.png)](https://github.com/alvr-org/ALVR/releases/tag/v20.14.1)

[https://github.com/alvr-org/ALVR/releases/tag/v20.14.1](https://github.com/alvr-org/ALVR/releases/tag/v20.14.1)

Téléchargeons l'APK depuis GitHub.

![alt text](image-6.png)

Lancez **Screen Copy**.

![alt text](image-7.png)

Avec Screen Copy, on peut copier l'APK sur le Quest.
Vous pouvez également utiliser **Developer Hub**.

![alt text](image-8.png)

Pour trouver votre application, il faut aller dans le menu **Sources inconnues**.

![alt text](image-9.png)

Puis chercher parmi les namespaces.

![alt text](image-10.png)

Vous devriez avoir une interface comme celle-ci.

![alt text](image-11.png)

Téléchargeons la version Windows d'ALVR depuis GitHub.

![alt text](image-12.png)

![alt text](image-13.png)

Puis lançons l'exécutable (l'assistant d'installation).

![alt text](image-14.png)

Il nous proposera gentiment d'ouvrir les ports de votre ordinateur.

![alt text](image-15.png)

Voici à quoi ressemble ALVR : un menu permettant de lancer une connexion en Wi-Fi ou en câble, ainsi que d'initier SteamVR (avec un menu **Settings** et de nombreux boutons).

![alt text](image-16.png)

Ce qui nous intéresse est une connexion câblée.
Histoire de ne pas avoir huit connexions Steam en Wi-Fi dans la pièce.

![alt text](image-17.png)

Lançons SteamVR.

![alt text](image-18.png)

Puis allons voir ses préférences.

![alt text](image-19.png)

C'est le bouton situé en haut à gauche.

![alt text](image-21.png)

Nous cherchons à faire en sorte que Steam soit utilisé par défaut comme runtime OpenXR.

![alt text](image-20.png)

N'oubliez pas de connecter votre casque et votre PC au même réseau Wi-Fi (pour ALVR, mais surtout pour votre futur jeu multijoueur).

![alt text](image-22.png)

Une petite sauvegarde s'impose.

![alt text](image-23.png)

Vérifiez que l'affichage des fichiers cachés et des extensions de fichiers est activé.

![alt text](image-24.png)

Allons à la racine du projet avec un petit Git.

![alt text](image-25.png)

Ajoutez le `.gitignore` si ce n'est pas déjà fait.

![alt text](image-26.png)

Ouvrez un terminal de commande.

![alt text](image-27.png)

`cmd` dans Windows Terminal.

Puis effectuez un petit **add / commit / pull / push**.

```bash
git add .
git status
git commit -m "Project is SteamVR ready."
git status
git pull
git push
```

![alt text](image-82.png)

Sauvegardons la scène de démonstration (**Sample**) afin de conserver l'original si nécessaire.

![alt text](image-28.png)

Je vous ai préparé, à partir de mon projet Godot, un **Hexa Chess** pour l'exercice.

[https://github.com/EloiStree/2026_06_15_gdp_hexa_chess](https://github.com/EloiStree/2026_06_15_gdp_hexa_chess)

![alt text](image-29.png)

Vous trouverez plus d'informations sur les règles du jeu ici :

[https://greenchess.net/rules.php?v=glinski](https://greenchess.net/rules.php?v=glinski)

Vous pouvez télécharger la texture et le modèle 3D ici :

![UV](hexa_chess_board_color_uv.png)

Download: [OBJ](hexa_chess_board.obj), [UV](hexa_chess_board_color_uv.png)

Sinon, je vous ai préparé un package sans Mirror ici :

[https://github.com/EloiStree/2026_06_15_upm_hexa_chess](https://github.com/EloiStree/2026_06_15_upm_hexa_chess)

Ajoutez un cube ainsi que le plateau, puis allons voir ce que cela donne.

![alt text](image-30.png)

![alt text](image-31.png)

Pour publier, n'oubliez pas de donner un nom à votre application.

![alt text](image-32.png)

Activez l'exécution même lorsque l'application n'a pas le focus.

![alt text](image-33.png)

Changez le namespace (`pays.entreprise.application`).

![alt text](image-34.png)

Puis générez l'APK.

![alt text](image-35.png)

Enfin, **Attendre**.

![alt text](image-36.png)



## Pour vous faire gagner du temps

Pour vous faire gagner du temps, j'ai préparé un plateau avec des ancrages ainsi qu'un ou deux scripts.

```bash
git submodule add https://github.com/EloiStree/2026_06_15_upm_hexa_chess.git Packages/be.elab.hexachess
```

Ou :

```bash
git clone https://github.com/EloiStree/2026_06_15_upm_hexa_chess.git Packages/be.elab.hexachess
```

Créez un prefab (sans Mirror) pour chaque pièce, en veillant à utiliser la bonne taille.

![alt text](image-38.png)

---

## Essayons de générer un APK

![alt text](image-37.png)

---

## Notre projet est prêt à passer en multijoueur

Notre projet est maintenant prêt à être transformé en version multijoueur.

![alt text](image-39.png)

![alt text](image-40.png)

![alt text](image-41.png)


![alt text](image-42.png)

![alt text](image-43.png)

![alt text](image-44.png)

![alt text](image-45.png)

```cs
using UnityEngine;

/*
	Documentation: https://mirror-networking.gitbook.io/docs/components/network-manager
	API Reference: https://mirror-networking.com/docs/api/Mirror.NetworkManager.html
*/

namespace Mirror.Examples.Pong
{
    // Custom NetworkManager that simply assigns the correct racket positions when
    // spawning players. The built in RoundRobin spawn method wouldn't work after
    // someone reconnects (both players would be on the same side).
    [AddComponentMenu("")]
    public class NetworkManagerPong : NetworkManager
    {
        public Transform leftRacketSpawn;
        public Transform rightRacketSpawn;
        GameObject ball;

        public override void OnServerAddPlayer(NetworkConnectionToClient conn)
        {
            // add player at correct spawn position
            Transform start = numPlayers == 0 ? leftRacketSpawn : rightRacketSpawn;
            GameObject player = Instantiate(playerPrefab, start.position, start.rotation);
            NetworkServer.AddPlayerForConnection(conn, player);

            // spawn ball if two players
            if (numPlayers == 2)
            {
                ball = Instantiate(spawnPrefabs.Find(prefab => prefab.name == "Ball"));
                NetworkServer.Spawn(ball);
            }
        }

        public override void OnServerDisconnect(NetworkConnectionToClient conn)
        {
            // destroy ball
            if (ball != null)
                NetworkServer.Destroy(ball);

            // call base functionality (actually destroys the player)
            base.OnServerDisconnect(conn);
        }
    }
}

```

keyword:
```
public class NetworkManagerPong : NetworkManager
public override void OnServerAddPlayer(NetworkConnectionToClient conn)
public override void OnServerDisconnect(NetworkConnectionToClient conn)
NetworkServer.AddPlayerForConnection(conn, player);
NetworkServer.Spawn(ball);
if (ball != null)
    NetworkServer.Destroy(ball);
```




------------

![alt text](image-46.png)

![alt text](image-47.png)


Nous on veut un object deja dans la scene.

Il nous faut donc un Gameobject avec un NetworkIdentity
![alt text](image-48.png)

Regardons comment un bullet est gerer:

Ici , cest gere niveau server.
On creer la bullet chez les joueurs mais c est le serveur qui calcule.

``` cs
using UnityEngine;

namespace Mirror.Examples.Tanks
{
    public class Projectile : NetworkBehaviour
    {
        public float destroyAfter = 2f;
        public Rigidbody rigidBody;
        public float force = 1000f;

        public override void OnStartServer()
        {
            Invoke(nameof(DestroySelf), destroyAfter);
        }

        // set velocity for server and client. this way we don't have to sync the
        // position, because both the server and the client simulate it.
        void Start()
        {
            rigidBody.AddForce(transform.forward * force);
        }

        // destroy for everyone on the server
        [Server]
        void DestroySelf()
        {
            NetworkServer.Destroy(gameObject);
        }

        // ServerCallback because we don't want a warning
        // if OnTriggerEnter is called on the client
        [ServerCallback]
        void OnTriggerEnter(Collider other)
        {
            Debug.Log("Hit: " + other.name);
            if (other.transform.parent.TryGetComponent(out Tank tank))
            {
                --tank.health;
                if (tank.health == 0)
                    NetworkServer.RemovePlayerForConnection(tank.netIdentity.connectionToClient, RemovePlayerOptions.Destroy);

                DestroySelf();
            }
        }
    }
}
```

Keyword:
```
NetworkBehaviour  
[Server] 
NetworkServer.Destroy(gameObject);
[ServerCallback]
NetworkServer.RemovePlayerForConnection(tank.netIdentity.connectionToClient, RemovePlayerOptions.Destroy);
```




Il nous faut un player fictif qui sera un representation du joueur VR.
Ne mettez pas la camera VR dans le NetworkIdentity

![alt text](image-49.png)

![alt text](image-50.png)

![alt text](image-51.png)

![alt text](image-52.png)



Il n y aura que un jouer avec la VR dans la scene.
La partie VR et donc pas multijoueur.
Et comme le point commun de tout les joueurs c est le plateau d echec.

On peut partager la position de la tete du jouer et ses main par rapport a ce plateau.

Si l est le prorittaire de ce session, c est lui qui upload.


![alt text](image-53.png)


On veut pouvoir calculer la position des joueurs par rapport au plateau d echec
Et le plateau lui sera positionner par rapport au monde reel.
https://github.com/EloiStree/2024_10_19_upm_relocation_rotation/blob/main/Runtime/RelocationUtility.cs

Il nous faut un code pour recuperer la position par rapport au jeu
```cs
    public static void GetLocal(Transform point, Transform reference, out Vector3 localPosition, out Quaternion localRotation)
    {
        GetWorldToLocal_DirectionalPoint(point.position, point.rotation, reference.position, reference.rotation, out localPosition, out localRotation);
    }
    public static void GetWorldToLocal_DirectionalPoint(in Vector3 worldPosition, in Quaternion worldRotation, in Vector3 positionReference, in Quaternion rotationReference, out Vector3 localPosition, out Quaternion localRotation)
    {
        localRotation = Quaternion.Inverse(rotationReference) * worldRotation;
        localPosition = Quaternion.Inverse(rotationReference) * (worldPosition - positionReference);
    }
```


Et un code pour replacer par la suite chez les autres;
```cs
  public static void SetToWorld(Transform point, Transform reference, in Vector3 localPosition, in Quaternion localRotation)
  {
      GetLocalToWorld_DirectionalPoint(localPosition, localRotation, reference.position, reference.rotation, out Vector3 worldPosition, out Quaternion worldRotation);
      point.position = worldPosition;
      point.rotation = worldRotation;
  }
  public static void GetLocalToWorld_DirectionalPoint(in Vector3 localPosition, in Quaternion localRotation, in Vector3 positionReference, in Quaternion rotationReference, out Vector3 worldPosition, out Quaternion worldRotation)
  {
      worldRotation = rotationReference * localRotation;
      worldPosition = (rotationReference * localPosition) + (positionReference);
  }
```



Creeons un script de tag pour le plateau et les points essentiels de la XR
```cs
public class PlayerChessXrTagMono_Head : MonoBehaviour
{
    public static Transform _in_scene_tag;
    void Awake()  => _in_scene_tag = this.transform;
   
}
public class PlayerChessXrTagMono_ChessBoardCenter : MonoBehaviour
{
    public static Transform _in_scene_tag;
    void Awake()  => _in_scene_tag = this.transform;
   
}
public class PlayerChessXrTagMono_LeftHand : MonoBehaviour
{
    public static Transform _in_scene_tag;
    void Awake()  => _in_scene_tag = this.transform;
    
}
public class PlayerChessXrTagMono_RightHand : MonoBehaviour
{
    public static Transform _in_scene_tag;
    void Awake()  => _in_scene_tag = this.transform;
   
}
```


![alt text](image-54.png)



Tag Head
![alt text](image-55.png)


Left Right Hand 
![alt text](image-56.png)


Center of the board game
![alt text](image-57.png)


Put the tag in the XR Origine structure can boring because it is quickly some script in the scene somewhere

So I created this followit script to have for prefab at the same place

```cs
using UnityEngine;
public class HexaChessMono_FollowIt : MonoBehaviour
{
    public Transform m_whatToFollow;
    public Transform m_whatToMove;


    private void Reset()
    {
        m_whatToMove = this.transform;
    }
    void Update()
    {
        if (m_whatToFollow != null && m_whatToMove != null)
        {
            m_whatToMove.position = m_whatToFollow.position;
            m_whatToMove.rotation = m_whatToFollow.rotation;
        }
    }
}
```

![alt text](image-58.png)


![alt text](image-59.png)

Tadaaam
On dirait pas mais on a un sphere gris qui represent la donner multi joueur sur le point rouge en dessou qui represent la postion de la manette
![alt text](image-60.png)
![alt text](image-61.png)


------------------



![alt text](image-63.png)

If you do a game where you are not reaclibrating in real life or scaling the board. Then you can use SyncTransform



Lets try to add a Grab Interaction and Mirror NetworkTransform (unrealiable)
It need a NetworkIdentity
![alt text](image-64.png)



NOte;
We need to do a code that disable the head of the player it he is on his own PC.
![alt text](image-65.png)

![alt text](image-66.png)

```cs
using UnityEngine;
using UnityEngine.Events;
using Mirror;

public class HexaChessMirrorMono_HideShowIfLocal : NetworkBehaviour
{
    [SerializeField] private UnityEvent m_onIsLocalPlayerEvent;
    [SerializeField] private UnityEvent m_onIsNotLocalPlayerEvent;
    [SerializeField] private UnityEvent<bool> m_onIsLocalPlayerBoolEvent;
    [SerializeField] private UnityEvent<bool> m_onIsNotLocalPlayerBoolEvent;

    [SerializeField]
    private bool m_resultDebugIsLocalPlayer = false;

    public override void OnStartClient()
    {
        Refresh();
    }

    public override void OnStartLocalPlayer()
    {
        Refresh();
    }

    private void Refresh()
    {
        m_resultDebugIsLocalPlayer = isLocalPlayer;
        if (isLocalPlayer)
        {
            m_onIsLocalPlayerEvent?.Invoke();
            m_onIsLocalPlayerBoolEvent?.Invoke(true);
            m_onIsNotLocalPlayerBoolEvent?.Invoke(false);
        }
        else
        {
            m_onIsNotLocalPlayerEvent?.Invoke();
            m_onIsLocalPlayerBoolEvent?.Invoke(false);
            m_onIsNotLocalPlayerBoolEvent?.Invoke(true);
        }
    }
}
```





----------

To find the server automaticaly if the network is friendly
![alt text](image-67.png)


What you can do it create a hotspot on window and host the server on window.




------------

Essayons de trouver ou d etre le server host


![alt text](image-69.png)
![alt text](image-68.png)



To test it I need a Quest link to our Unity editor.
Lets run on Quest under the Wifi to ease the build and push the apk
![alt text](image-70.png)
https://github.com/EloiStree/2025_01_12_pyhton_build_run_apk_broadcaster.git

Il y a un outil avec Mirror pour et Unity Network pour test le multijoueur dans l editor. mais je skip.



![alt text](image-71.png)

C est la raison pour laquel je conseille de faire cette exercice a deux.


-----------------

I AM HERE

-----------------


https://mirror-networking.gitbook.io/docs/manual/components/network-transform
![alt text](image-72.png)


To make object grabbable by only a player in the game.
We should use 
```
GetComponent<NetworkIdentity>()
    .AssignClientAuthority(connectionToClient);
```


Essayons une fois un piece attrapee de donner l authoriter de la bouger a ce joueur

![alt text](image-73.png)

Il nous faut donc XR Interaction dans l assembly de notre outil.



Creeons un script qui permet de reprendre le control d un object a bouger

Vibed with experience 😜



**Allows to notify an object is grabbed:**
```cs

using UnityEngine;
using UnityEngine.Events;
using UnityEngine.XR.Interaction.Toolkit;

/// <summary>
/// Emits UnityEvents when the referenced XRGrabInteractable is grabbed or released.
/// Designed to be assigned by game designers in the Inspector.
/// </summary>
public class HexaChessMono_ListenToXRGrab : MonoBehaviour
{
    [Header("References")]
    [Tooltip("The XR Grab Interactable component to listen to. If null, will try to find one on this GameObject.")]
    [SerializeField] private UnityEngine.XR.Interaction.Toolkit.Interactables.XRGrabInteractable grabInteractable;

    [Header("Grab Events")]
    [Tooltip("Fired when an interactor grabs the object.")]
    [SerializeField] private UnityEvent onGrabbed;

    [Tooltip("Fired when an interactor releases the object. Includes the interactor that released it.")]
    [SerializeField] private UnityEvent<UnityEngine.XR.Interaction.Toolkit.Interactors.IXRSelectInteractor> onReleased;



    [Tooltip("If true, will log debug messages when grab/release events fire.")]
    [SerializeField] private bool debugLogs = false;

   

    #region Unity Lifecycle

    private void OnEnable()
    {
        if (grabInteractable != null)
        {
            SubscribeToEvents();
        }
   
    }

    private void OnDisable()
    {
        UnsubscribeFromEvents();
    }

    #endregion

    #region Event Subscription

    private void SubscribeToEvents()
    {
        grabInteractable.selectEntered.AddListener(HandleSelectEntered);
        grabInteractable.selectExited.AddListener(HandleSelectExited);
    }

    private void UnsubscribeFromEvents()
    {
        if (grabInteractable != null)
        {
            grabInteractable.selectEntered.RemoveListener(HandleSelectEntered);
            grabInteractable.selectExited.RemoveListener(HandleSelectExited);
        }
    }

    #endregion

    #region Event Handlers

    private void HandleSelectEntered(SelectEnterEventArgs args)
    {
        if (debugLogs)
        {
            Debug.Log($"[XRGrabEventEmitter] {gameObject.name} GRABBED by {args.interactorObject.transform.name}", this);
        }

        onGrabbed?.Invoke();
    }

    private void HandleSelectExited(SelectExitEventArgs args)
    {
        if (debugLogs)
        {
            Debug.Log($"[XRGrabEventEmitter] {gameObject.name} RELEASED by {args.interactorObject.transform.name}", this);
        }

        onReleased?.Invoke(args.interactorObject);
    }

    #endregion

    #region Public Methods

    /// <summary>
    /// Manually re-subscribe to events (useful if grabInteractable is changed at runtime).
    /// </summary>
    public void RefreshSubscription()
    {
        UnsubscribeFromEvents();
        if (grabInteractable != null)
        {
            SubscribeToEvents();
        }
    }

    /// <summary>
    /// Sets a new grab interactable and refreshes the subscription.
    /// </summary>
    /// <param name="newInteractable">The new XRGrabInteractable to listen to.</param>
    public void SetGrabInteractable(UnityEngine.XR.Interaction.Toolkit.Interactables.XRGrabInteractable newInteractable)
    {
        UnsubscribeFromEvents();
        grabInteractable = newInteractable;
        if (grabInteractable != null)
        {
            SubscribeToEvents();
        }
    }

    #endregion

}
```



**Allow to claim the authority:**   

```cs
using System.Collections.Generic;
using Mirror;
using UnityEngine;

public class HexaChessMirrorMono_ClaimAuthorityOfMoving : NetworkBehaviour
{
    [Header("Target Object")]
    [SerializeField] private NetworkIdentity m_toAffect;

    [SyncVar(hook = nameof(OnOwnerChanged))]
    public uint currentOwnerNetId = 0;

    private void Awake()
    {
        if (m_toAffect == null)
            m_toAffect = GetComponent<NetworkIdentity>();
    }

    private void Start()
    {
        if (m_toAffect == null)
        {
            Debug.LogError($"[{gameObject.name}] m_toAffect is not assigned!", this);
            return;
        }
    }

    [Client]
    public void OnInteracted()
    {
        ClaimAuthority();
    }

    public NetworkIdentity LookInSceneForLocalPlayer()
    {
        return NetworkClient.localPlayer;
    }

    [ContextMenu("Force Claim Authority")]
    public void ClaimAuthority()
    {
        if (m_toAffect == null) return;

        NetworkIdentity localPlayer = LookInSceneForLocalPlayer();
        if (localPlayer == null)
        {
            Debug.LogWarning("ClaimAuthority: Could not find local player.");
            return;
        }

        // Optional: prevent claiming if already owner
        if (currentOwnerNetId == localPlayer.netId)
        {
            Debug.Log("Already own this piece.");
            return;
        }

        ClaimAuthorityFromClientNetworkId(localPlayer.netId);
    }

    [Command(requiresAuthority = false)]
    private void ClaimAuthorityFromClientNetworkId(uint playerNetId)
    {
        if (m_toAffect == null) return;

        if (!NetworkServer.spawned.TryGetValue(playerNetId, out NetworkIdentity playerIdentity))
        {
            Debug.LogWarning($"ClaimAuthority: No player found with netId {playerNetId}.");
            return;
        }

        NetworkConnectionToClient targetConnection = playerIdentity.connectionToClient;
        if (targetConnection == null)
        {
            Debug.LogWarning($"ClaimAuthority: Player {playerNetId} has no client connection.");
            return;
        }

        m_toAffect.RemoveClientAuthority();
        m_toAffect.AssignClientAuthority(targetConnection);
        currentOwnerNetId = playerNetId;   // SyncVar

        Debug.Log($"[Server] Authority transferred to {playerNetId} for {m_toAffect.name}");
    }

    private void OnOwnerChanged(uint oldOwner, uint newOwner)
    {
        Debug.Log($"[Authority] Owner changed: {oldOwner} → {newOwner} | {m_toAffect?.name}");

        // Optional: React here (enable/disable dragging, highlight, etc.)
        bool isMine = newOwner == (NetworkClient.localPlayer?.netId ?? 0);
        // e.g. GetComponent<Draggable>()?.SetInteractable(isMine);
    }
    /// <summary>
    /// Returns true if the local client has authority over m_toAffect
    /// </summary>
    public bool HasAuthority()
    {
        if (m_toAffect == null) return false;

        // Preferred way: check from a NetworkBehaviour on the target object
        var nb = m_toAffect.GetComponent<NetworkBehaviour>();
        if (nb != null)
            return nb.isOwned;

        // Fallback (less common)
        return m_toAffect.isOwned; // NetworkIdentity also has isOwned in newer Mirror
    }
}
```


Tadam Si on pend pas en compte le repositionment et le resize du plateau on est bon.

Ils nous reste a faire un prefab avec cela pour et un varian pour chaque piece.


Un prefab absrait
![alt text](image-74.png)


![alt text](image-75.png)


Prefab variant   
![alt text](image-76.png)   

![alt text](image-77.png)


Et une fois les prefabs dupliquer placer et cropper niveau du collider.
Cela nous donne ceci.
![alt text](image-78.png)



----------



Hey hey we have now a VR Hexa Chess multiplayer.

Instead of going direclty on sync on the real world.

Let's create the timer to talk more about Mirror architecture.



-------------------

![alt text](image-79.png)

![alt text](image-80.png)

