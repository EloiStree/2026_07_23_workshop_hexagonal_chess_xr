## Ok, let's create a chess game.

One part is how to move the pieces and determine whose turn it is.

The other part is having a timer.

---

```text
🔹 Execution control attributes (where a method is allowed to run)

[Server] → only runs on the server, warns if called on a client
[ServerCallback] → only runs on the server, no warning if called on a client
[Client] → only runs on a client, warns if called on the server
[ClientCallback] → only runs on a client, no warning if called on the server

🔹 Networking synchronization attributes (how data and calls travel between the server and clients)

[Command] → client → server call
[ClientRpc] → server → all clients call
[TargetRpc] → server → one client call
[SyncVar] → variable automatically syncs from the server → clients
[SyncObject] → collection automatically syncs from the server → clients
```

More information:
https://github.com/EloiStree/2024_06_01_unity_hello_mirror_drone_soccer/blob/main/README.md

---

Ce que l'on veut, c'est un timer avec deux compteurs et un énumérateur indiquant **White** ou **Black**.

Il nous faut donc un **NetworkIdentity** et un script qui hérite de **NetworkBehaviour**.

Il possédera deux booléens et deux timers, chacun avec un **[SyncVar]**.

Le **`[SyncVar]`** est un attribut qui permet de modifier une donnée sur le serveur et de la synchroniser automatiquement avec tous les clients.

Il nous faudra également des appels client pour demander au serveur d'effectuer certaines actions.

C'est ce que nous allons faire avec les **`[Command]`**.

Des **UnityEvents** permettront de mettre à jour le visuel.

---

![alt text](image.png)

https://sketchfab.com/3d-models/chess-digital-timer-game-clock-4b0d351d0ddc492db2bb4090d4d4f263

---

![alt text](image-1.png)

https://sketchfab.com/3d-models/chess-analog-timer-game-clock-cac9854daabc4126ac585417e6c0edb9

---

Comme on ne veut pas avoir de dépendance avec **TextMeshPro**, on va partir sur un timer à aiguilles.

Il nous faut donc deux aiguilles, chacune attachée à une ancre, qui tourneront sur leur axe **Y** local.

Ce code n'a pas besoin d'être synchronisé sur le réseau.

![alt text](image-2.png)


```cs
using UnityEngine;

public class HexaChessMono_RotatingClockRotation : MonoBehaviour
{

    public Transform m_totalTimeLeftAnchorToRotate;
    public Transform m_secondAnchorToRotate;

    public float m_minuteForFullRotation = 15f;

    public float m_timeReceivedInSeconds = 0f;

    private void OnValidate()
    {
        UpdateCurrentTime(m_timeReceivedInSeconds);
    }

    public void UpdateCurrentTime(float time)
    {
        m_timeReceivedInSeconds = time;
        RefreshClock();
    }

    public void RefreshClock()
    {
        float timeReceived = m_timeReceivedInSeconds;
        float seconds = timeReceived % 60f;
        float totalMinutesPercentage = (m_timeReceivedInSeconds / (m_minuteForFullRotation * 60f));
        float percentageOfSecond = seconds / 60f;

        if (m_secondAnchorToRotate)
            m_secondAnchorToRotate.localEulerAngles = new Vector3(0f, percentageOfSecond * 360f, 0f);
        if (m_totalTimeLeftAnchorToRotate)
            m_totalTimeLeftAnchorToRotate.localEulerAngles = new Vector3(0f, totalMinutesPercentage  * 360f, 0f);
    }
}
```




Il nous faudra aussi une **animation** pour le **bouton**.

En attendant, utilisons deux **ancres**.

We need a button to indicate whether the timer is **on** or **off**.

For now, we'll use a temporary trigger that toggles the timer whenever a collision is detected.



![alt text](image-3.png)
```cs
public class HexaChessMono_TimerPinOnOff : MonoBehaviour {

    public Transform m_pinToMove;
    public Transform m_pinOnAnchor;
    public Transform m_pinOffAnchor;

    public void SetPinOnOffState(bool pinIsOn) {

        if (pinIsOn)
        {
            m_pinToMove.position = m_pinOnAnchor.position;
            m_pinToMove.rotation = m_pinOnAnchor.rotation;
        }
        else
        {
            m_pinToMove.position = m_pinOffAnchor.position;
            m_pinToMove.rotation = m_pinOffAnchor.rotation;
        }
    }
    [ContextMenu("Set Pin On")]
    public void SetPinOn()
    {
        SetPinOnOffState(true);
    }
    [ContextMenu("Set Pin Off")]
    public void SetPinOff()
    {
        SetPinOnOffState(false);
    }
}
```

You can add layer, tag name or script tag collision detection if you want more clean code.


```cs
using UnityEngine;
using UnityEngine.Events;

public class HexaChessMono_AnyCollisionEnterToUnityEvent : MonoBehaviour
{
    public UnityEvent m_onCollisionEnterEvent;

    public bool m_useCollisionEnter=true;
    public bool m_useTriggerEnter;


    private void OnCollisionEnter(Collision collision)
    {
        if (m_useCollisionEnter)    
            m_onCollisionEnterEvent.Invoke();
    }

    private void OnTriggerEnter(Collider other)
    {
        if (m_useTriggerEnter)  
            m_onCollisionEnterEvent.Invoke();
    }
}
```


![alt text](image-5.png)
Using Tag
```cs
using UnityEngine;
using UnityEngine.Events;

public class HexaChessMono_AnyCollisionEnterToUnityEvent : MonoBehaviour
{
    public UnityEvent m_onCollisionEnterEvent;

    public bool m_useCollisionEnter=true;
    public bool m_useTriggerEnter;

    public bool m_useTagNameFilter=true;
    public string m_tagNameFilter="TimerInteractable";


    private void OnCollisionEnter(Collision collision)
    {
        if (m_useCollisionEnter)
        {
            if (m_useTagNameFilter)
            {
                if (collision.gameObject.CompareTag(m_tagNameFilter))
                {
                    m_onCollisionEnterEvent.Invoke();
                }
            }
            else
            {
                m_onCollisionEnterEvent.Invoke();
            }
        }
    }

    private void OnTriggerEnter(Collider other)
    {
        if (m_useTriggerEnter)
        {
            if (m_useTagNameFilter)
            {
                if (other.gameObject.CompareTag(m_tagNameFilter))
                {
                    m_onCollisionEnterEvent.Invoke();
                }
            }
            else
            {
                m_onCollisionEnterEvent.Invoke();
            }
        }
    }
}

```

N'oublie pas d'ajouter un petit **Rigidbody** sur la main du joueur ou sur les boutons.

![alt text](image-6.png)

Plus qu'à raccorder le tout.

Le trigger peut appeler une **`[Command]`** qui communiquera avec le serveur.

Le serveur mettra à jour le timer et, grâce aux **`[SyncVar]`**, tous les clients recevront automatiquement la valeur du temps restant sous forme de **float**.


![alt text](image-4.png)

```cs
using UnityEngine;
using Mirror;
using UnityEngine.Events;
public class HexaChessMirrorMono_TimerState : NetworkBehaviour
{

    [SyncVar]
    [SerializeField] float m_timeLeftWhiteAtStart = 60f * 15f;
    [SyncVar]
    [SerializeField] float m_timeLeftBlackAtStart = 60f * 15f;

    [SyncVar]
    [SerializeField] float m_timeLeftWhite = 60f * 15f;
    [SyncVar]
    [SerializeField] float m_timeLeftBlack = 60f* 15f;

    [SyncVar]
    [SerializeField] bool m_isWhiteTurnOn = false;
    [SyncVar]
    [SerializeField] bool m_isBlackTurnOn = false;


    [SerializeField] Event m_event;
    [System.Serializable]
    public class Event {

        
        public UnityEvent<bool> m_onClientIsWhiteTurnUpdated;
        public UnityEvent<bool> m_onClientIsBlackTurnUpdated;
        public UnityEvent<float> m_onClientTimeLeftWhiteUpdated;
        public UnityEvent<float> m_onClientTimeLeftBlackUpdated;
        public UnityEvent m_onClientWhiteMissingTimeEvent;
        public UnityEvent m_onClientBlackMissingTimeEvent;
    }

    public void FixedUpdate()
    {
        if (!isServer)
            return;

        if (m_isWhiteTurnOn)
        {
            if (m_timeLeftWhite > 0.0f) { 
                m_timeLeftWhite -= Time.fixedDeltaTime;
                if (m_timeLeftWhite < 0.0f) {
                    m_timeLeftWhite = 0.0f;
                    RpcWhiteMissingTime();
                }
            }
        }
        if (m_isBlackTurnOn)
        {
            if (m_timeLeftBlack > 0.0f)
            {
                m_timeLeftBlack -= Time.fixedDeltaTime;
                if (m_timeLeftBlack < 0.0f)
                {
                    m_timeLeftBlack = 0.0f;
                    RpcBlackMissingTime();
                }
            }
        }

        m_event.m_onClientIsWhiteTurnUpdated?.Invoke(m_isWhiteTurnOn);
        m_event.m_onClientIsBlackTurnUpdated?.Invoke(m_isBlackTurnOn);
        m_event.m_onClientTimeLeftWhiteUpdated?.Invoke(m_timeLeftWhite);
        m_event.m_onClientTimeLeftBlackUpdated?.Invoke(m_timeLeftBlack);
    }

    [ClientRpc]
    void RpcWhiteMissingTime()
    {
        m_event.m_onClientWhiteMissingTimeEvent?.Invoke();
    }
    [ClientRpc]
    void RpcBlackMissingTime()
    {
        m_event.m_onClientBlackMissingTimeEvent?.Invoke();
    }

    [ContextMenu("Set as Black Turn")]
    [Command(requiresAuthority = false)]
    public void CmdSetAsBlackTurn()
    {
        m_isWhiteTurnOn = false;
        m_isBlackTurnOn = true;

    }
    [ContextMenu("Set as White Turn")]
    [Command(requiresAuthority = false)]
    public void CmdSetAsWhiteTurn()
    {
        m_isWhiteTurnOn = true;
        m_isBlackTurnOn = false;
    }

    [ContextMenu("Set as Pause State")]
    [Command(requiresAuthority = false)]
    public void CmdSetAsPauseState()
    {
        m_isWhiteTurnOn = false;
        m_isBlackTurnOn = false;
    }

    [ContextMenu("Reset the Game Time")]
    [Command(requiresAuthority = false)]
    public void CmdResetTheGameTime() {
        m_timeLeftWhite = m_timeLeftWhiteAtStart;
        m_timeLeftBlack = m_timeLeftBlackAtStart;
        m_isWhiteTurnOn = false;
        m_isBlackTurnOn = false;
    }

}
```



Il nous reste à écrire un code qui permet de remettre les pièces en place en reliant les positions de départ au prefab Mirror.

Par exemple :


```cs

using Mirror;
using System.Collections.Generic;
using UnityEngine;

public class HexaChessMirrorMono_SaveStartPoint : NetworkBehaviour
{
    public static List<HexaChessMirrorMono_SaveStartPoint> Instances { get; } = new();

    [Header("References")]
    [SerializeField] private Transform m_whatToAffect;

    [SyncVar]
    private Vector3 m_startPointAtAwake;

    [SyncVar]
    private Quaternion m_startRotationAtAwake;


    private void Reset()
    {
        m_whatToAffect = transform;
    }


    void Awake()
    {
        Instances.Add(this);
    }

    public override void OnStartServer()
    {
        base.OnStartServer();
        if (m_whatToAffect != null)
        {
            m_startPointAtAwake = m_whatToAffect.position;
            m_startRotationAtAwake = m_whatToAffect.rotation;
        }
    }

    private void OnDestroy()
    {
        Instances.Remove(this);
    }

    [ContextMenu("Reset Pieces At Start Point")]
    [Command(requiresAuthority = false)]
    public void CmdResetAllPiecesAtStartPoint()
    {
        ResetAllPiecesAtStartPoint();
    }


    [Server]
    void ResetAllPiecesAtStartPoint()
    {
        if (!isServer) 
            return;

        foreach (var piece in Instances)
        {
            if (piece != null)
                piece.RpcResetAtStartPoint();
        }
    }

    [ClientRpc]
    private void RpcResetAtStartPoint()
    {
        if (m_whatToAffect != null) { 
       
            m_whatToAffect.position = m_startPointAtAwake;
            m_whatToAffect.rotation = m_startRotationAtAwake;
        }
    }
}

```
![alt text](image-7.png)