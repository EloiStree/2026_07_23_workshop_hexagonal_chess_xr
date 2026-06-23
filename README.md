# Hexagonal Chess

[<img width="1298" height="663" alt="image" src="https://github.com/user-attachments/assets/6754aaea-7f16-4a51-96f0-885f386817bc" />](https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s)    
[<img width="1221" height="646" alt="image" src="https://github.com/user-attachments/assets/ae302df2-ae91-4c79-8e6c-65ffe05fefaa" />](https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s)    
[https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s](https://www.youtube.com/watch?v=NCeAVAVr2v4&t=102s)       

Lors de la formation précédente, je vous ai montré comment charger une scène sur une table en XR avec Unity et Meta :

[https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr](https://github.com/EloiStree/2026_05_11_workshop_gaming_hello_xr)    

Comme vous êtes en fin de formation Unity avant votre atelier. 😉   
<img width="498" height="283" alt="image" src="https://github.com/user-attachments/assets/4a3fc7a9-4cda-4189-a08e-34558c6d797f" />       

## Checklist des étapes

Faux clients: PreviewLabs a un client avec 4 casques Quest et demande de pouvoir jouer au echec hexagonal dans un barre a biere sur des tonneaux.
Evaluer les contraintes de fessabiliters en creant un prototype. Essaayer d estimer les difficulters d un telle projet.
Le but est d apprendre a prototyper sous contrainte de temps.



## Day 1

* À compléter...
* Créer un projet Unity URP vide.
  * Gitter le projet.
* Ajouter l’outil Meta depuis l’Asset Store.
  * Gitter le projet.
* Ajouter OpenXR.
* Valider les correctifs automatiques avec les outils Meta et la configuration OpenXR.
* Créer une scène vide avec le bloc de démarrage Meta.
* Vérifier son fonctionnement avec Meta Link.
* Tester un build Android sur le Quest 2.
* Ajouter la fonctionnalité permettant d’attraper des objets 3D avec les outils XR de Unity.
* Ajouter le plateau d’échecs et les pièces.
* Créer des Input Actions pour valider un point dans l’espace.
* Ajouter un script permettant de générer les points d’un triangle.
* Ajouter un point sous la manette lorsque le bouton est enfoncé.
* Lorsqu’il y a trois points, émettre un Unity Event contenant trois `Vector3`.
* À partir de ces trois points, à l’aide de mathématiques ou d’une IA :
  * Charger une table ronde (voir Fusion 360 ou mon outil de démonstration sous Godot).
* Déplacer et mettre à l’échelle la table d’échecs à partir de ces trois points.
* Ajouter les scripts Meta permettant d’attraper des objets 3D.
* Créer un prefab interactif pour toutes les pièces du jeu.
* Essayer de jouer seul aux échecs afin de trouver des bugs ou des améliorations.
* Permettre de replacer les pièces à leur position de départ.

## Day 2

* Qu’est-ce que Mirror ? Qu’est-ce que Photon ?
* Quels sont les attributs de base de Mirror ?
* Essayons de voir notre tête et nos mains bouger en multijoueur.
* Essayons d’ajouter un `NetworkTransform` aux pièces du jeu.
* **Bonus :**
  * Essayer de créer un timer afin de pratiquer l’utilisation des attributs et tags de Mirror.



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
