# Hexagonal Chess

Bienvenue dans cet exercice VR, dans la continuité de la formation précédente.   
Nous avons vu comment réaliser un projet avec Meta.   

Mais comme nous sommes à l’aube des Steam Machines et des Steam Frames,    
regardons un peu du côté de SteamVR, OpenXR, ALVR et Steam Link.      

## Objectif

Notre but est de réaliser un jeu d’échecs hexagonal :   
[<img width="1298" height="663" alt="image" src="https://github.com/user-attachments/assets/6754aaea-7f16-4a51-96f0-885f386817bc" />](https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s)   
[<img width="1221" height="646" alt="image" src="https://github.com/user-attachments/assets/ae302df2-ae91-4c79-8e6c-65ffe05fefaa" />](https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s)   
https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s   

Lors de la formation précédente, je vous ai montré comment charger une scène sur une table en XR avec Unity et Meta :     
[<img width="941" height="526" alt="image" src="https://github.com/user-attachments/assets/829aadb9-5ba5-406b-9f8f-bf90e0df89a0" />](https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr/tree/main/Steps/RelocateSceneWithTwoPoint)   
Setup XR https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr/tree/main/Steps/InstallUnityForXR       
Relocalisation: https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr/tree/main/Steps/RelocateSceneWithTwoPoint      

Comme Vincent m'a dit qu'il préférait les jeux sur table ronde, montrez-moi que vous avez compris le cours précédent 😉.     
Créez un outil qui permet d’ajouter trois points donnés par l’utilisateur afin de positionner une table ronde en 3D.        
<img width="720" alt="image" src="https://github.com/user-attachments/assets/c9d387bd-ba71-4166-8c1e-76769b111f6b" />      
<img width="720" alt="image" src="https://github.com/user-attachments/assets/4bc249ac-4ef2-46d8-9c12-c375a18695e3" />     

Vous pouvez consulter mon code Godot si vous avez besoin de vous en inspirer :     
[https://github.com/EloiStree/2026_06_13_gdp_three_points_xr_cursor](https://github.com/EloiStree/2026_06_13_gdp_three_points_xr_cursor)   

Je vous avoue que je me suis aidé de l’IA pour cette partie mathématique du code :    
```gdscript
class_name TriPointsRelocateTableExample
extends Node

@export var _table_to_relocate: Node3D

func relocate_table(start: Vector3, middle: Vector3, end: Vector3):
    start.y = middle.y
    end.y = middle.y
    if start.distance_to(middle) < 0.001 or middle.distance_to(end) < 0.001 or start.distance_to(end) < 0.001:
        _table_to_relocate.global_position = middle
        _table_to_relocate.scale = Vector3.ONE
        return
    var center: Vector3 = get_circumcenter(start, middle, end)
    if center == Vector3.ZERO or is_nan(center.x):
        _table_to_relocate.global_position = middle
        _table_to_relocate.scale = Vector3.ONE
        return
    var r1 = (start - center).length()
    var r2 = (middle - center).length()
    var r3 = (end - center).length()
    var radius = r2
    _table_to_relocate.global_position = center
    _table_to_relocate.scale = Vector3(radius*2.0, 0.01, radius*2.0)
    var direction = (middle - center).normalized()
    var angle_y: float = Vector3.FORWARD.signed_angle_to(direction, Vector3.UP)
    _table_to_relocate.global_rotation_degrees = Vector3(0, rad_to_deg(angle_y), 0)

func get_circumcenter(a: Vector3, b: Vector3, c: Vector3) -> Vector3:
    var ab = b - a
    var ac = c - a
    var ab_cross_ac = ab.cross(ac)
    if ab_cross_ac.length_squared() < 1e-8:
        return Vector3.ZERO
    var to_center = (
        ab_cross_ac.cross(ab) * ac.length_squared() +
        ac.cross(ab_cross_ac) * ab.length_squared()
    ) / (2.0 * ab_cross_ac.length_squared())
    return a + to_center
```
 
Comme vous êtes en fin de formation Unity avant votre atelier 😉 :     
<img width="498" height="283" alt="image" src="https://github.com/user-attachments/assets/4a3fc7a9-4cda-4189-a08e-34558c6d797f" />   
Vous trouverez dans ce cours une checklist des étapes à comprendre et à pratiquer pendant ces deux jours.      

## Ressources

Voici des pièces d’un jeu d’échecs :
[<img width="816" height="333" alt="image" src="https://github.com/user-attachments/assets/b2d2229c-e3c7-466f-98c0-abde62333ef2" />](https://sketchfab.com/3d-models/chess-scene-pieces-blender-218776bed6144332ab41417badd5df6b)    
https://sketchfab.com/3d-models/chess-scene-pieces-blender-218776bed6144332ab41417badd5df6b   

Et un plateau que je vous ai préparé pour l’occasion :   
[<img width="493" height="708" alt="image" src="https://github.com/user-attachments/assets/0527c7e6-3fb9-469a-8acc-ecf5205d88a2" />](https://github.com/EloiStree/2026_06_15_upm_hexa_chess)     

Téléchargement :  
* Unity : https://github.com/EloiStree/2026_06_15_upm_hexa_chess   
* Godot : https://github.com/EloiStree/2026_06_15_gdp_hexa_chess    


Je vous ai dit que c’était une très mauvaise idée de faire un jeu multijoueur...     
Cela n’a pas empêché un élève de vouloir réaliser un jeu VR multijoueur l’année passée.       
Plutôt que de vous former en dehors de mes heures de cours, autant vous donner l’occasion de pratiquer.      

Essayons avec Mirror de permettre le déplacement des pièces.   
Et si vous allez trop vite, ajoutez un chronomètre.     

Nous pourrions utiliser le réseau multijoueur de Steam ou Photon, mais Mirror permet davantage d’indépendance.  

Allons voir Mirror :     
https://mirror-networking.com     

## Client fictif pour l’atelier

PreviewLabs a un client disposant de 4 casques Quest et souhaite permettre à plusieurs joueurs de jouer aux échecs hexagonaux dans un bar à bière, sur des tonneaux.   
Évaluez les contraintes de faisabilité en créant un prototype rapide mais efficace. Essayez d’estimer les difficultés d’un tel projet.    
Le but est d’apprendre à prototyper sous contrainte de temps.     

---

## Vieilles ressources

**TNET - Version hackathon**  
* https://github.com/EloiStree/2023_03_25_unity_dev_vs_wild_chill_chess

**Tutoriel Mirror**
* https://www.youtube.com/watch?v=oKf_EAU-ct4&t=533s

**Mon dernier prototype Mirror : Drone Soccer**   
* https://github.com/EloiStree/2024_06_01_unity_hello_mirror_drone_soccer
* https://youtu.be/L_VJgbrHmzw   




---------

Old Note:
- https://github.com/EloiStree/2026_01_08_workshop_hello_job_in_xr
- XInput Xbox Native https://github.com/EloiStree/2020_11_26_upm_xinput_dot_net
- mqtt vr https://github.com/EloiStree/2019_06_23_unity_empty_start_mqtt_vr
