# 14 — Navigation du monstre (navmesh et pathfinding)

Source : vidéo du **Bazar du Grenier** « LE NAVMESH » (35 min, 2026) — https://www.youtube.com/watch?v=FgT-ja_U3tY
Avec des développeurs d'Ubisoft. Analyse faite sur la transcription complète, puis traduite en outils **Roblox**.

## Résumé de la vidéo
1. **La navigation est la base de toute IA** : avant de réagir au bruit ou de traquer, le monstre doit savoir **marcher**. C'est aussi ce qui se voit le plus quand ça rate (PNJ bloqué par un caillou, debout sur une chaise).
2. Le **navmesh** est une surface invisible calculée sur le sol qui contient 3 informations :
   - **où l'IA peut aller** (zones accessibles) ;
   - **comment les zones sont connectées**, y compris par des passages invisibles (sauter, escalader, enjamber une rambarde) ;
   - **le coût de chaque surface** : l'IA ne prend pas forcément le plus court, mais le moins « cher ».
3. Les **liens entre zones** sont souvent joués avec une **animation** (sauter, s'accrocher, se baisser). Exemple : un monstre géant de *Resident Evil* qui **se baisse et s'agrippe au cadre** pour passer une porte.
4. On peut **ouvrir ou fermer des passages selon des conditions** (*BioShock* : Elizabeth ne passe dans une pièce qu'après le joueur).
5. **Coûts de surface** : un PNJ civil reste sur le trottoir, sauf en cas d'urgence. Les coûts peuvent **changer selon la situation**.
6. **Le navmesh doit être dynamique** : objets déplacés, portes, destructions (voiture garée dans *GTA*, murs détruits dans *Rainbow Six Siege*, recalculés pendant l'animation de l'explosion).
7. **Exploits** : les joueurs se mettent sur un point inaccessible et l'IA reste plantée (*World of Warcraft*). Solution courante : si l'IA ne bouge plus depuis X secondes, **la téléporter**.
8. **Économie de ressources** : ne pas recalculer les chemins à chaque image, répartir les calculs, et **à courte distance foncer tout droit** vers la cible sans pathfinding. *Left 4 Dead* fait **apparaître les ennemis hors de la vue** des joueurs.
9. **Limites voulues** : dans *Cyberpunk*, les ennemis ne poursuivent pas au-delà d'une certaine distance ; dans *Arc Raiders*, le drone qui ne rentre pas dans l'abri est un « bug » qui **sert le gameplay**. Il n'y a pas de bon ou mauvais pathfinding, seulement ce qui **sert l'expérience**.
10. **Terrain naturel = irrégulier** : il faut tester le navmesh sur les formes organiques, sans rendre la map artificiellement « propre ».
11. Le navmesh n'est pas physique : le personnage marche sur les **collisions** (souvent une **capsule**), le navmesh n'est qu'une **information**.

## Traduction dans Roblox
Roblox a tout ça intégré dans **`PathfindingService`** :

| Concept de la vidéo | Outil Roblox |
|---|---|
| Navmesh calculé automatiquement | Généré par Roblox à partir des collisions de la map |
| Taille de l'IA | `AgentRadius`, `AgentHeight` dans `CreatePath` |
| Capacités | `AgentCanJump`, `AgentCanClimb` (TrussPart) |
| Coût des surfaces | Table `Costs` par **matériau** (Grass, Mud, Water…) ou par **label** |
| Zones à coût personnalisé | **`PathfindingModifier`** (label + coût, ou `PassThrough`) |
| Liens entre zones (sauter, grimper, se baisser) | **`PathfindingLink`** entre deux `Attachment`, avec un label pour déclencher l'animation |
| Navmesh dynamique | Recalcul automatique ; l'événement **`Path.Blocked`** prévient qu'un chemin est coupé |
| Debug du navmesh | Studio : **Afficher le navmesh** (Navigation Mesh) dans les paramètres de visualisation |

## Ce qu'on applique au monstre

### 1. Ses dimensions dans le pathfinding
- Monstre de **2,5 m** : `AgentHeight` ≈ 9 studs (ajustable), `AgentRadius` adapté à sa largeur.
- Il **ne passe pas sous les portes basses** de la cabane : on place un **`PathfindingLink` « SeBaisser »** à chaque porte, qui joue l'animation où il se penche et s'agrippe au cadre (comme le monstre de Resident Evil). Bonus horreur : les joueurs voient ses doigts apparaître sur le cadre.

### 2. Des liens pour ses capacités spéciales
| Lien (`PathfindingLink`) | Animation | Où |
|---|---|---|
| `SeBaisser` | Se pencher sous la porte | Portes de la cabane |
| `Grimper` | Escalader | Tour de guet, rochers hauts |
| `Sauter` | Saut / enjamber | Rivière, troncs couchés, clôtures |
| `Fenetre` | Passer par une fenêtre | Fenêtres de la cabane |

**Aucun endroit inaccessible** : chaque cachette « en hauteur » doit avoir un lien, sinon les joueurs l'exploiteront (exploit WoW). C'est le principe de notre doc : aucune cachette sûre à 100 %.

### 3. Des coûts de surface selon l'intention
Les coûts changent selon ce que fait le monstre :

| Intention | Préfère | Évite |
|---|---|---|
| **Traquer / ramper** (discret) | Buissons, herbes hautes, sous-bois sombres (coût bas) | Chemins dégagés, zones éclairées (coût haut) |
| **Chasser** | Le plus court, chemins dégagés | — |
| **Se montrer au loin** | Lisières, bout des chemins (visible) | — |
| **Enlever un joueur** | Itinéraire loin du groupe | Zones proches des autres joueurs |

Les zones se marquent avec des `PathfindingModifier` (labels `Buisson`, `Eclaire`, `Chemin`, `Cabane`…). Le Directeur choisit la table de coûts selon l'intention.

### 4. Anti-blocage « fantôme »
Exactement le système décrit dans la vidéo, mais adapté à l'horreur :
- si le monstre ne progresse plus depuis quelques secondes **et qu'aucun joueur ne le voit**, il **disparaît et réapparaît** plus loin sur son chemin ;
- s'il est vu, il recule dans l'ombre puis disparaît ;
- **jamais de téléportation sous les yeux d'un joueur** (ça casserait l'immersion).
Ça colle avec sa capacité **Fantôme**.

### 5. Apparitions hors de vue (comme Left 4 Dead)
Pour aller vite d'un bout à l'autre de la map, le monstre peut **réapparaître à un point `MonsterSpawns` que personne ne voit**, plutôt que de marcher. Le Directeur vérifie la ligne de vue de chaque joueur avant.

### 6. Économie de ressources
- Recalculer le chemin **toutes les 0,5 à 1 s**, pas à chaque image, et seulement si la cible a bougé.
- **À moins de quelques mètres** de la cible : avancer en ligne droite (`MoveTo`) sans pathfinding.
- Écouter `Path.Blocked` pour recalculer seulement quand c'est nécessaire.

### 7. Limites voulues (qui servent la peur)
- **Pitié** : lors des premières nuits, la chasse s'arrête si le joueur atteint un « refuge » (lumière de la cabane, générateur en marche). Ce n'est pas un bug, c'est le moment où le joueur respire. En fin de partie, ces refuges ne protègent plus.
- **Durée maximale de chasse** réglable par phase, pour éviter la poursuite infinie.

### 8. Tester sur une map réaliste
Une forêt hyper-réaliste est **irrégulière** (racines, rochers, pentes). Il faudra :
- vérifier le navmesh dans Studio sur toute la map ;
- donner aux décors fins (herbes, petites branches) **`CanCollide = false`** pour qu'ils ne bloquent pas le monstre ;
- utiliser des collisions simplifiées (`CollisionFidelity` : Box ou Hull) pour les gros modèles, comme les capsules de la vidéo ;
- placer des liens à la main là où le calcul automatique échoue.

## À ajouter dans Roblox Studio (complète [11-map.md](11-map.md))
- `Map/NavLinks` : tous les `PathfindingLink` (SeBaisser, Grimper, Sauter, Fenetre).
- `PathfindingModifier` sur les zones : `Buisson`, `Eclaire`, `Chemin`, `Cabane`, `Riviere`.
- Vérifier le navmesh (vue debug Studio) après chaque modification de la map.
