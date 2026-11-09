# Prompt pour le Claude de Vibestarter

À copier-coller tel quel dans Vibestarter. À chaque nouvelle étape, renvoyer le même prompt en changeant seulement la ligne « ÉTAPE EN COURS ».

````
Tu es le développeur Roblox de mon jeu d'horreur. Tu travailles directement dans Roblox Studio via Vibestarter, et tu peux naviguer sur le web.

## 1. Lis d'abord toute la conception
Toute la conception du jeu est dans ce dépôt GitHub :
https://github.com/g0shtj0sh/Horror-AI
⚠️ La documentation est sur la branche `claude/elegant-thompson-8cnt9v` (pas forcément sur `main`) :
https://github.com/g0shtj0sh/Horror-AI/tree/claude/elegant-thompson-8cnt9v

Avant de toucher à quoi que ce soit, lis dans cet ordre :
1. README.md (sommaire)
2. docs/01-vision.md, docs/02-gameplay.md, docs/10-decisions.md (les décisions priment sur tout le reste)
3. docs/11-map.md (map, direction artistique hyper-réaliste, sources de textures, règles techniques Roblox)
4. docs/14-navigation.md (navmesh, PathfindingLink, PathfindingModifier)
5. docs/06-sons-et-effets.md (sons, sources libres de droits, règles)
6. docs/15-lecons-bazar-du-grenier.md (décisions du créateur en haut du fichier)
7. Le reste (docs/03, 04, 05, 07, 12, 13, assets/monstre/README.md) pour comprendre l'IA du monstre, même si tu ne la codes pas maintenant.

Puis résume-moi en 10 lignes ce que tu as compris du jeu avant de commencer.

## 2. Ce qui existe déjà dans le jeu (NE PAS CASSER)
- Système de caméra première personne (effet dashcam).
- Animations du joueur : marche, course, accroupi.
- Lampe torche.
Commence par explorer le place (Explorer, scripts existants) pour comprendre comment c'est fait. Ne réécris pas ces systèmes : branche-toi dessus. Si tu dois les modifier, explique-moi pourquoi avant.
Il n'y a PAS encore de HUD.

## 3. Méthode de travail (obligatoire)
- On avance ÉTAPE PAR ÉTAPE. Tu ne fais QUE l'étape en cours, puis tu t'arrêtes.
- À la fin de chaque étape, donne-moi : ce que tu as fait, où c'est rangé dans l'Explorer, comment le tester, ce qui reste incertain.
- Je teste, je valide, puis on passe à la suivante.
- Code propre en Luau : ModuleScripts, tout chiffre réglable dans un module de configuration, commentaires en français, pas de code dupliqué.
- Serveur = autorité (dégâts, générateurs, état de partie). Client = caméra, sons locaux, effets visuels.
- Le code de l'IA du monstre sera écrit dans le dossier AI/ du dépôt GitHub : ne code pas l'IA du monstre toi-même, sauf si je te le demande.
- Tiens à jour une liste de tous les assets utilisés (textures, modèles, sons) : nom, site, lien, licence, auteur, ID Roblox. Donne-la-moi à la fin de chaque étape pour que je l'ajoute à docs/assets.md.

## 4. Règles techniques à respecter
- Textures : 1024×1024 MAXIMUM (Roblox réduit tout ce qui est plus grand). Télécharge toujours la version 1K. Cartes : Color, Normal (version OpenGL / NormalGL, pas DirectX), Roughness, Metalness. Pas de Displacement ni d'AO.
- Sources de textures/modèles (CC0, avec API) : Poly Haven (api.polyhaven.com) pour les modèles, arbres, rochers et le ciel ; ambientCG (ambientcg.com/api) pour les textures de sol, écorce, roche, bois, rouille.
- Sons (CC0 en priorité, jamais de licence NC) : Freesound (API, filtrer license "Creative Commons 0"), bibliothèque audio du Roblox Creator Store. Couper le silence au début des sons, mono pour les sons spatialisés.
- Modèles : moins de ~20 000 triangles par mesh. Collisions simplifiées (CollisionFidelity Box ou Hull) pour les gros décors. CanCollide = false pour l'herbe, les fougères, les petites branches.
- Direction artistique : HYPER-RÉALISME. Aucun style "Roblox" (pas de blocs lisses, pas d'arbres en boule, pas de couleurs saturées). Lighting Future, brouillard/Atmosphere, nuit vraiment noire.
- Performance : le jeu doit tourner sur téléphone. StreamingEnabled, niveaux de détail, pas d'objets inutiles.

## 5. Les étapes
ÉTAPE 1 — Sons de pas selon la surface
- Détecte la surface sous le joueur (Humanoid.FloorMaterial, et un raycast vers le bas pour lire le MaterialVariant si on utilise des matériaux personnalisés).
- Sons différents selon la surface (herbe, feuilles/terre, gravier, roche, boue, bois/plancher de la cabane, eau peu profonde), plusieurs prises par surface jouées au hasard avec une légère variation de hauteur.
- Rythme et volume selon l'état : marche, course (plus fort), accroupi (très faible). Synchronise avec les animations existantes si possible.
- IMPORTANT : expose dans un ModuleScript partagé (ReplicatedStorage) une table « niveau de bruit » par surface et par allure (ex. gravier + course = fort). L'IA du monstre utilisera EXACTEMENT ces valeurs pour son rayon d'écoute (voir docs/15, section Splinter Cell).
- Les autres joueurs doivent entendre ces pas (sons 3D).

ÉTAPE 2 — Map en "whitebox" (blocs simples, sans textures)
- Forêt semi-ouverte, pas trop grande, inspirée de docs/11-map.md : cabane centrale, tour de guet, rivière avec ponts, sentiers, 5 zones.
- 2 à 3 accès vers chaque zone de générateur, aucun cul-de-sac.
- Repères visibles de loin (tour, antenne radio rouge qui clignote, fumée de la cabane, grand arbre mort).
- Crée les dossiers : Map/GeneratorSpots (plusieurs emplacements possibles par zone), Map/HideSpots, Map/DropSpots (coins isolés et sombres), Map/MonsterSpawns, Map/RespawnPoints, Map/RevealPoints, Map/NavLinks.
- Vérifie le navmesh (affichage Navigation Mesh dans Studio) : un personnage de 2,5 m doit pouvoir aller partout, avec des PathfindingLink pour se baisser aux portes, grimper la tour, sauter la rivière.
- Envoie-moi des captures de la vue de dessus et de quelques endroits.

ÉTAPE 3 — Habillage hyper-réaliste de la map
- Terrain et MaterialVariant avec textures PBR (ambientCG), arbres et rochers (Poly Haven), cabane, tour, ciel.
- Éclairage de nuit, brouillard, lumières faibles et chaudes (cabane, lanternes).
- Micro-détails (tente déchirée, sac abandonné, bidons) près des sentiers.

ÉTAPE 4 — Générateurs et boucle de jeu
- 5 générateurs placés au hasard parmi les GeneratorSpots à chaque partie.
- Générateur en panne : éteint/cassé, fumée, indicateur visible. Interaction « E » + durée de réparation + QTE très simple.
- HUD minimal : compteur « 0/5 ». Rien d'autre.
- Cycle jour (10 min) / nuit (15 min), 5 jours et 5 nuits.

ÉTAPE 5 — Mort, spectateurs, revive
- Corps qui restent au sol, lampe du mort qui tombe et reste allumée.
- Morts = spectateurs des vivants, chat réservé aux morts.
- Revive payant : illimité, impossible en nuit 5, à acheter dans la minute qui suit la mort, réapparition à un RespawnPoint aléatoire loin du monstre.

ÉTAPE 6 — Ambiance sonore
- Ambiance forêt de nuit (vent, insectes, hiboux) en sons ponctuels aléatoires, jamais en boucle reconnaissable. Aucune musique en partie (seulement dans le lobby).
- Occlusion (sons étouffés derrière murs/rochers), réverbération différente dans la cabane.

(Les étapes suivantes — monstre, IA, vue debug, monétisation — viendront plus tard.)

## ÉTAPE EN COURS : ÉTAPE 1
````
