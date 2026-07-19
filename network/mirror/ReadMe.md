https://mirror-networking.com/

[<img width="709" height="434" alt="image" src="https://github.com/user-attachments/assets/fa204aff-f697-4698-b140-3bee16dbf947" />
<img width="720" height="308" alt="image" src="https://github.com/user-attachments/assets/ff768de4-c4b3-4bbe-89d1-8066beea43bf" />
](https://mirror-networking.gitbook.io/docs/manual/general)
https://mirror-networking.gitbook.io/docs/manual/general

-------------------------


[<img width="1196" height="619" alt="image" src="https://github.com/user-attachments/assets/ea9c8ba0-9adf-4e86-816a-cdbc3b8d511f" />](https://mirror-networking.gitbook.io/docs/manual/transports)
https://mirror-networking.gitbook.io/docs/manual/transports

Built-in Transports
These transports are included with Mirror.

[KCP ](https://mirror-networking.gitbook.io/docs/manual/transports/kcp-transport)UDP transport based on kcp.c, line-by-line translation to C#

[Telepathy](https://mirror-networking.gitbook.io/docs/manual/transports/telepathy-transport) - Simple, message based, MMO Scale TCP networking in C#. And no magic.

[Simple Web Sockets](https://mirror-networking.gitbook.io/docs/manual/transports/websockets-transport) - WebGL transport layer for Mirror that target browser clients.

[Multiplexer](https://mirror-networking.gitbook.io/docs/manual/transports/multiplex-transport) - Bridging transport to allow a server to handle clients on different transports concurrently, for example desktop clients using Telepathy together with WebGL clients using Websockets.

[Latency Simulation](https://mirror-networking.gitbook.io/docs/manual/transports/latency-simulaton-transport) - Middleman transport to test non-ideal network conditions

[Encryption](https://mirror-networking.gitbook.io/docs/manual/transports/encryption-transport) - Middleman transport to encrypt a different transport

[Edgegap Relay Transports](https://mirror-networking.gitbook.io/docs/manual/transports/edgegap-transports) - Transports to utilize [Edgegaps Destributed Relay](https://edgegap.com/en/platform/distributed-relay) Service

Additional Transports
These transports are maintained by third parties outside of Mirror.

[Monke](https://github.com/JesusLuvsYooh/monke) - plug and play encrypted middleman transport layer for mirror.

[Ignorance](https://mirror-networking.gitbook.io/docs/manual/transports/ignorance) - reliable and unreliable sequenced UDP transport based on ENet.

[LiteNetLibTransport](https://mirror-networking.gitbook.io/docs/manual/transports/litenetlib-transport) - UDP transport based on [LiteNetLib](https://github.com/RevenantX/LiteNetLib).

Relay Transports
These transports are maintained by third parties and use relay infrastructure to connect clients to servers behind firewalls / NAT.

[Steam - FizzySteamworks](https://mirror-networking.gitbook.io/docs/manual/transports/fizzysteamworks-transport) - Transport utilizing Steam P2P network, building on [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET).

[Epic - Epic Online Services](https://github.com/Ludogram/EpicOnlineTransport) - Relay transport utilizing Epic's free relay service.

[LRM - Light Reflective Mirror](https://github.com/Speidy674/Light-Reflective-Mirror) - Relay transport for WebGL clients.
