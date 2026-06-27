I wanted to show how use Meta SKD but with Mirror.
But the Meta Launcher was bugging. 
Some DLL was missing.
And some Meta Bug was present in the Meta Sample.

As the Steam Frame and Steam machine is at the door.

It is the good time to speak about Steam VR / Steam Link and ALVR


As Steam Link need a good Wifi router connection from your PC to the router... We will see ALVR but if you are at home you can use Steam Link with the wifi.

ALVR can be use from cable ;)


The trade off is that we wont be able to do passthrough app on PC.


---------------


![alt text](image.png)

![alt text](image-1.png)


https://docs.unity3d.com/Packages/com.unity.template.mixed-reality@2.2/manual/index.html



![alt text](image-2.png)


![alt text](image-3.png)


-------------------------




[![alt text](image-4.png)](https://youtu.be/DmDK-F8eoI4?t=41)     
https://youtu.be/DmDK-F8eoI4?t=41  



![alt text](image-5.png)
https://github.com/alvr-org/ALVR/releases/tag/v20.14.1


![alt text](image-6.png)


![alt text](image-7.png)


![alt text](image-8.png)

![alt text](image-9.png)

![alt text](image-10.png)

![alt text](image-11.png)

![alt text](image-12.png)

![alt text](image-13.png)

![alt text](image-14.png)

![alt text](image-15.png)


![alt text](image-16.png)


![alt text](image-17.png)


![alt text](image-18.png)


![alt text](image-19.png)


![alt text](image-21.png)

![alt text](image-20.png)

Connect to the same wifi in case you want to use something else that cable




![alt text](image-22.png)


![alt text](image-23.png)


![alt text](image-24.png)

![alt text](image-25.png)


![alt text](image-26.png)



![alt text](image-27.png)
cmd in window terminal


```init
git add . 
git status
git commit -m "Project is SteamVR ready."
git status
git pull
git push
```


![alt text](image-28.png)


Less download the 3D model of the Hexa Chess I did for you:
https://github.com/EloiStree/2026_06_15_gdp_hexa_chess

![alt text](image-29.png)
https://greenchess.net/rules.php?v=glinski



![UV](hexa_chess_board_color_uv.png)
Download: [OBJ](hexa_chess_board.obj) , [UV](hexa_chess_board_color_uv.png)


You can check the Unity Package here:
https://github.com/EloiStree/2026_06_15_upm_hexa_chess

![alt text](image-30.png)   
![alt text](image-31.png)  
![alt text](image-32.png)   
![alt text](image-33.png)   
![alt text](image-34.png)  
![alt text](image-35.png)  
![alt text](image-36.png)     





-----------

Pour vous faire gagner du temps, j ai preparer un plateau avec des anchages et un ou deux scripts.
```
git submodule add https://github.com/EloiStree/2026_06_15_upm_hexa_chess.git Packages/be.elab.hexachess
```


Faire de prefab sans mirror de chaque piece avec la bonne taille.
![alt text](image-38.png)

---------------------

Let's try to build an apk.

![alt text](image-37.png)



-----------

Ok our project is ready to be turn in multiplayer.

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

