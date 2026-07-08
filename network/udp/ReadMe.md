Let's try with the Aquarium example

Go to the release of this project.
The game is only playable by sending and receiving network pacakge;
- Add link


You can send a text to the app to be display.
You need for that an IPV4 address to send to and a port given by the game developer.
I am using 3615 for byte array and 3614 for text.

---------------

If you play on your own PC you can use 127.0.0.1 as ip address
If you play on your phone, you need to be on the same wifi.
Try to create a Wifi Hotspot on Window, because network that are not yours are often blocking port on the modem.

Not that you will probably have to open a port or disable firework.

---------------

# Send UDP

## Send Text
Send a Hello World.

Example in Python
```py

```

Example in C# Console
```cs

```

Example in Unity
```cs

```

Example in Godot
``` gdscript

```

## Send Byte

For UDP, the game works in a thrusted mode.
I thrust the player to not cheat or sabotage the other player.


You need to send the game, on 3615, 20 bytes
- 4 bytes for the index of the fish as integer 32 bits
- 4 bytes for the float of motor left
- 4 bytes for the float of motor right
- 4 bytes for the float of motor back
- 4 bytes for the float of motor front

(In little endian that is the direction of the bit in the byte)
(See Little Endian Here)






# Listen UDP

In my app, I have some code that as soon as a ipv4 give ma something, I broadcast him back the state of the game.

Create an C# code that listen to two ports the 3615 for bytes and the 3614 for text.



```py


```

As you can see in python we must use what is called a Thread.
It is like an application running on the side of an application to avoid blocking the main one.

Because you need to listen very carefully for the incoming message.

In Unity it can be hard to create a thread because calling a Unity feature from the thread break the application.
I propose you to have a look and use what I coded as a package.

LInk Git UDP:




Try to listen with my package to the incoming Text and Byte.






# Turn Byte and Text into game context.





