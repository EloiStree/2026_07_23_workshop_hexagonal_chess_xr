**Solution:** [Workshop](https://github.com/EloiStree/2026_07_23_workshop_hexagonal_chess_xr) - [Unity XR](https://github.com/EloiStree/2026_06_24_unity_hexa_chess_mirror) - [Chess 3D](https://github.com/EloiStree/2026_06_15_upm_hexa_chess) - [Chess Mirror](https://github.com/EloiStree/2026_06_26_upm_hexa_chess_mirror)   

# Planning

**Jeudi matin :** SteamVR + ALVR  
**Jeudi avant-midi :** Unity VR sans le Meta SDK  
**Jeudi après-midi :** Qu'est-ce que Mirror, sans VR ?  
**Vendredi :** Créons un jeu de plateau en VR sur le PC de Vincent.  

# Hexagonal Chess

Comme j'ai vu que vous aimiez les échecs 😋,     
et que le Steam Frame est en approche...     

Regardons comment réaliser un jeu d'échecs hexagonal ♟️ multijoueur.  
[Hello Unity Mirror](https://github.com/EloiStree/HelloUnityMirror)   

Les laptops de la formation ne sont pas conçus pour la VR.    
C'est l'occasion de parler de [ALVR](https://github.com/EloiStree/HelloGodotXR/issues/76) / [SteamVR](https://github.com/EloiStree/HelloGodotXR/issues/75).   

## Objectif

[<img width="1221" alt="image" src="https://github.com/user-attachments/assets/ae302df2-ae91-4c79-8e6c-65ffe05fefaa" />](https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s)   
[<img width="1298" alt="image" src="https://github.com/user-attachments/assets/6754aaea-7f16-4a51-96f0-885f386817bc" />](https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s)  
https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s   

### Challenge A : Sauver les positions par rapport au plateau

Si on veut faire un jeu en réalité augmentée, il nous faudra un plateau redimensionnable et déplaçable.   
[<img width="1231" height="680" alt="image" src="https://github.com/user-attachments/assets/81934347-ae42-4c4a-8c23-2f1d5d7a1a95" />](https://github.com/EloiStree/2026_06_26_upm_hexa_chess_mirror/blob/1cc1d1c5a310f16a4280d4fc08ad1c8519e6af3b/Runtime/HexaChessMono_SyncLocalPositionFromAnchor.cs)   
  
Une solution: https://github.com/EloiStree/2026_06_26_upm_hexa_chess_mirror/blob/1cc1d1c5a310f16a4280d4fc08ad1c8519e6af3b/Runtime/HexaChessMono_SyncLocalPositionFromAnchor.cs    

### Challenge B : Jouer sur la même table

[<img width="941" alt="image" src="https://github.com/user-attachments/assets/829aadb9-5ba5-406b-9f8f-bf90e0df89a0" />](https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr/tree/main/Steps/RelocateSceneWithTwoPoint)   

Tutoriels :   
[Setup XR 🔗](https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr/tree/main/Steps/InstallUnityForXR), [Relocalisation 🔗](https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr/tree/main/Steps/RelocateSceneWithTwoPoint)   

### Challenge C : Jouer sur une table ronde

[<img width="auto" alt="image" src="https://github.com/user-attachments/assets/4bc249ac-4ef2-46d8-9c12-c375a18695e3" />](https://github.com/EloiStree/2026_06_13_gdp_three_points_xr_cursor)   
[Example Godot](https://github.com/EloiStree/2026_06_13_gdp_three_points_xr_cursor)      
Comme Vincent m'a dit qu'il préférait les jeux sur table ronde, montrez-moi que vous avez compris le cours précédent 😉 en l'adaptant.  



## Ressources   

[<img width="720" alt="image" src="https://github.com/user-attachments/assets/b2d2229c-e3c7-466f-98c0-abde62333ef2" />](https://github.com/EloiStree/2026_06_15_upm_hexa_chess)   
[<img width="720" alt="image" src="https://github.com/user-attachments/assets/0527c7e6-3fb9-469a-8acc-ecf5205d88a2" />](https://github.com/EloiStree/2026_06_15_upm_hexa_chess)   
Téléchargement : [Unity 📦](https://github.com/EloiStree/2026_06_15_upm_hexa_chess), [Godot 📦](https://github.com/EloiStree/2026_06_15_gdp_hexa_chess)   

# Mirror

[<img width="720" alt="image" src="https://github.com/user-attachments/assets/4fbf5bb1-73a8-414a-8959-ae4562242f2a" />](https://mirror-networking.com)    
https://mirror-networking.com    

# L'exercice

[Introduction et checklist](introduction.md)

# À vous de jouer 😉

Comme vous êtes en fin de formation Unity avant votre atelier 😉 :     
<img width="720" alt="image" src="https://github.com/user-attachments/assets/4a3fc7a9-4cda-4189-a08e-34558c6d797f" />     


---

# Notes

**TNET Chess** : [Unity TNET Git](https://github.com/EloiStree/2023_03_25_unity_dev_vs_wild_chill_chess)    
**Tutoriel Mirror** : [Vidéo](https://www.youtube.com/watch?v=oKf_EAU-ct4&t=533s)   
**Drone Soccer** : [Unity Mirror Git](https://github.com/EloiStree/2024_06_01_unity_hello_mirror_drone_soccer)   
**Vidéo** : https://youtu.be/L_VJgbrHmzw    

---

## Anciennes notes

* [Job in XR](https://github.com/EloiStree/2026_01_08_workshop_hello_job_in_xr)
* [XInput Xbox Native](https://github.com/EloiStree/2020_11_26_upm_xinput_dot_net)
* [MQTT VR](https://github.com/EloiStree/2019_06_23_unity_empty_start_mqtt_vr)
* [FTL Bullets Photo](https://github.com/EloiStree/2021_09_09_photo_ftl_planetary_bullets)
* [Kinect to Texture2D](https://github.com/EloiStree/2022_06_06_upm_irregular_quadrilaterals_to_texture2d)
* [Hello Code And Quest](https://github.com/EloiStree/CodeAndQuestsEveryDay)
* [TBIO Layout](https://github.com/EloiStree/HelloTextByteInOutLayer)
* [Hello Mons XR](https://github.com/EloiStree/2024_07_03_workshop_mons_xr)
  * [Cool XR Mons](https://github.com/EloiStree/2024_07_03_workshop_mons_xr/blob/main/CoolXR.md), [Cool XR](https://github.com/EloiStree/HelloCoolXR/tree/main/Note)
  * [Pooling et Atlas](https://github.com/EloiStree/2024_07_03_workshop_mons_xr/blob/main/Pooling.md)
* [Hello Three Points](https://github.com/EloiStree/2025_03_24_workshop_hello_three_points)
* [Kyber and XR](https://github.com/EloiStree/HelloKyberShadowXR/tree/main)

---------

Full Tutorial on RSA Mirror:   
https://github.com/EloiStree/HelloUnityMirror/tree/main/video/mirror_and_rsa_workflow   



