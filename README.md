# Hexagonal Chess

Bienvenu dans cette exercice VR continuation de la formation precedent.
On a vu comment faire un projet avec Meta.

Mais comme on est a l aube du Steam Machine et Steam Frame.
Regardons un peu a: SteamVR, Open XR, ALVR et Steam Link


Notre but faire un jeu d echec hexagonal:   
[<img width="1298" height="663" alt="image" src="https://github.com/user-attachments/assets/6754aaea-7f16-4a51-96f0-885f386817bc" />](https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s)      
[<img width="1221" height="646" alt="image" src="https://github.com/user-attachments/assets/ae302df2-ae91-4c79-8e6c-65ffe05fefaa" />](https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s)      
[https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s](https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s)         

Lors de la formation précédente, je vous ai montré comment charger une scène sur une table en XR avec Unity et Meta :
[https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr](https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr)    

Et comme vincent m'a dit qui prefere les jeux sur table ronde, montrer mois que vous avez compris le cours precenent 😉.
Creer un outil qui permet ajouter trois points donner par l utilisateur pour charger un table 3D
<img width="508" height="421" alt="image" src="https://github.com/user-attachments/assets/c9d387bd-ba71-4166-8c1e-76769b111f6b" />
<img width="574" height="235" alt="image" src="https://github.com/user-attachments/assets/d336c506-0869-4698-88ed-bd344e46e310" />

Vous pouvez trouver mon code Godot si vous avec besoin de vous inspirer:
https://github.com/EloiStree/2026_06_13_gdp_three_points_xr_cursor

Je vous avoue que je suis aider de l'AI pour cette partie du code:      
```
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


Comme vous êtes en fin de formation Unity avant votre atelier 😉   
<img width="498" height="283" alt="image" src="https://github.com/user-attachments/assets/4a3fc7a9-4cda-4189-a08e-34558c6d797f" />       
Vous trouverez dans ce cours un check liste des etapes a comprendre et pratiquer pendant c'est deux jours.



Voici des pieces d un jeu d echec:
[<img width="816" height="333" alt="image" src="https://github.com/user-attachments/assets/b2d2229c-e3c7-466f-98c0-abde62333ef2" />](https://sketchfab.com/3d-models/chess-scene-pieces-blender-218776bed6144332ab41417badd5df6b)     
https://sketchfab.com/3d-models/chess-scene-pieces-blender-218776bed6144332ab41417badd5df6b    

Et un plateau que je vous ai fait pour l occasion:   
[<img width="493" height="708" alt="image" src="https://github.com/user-attachments/assets/0527c7e6-3fb9-469a-8acc-ecf5205d88a2" />](https://github.com/EloiStree/2026_06_15_upm_hexa_chess)   
Download: [Unity](https://github.com/EloiStree/2026_06_15_upm_hexa_chess) , [Godot](https://github.com/EloiStree/2026_06_15_gdp_hexa_chess)   



## Client fictif pour l atelier

PreviewLabs a un client avec 4 casques Quest et demande de pouvoir jouer au echec hexagonal dans un barre a biere sur des tonneaux.
Evaluer les contraintes de fessabiliters en creant un prototype. Essaayer d estimer les difficulters d un telle projet.
Le but est d apprendre a prototyper sous contrainte de temps.



## Ce qui a inspiré cet atelier

* Vincent m’avait parlé de son envie de créer un jeu de plateau sur une table ronde.
  * L’exercice réalisé ensemble sur Unity constitue une excellente base pour ce type de projet.
* Je vous ai vus particulièrement motivés par les parties d’échecs pendant les pauses.
* L’année passée, j’ai accompagné un groupe en dehors de la formation sur les sujets du réseau multijoueur avec Mirror.

## Objectifs de l’atelier

Créez un jeu d’échecs hexagonal sur une table ronde en XR.   
(Pas de code de contrôle, sauf si vous avez terminé en avance.)   

Allons voir [Mirror](https://mirror-networking.com/?utm_source=chatgpt.com) qu’il sera utile d’étudier pour mener ce projet à bien.   




----


# Done during a hackathon

- https://github.com/EloiStree/2023_03_25_unity_dev_vs_wild_chill_chess

# Mirror tutorial:
- https://www.youtube.com/watch?v=oKf_EAU-ct4&t=533s


# Jeux de drone soccer

- https://github.com/EloiStree/2024_06_01_HelloMirrorDroneMulti/blob/main/README.md
- https://youtu.be/L_VJgbrHmzw
