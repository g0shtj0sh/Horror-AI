# 15 — Leçons des autres vidéos du Bazar du Grenier

Analyse de la playlist « One Shots du Bazar » (32 vidéos) et de la série « Ces jeux qui m'ont marqué », sur les transcriptions complètes. Les deux vidéos déjà traitées sont dans [13](13-lecons-ia-jeu-video.md) (IA) et [14](14-navigation.md) (navmesh).

| Vidéo | Lien | Pertinence |
|---|---|---|
| Le problème des Open Worlds | https://www.youtube.com/watch?v=Dp6C4KrCtgw | ⭐⭐⭐ map, guidage, rythme |
| Les Musiques de Jeux Vidéo - Comment ça fonctionne ? | https://www.youtube.com/watch?v=dm8wJ4IoEbA | ⭐⭐⭐ son et musique |
| Parlons immersion | https://www.youtube.com/watch?v=OHFXvt2SSjg | ⭐⭐⭐ interface, faune, faiblesse |
| Ces jeux qui m'ont marqué - Splinter Cell | https://www.youtube.com/watch?v=8NBlw9LQt0k | ⭐⭐⭐ alerte, bruit, discrétion |
| Ces jeux qui m'ont marqué - Half-Life | https://www.youtube.com/watch?v=0Nsc96FQWro | ⭐⭐ intro, « montrer plutôt qu'écrire » |
| Parlons des microtransactions | https://www.youtube.com/watch?v=pZxvHcaywKk | ⭐⭐ monétisation éthique |
| Qui a tué les RTS ? | https://www.youtube.com/watch?v=kixpgxlFwz4 | ⭐ simplicité, public coop |
| Ce jeu qui… avait le meilleur level design (chaîne JV) | https://www.youtube.com/watch?v=Vm9ezj7q5Is | ⭐ chemins multiples |

Les 24 autres vidéos de la playlist (Blizzard, E3, Sega, mascottes…) n'apportent rien à notre jeu.

---

## 1. La map et le guidage (Open Worlds, level design)

- **Pas de minimap ni de marqueurs : des repères lointains.** Trois ou quatre silhouettes visibles de presque partout servent de boussole : tour de guet, antenne radio rouge qui clignote, fumée de la cheminée de la cabane, grand arbre mort.
- **Des zones annoncées par des indices**, sans interface :
  - générateur : câbles au sol, bidons, bourdonnement qui grossit ;
  - cabane : chemin de planches, clôture ;
  - **antre du monstre** : carcasses, griffures sur les troncs, mouches.
  Les joueurs apprennent à « lire » la forêt.
- **Points de révélation (`Map/RevealPoints`).** Buttes et rochers qui bloquent la vue, et passages de crête marqués dans la map. Le Directeur sait que le joueur va y découvrir le paysage : c'est l'endroit idéal pour placer une apparition dans son champ de vision naturel.
- **Au moins 2 ou 3 accès à chaque générateur**, et **aucun cul-de-sac**. Si le monstre attend sur un chemin, il en reste un autre.
- **La carte évolue entre les nuits** : arbre tombé qui coupe un sentier, tronc qui fait pont, brouillard sur une vallée. Les joueurs doivent réapprendre la carte ; la navigation suit avec les `PathfindingModifier` ([14](14-navigation.md)).
- **Forêt semi-ouverte plutôt que gigantesque** : cabane centrale, sentiers vers les générateurs, hors-piste entre les deux. Plus facile à mettre en scène et plus léger pour Roblox.
- **Heatmaps maison** : l'enregistreur de données note la position des joueurs toutes les X secondes pour voir où ils passent, se perdent et meurent. Les mêmes données alimentent la détection d'habitudes.

## 2. Le rythme

- **Règle des 60 s appliquée à la peur.** En plus de la jauge de tension, le Directeur garantit qu'un joueur ne reste jamais plus de N secondes sans le moindre stimulus (bruit, silhouette, branche qui craque), N dépendant de la phase. Les trajets entre générateurs deviennent son terrain de jeu.
- **Pas de remplissage** : des nuits denses, et **une variation par nuit** pour ne jamais rejouer la même :
  - brouillard ;
  - carburant à porter jusqu'au générateur ;
  - plusieurs générateurs éloignés en panne en même temps ;
  - panne de la lumière de la cabane.
- **Varier la réparation** d'une nuit à l'autre pour ne pas refaire 15 fois le même mini-jeu.
- **Les moments calmes ont de la valeur** : réparer en écoutant la forêt fait partie de l'expérience.

## 3. Le son et la musique

- **Effet Space Invaders.** Une nappe (drone ou battement de cœur) dont la vitesse et le volume suivent **l'état du Directeur pour ce joueur** (calme, traque, chasse), et **pas la distance exacte du monstre**, sinon on pourrait le pister. Elle s'accélère toujours quand l'état monte : signal constant.
- **Musique en couches** : 3 ou 4 pistes au même tempo (nappe, pulsation, cordes stridentes, percussions de chasse) jouées ensemble et synchronisées. On fait seulement varier leur volume (`TweenService`, `SoundGroup`) selon l'état.
- **Peu de musique** : en horreur, l'**arrivée** de la musique est elle-même un signal. Pas de musique = rien d'imminent.
- **Occlusion du son** : un rayon entre la source et l'oreille ; s'il touche un mur ou un rocher, un `EqualizerSoundEffect` étouffe le son. Réverbération différente dans la cabane et dans la forêt (`ReverbSoundEffect`). Les joueurs localisent mieux le monstre, ce qui rend le jeu plus juste.
- **Un échantillon, mille variantes** : sons d'ambiance ponctuels (vent, oiseaux, branches) à des positions et intervalles aléatoires, avec une hauteur qui varie de ±5 à 10 %. Jamais de boucle reconnaissable. Même principe pour les cris du monstre.
- **Précharger tous les sons de peur** (`ContentProvider:PreloadAsync`) au début de la nuit : un screamer en retard de 300 ms est raté.
- **Garder le monstre audible** : la musique baisse automatiquement quand un son du monstre joue.

## 4. Immersion et interface

- **Interface intégrée au monde au maximum**, sans barres :
  - endurance : respiration plus forte et flou ;
  - batterie de la lampe : faisceau qui faiblit et clignote ;
  - blessure : boiterie et vignette ;
  - générateur : son et lumière qui montent.
  La dashcam porte sa propre interface (REC, heure, batterie).
- **Faune vivante et silence.** Corbeaux, cerfs et hiboux suivent leur propre vie. **Près du monstre, la faune se tait ou fuit** : c'est un **nouveau signal constant** à ajouter à la liste du doc [13](13-lecons-ia-jeu-video.md).
- **Micro-détails** : tente déchirée, sac abandonné, traces, griffures, surtout près des sentiers. Le monstre immobile au fond, perdu parmi les détails, devient un jeu de « trouve le monstre ».
- **La faiblesse fait peur, pas les graphismes** (The Long Dark) : pas d'arme, lumière limitée, essoufflement.
- **Conséquences visibles** : quand un joueur meurt ou est enlevé, **sa lampe tombe et reste allumée** à cet endroit. C'est un repère sinistre, un objet récupérable, et une matière pour le mimic.
- **Pas de téléportation pour les joueurs** : la distance fait partie du jeu. Les générateurs éloignés rapportent plus, mais y aller seul est risqué.
- **Hyper-réaliste à l'image, simple dans les règles** : pas de poids d'inventaire ni de survie complexe.

## 5. Discrétion et alerte (Splinter Cell)

- **Niveau d'alerte global, progressif et réversible.** Si le groupe est imprudent (sprint permanent, lampes toujours allumées, tout le monde dispersé), le Directeur monte d'un cran :
  - le monstre patrouille davantage ;
  - il **attend près des générateurs** au lieu de rôder ;
  - moins de pitié ;
  - griffures fraîches et générateurs sabotés comme indices.
  Le niveau redescend si le groupe redevient prudent. C'est un état de groupe, différent des contre-mesures par habitude du doc 13.
- **Bruit des pas honnête.** Le volume des pas dépend du sol (`Humanoid.FloorMaterial` : gravier ou branches = fort, mousse ou terre = faible), et **les mêmes valeurs** servent au rayon d'écoute du monstre. Le joueur entend son propre niveau de bruit.
- **Savoir si on est caché**, sans barre : feuillage devant la caméra dans un buisson, vignette plus sombre lampe éteinte.
- **Mode infrarouge de la dashcam** : voir dans le noir **sans émettre de lumière**, avec un écran granuleux, un champ réduit et une batterie limitée. La lampe éclaire mais trahit ; l'infrarouge est discret mais pauvre.
- **Le monstre enquête sur les changements** : porte laissée ouverte, générateur relancé, objet déplacé. En option, un objet à lancer pour faire diversion.
- **Garder l'identité** : pas d'armes, pas de virage action. Se cacher et attendre reste une stratégie valable, dans la limite des contre-mesures.

## 6. Introduction et narration (Half-Life)

- **Jour 1 sans tutoriel.** Arrivée scénarisée où l'on garde le contrôle (camionnette qui dépose le groupe, marche jusqu'au camp). Une voix à la radio raconte pendant que les joueurs testent le sprint, la lampe et la caméra.
- **L'interface apparaît en ramassant les objets** : REC en prenant la dashcam, indicateur de lampe en prenant la lampe.
- **Montrer chaque capacité avant de l'utiliser contre les joueurs.** Par exemple, on voit le monstre grimper la tour au loin avant qu'il ne grimpe pour attraper quelqu'un.
- **Scènes « pas ma guerre ».** Les joueurs voient de loin le monstre faire autre chose (traîner une carcasse de cerf, chasser un animal). Ça montre sa puissance sans viser personne : une nouvelle intention « Spectacle » pour le Directeur.
- **Montrer plutôt qu'écrire** : pas de notes ou d'enregistrements comme source principale de l'histoire.

## 7. Monétisation éthique (microtransactions)

- **Rien de payant ne change le rapport de force avec le monstre** : pas de batterie plus longue, d'endurance, de résurrection ni de lampe plus puissante. Seulement du cosmétique, sans effet sur la visibilité (même faisceau quelle que soit la skin de lampe), et éventuellement des serveurs privés.
- **Les achats ne sont jamais une donnée du Directeur** : pitié, difficulté et choix de cible ignorent totalement qui a payé.
- **Pas de hasard payant** (loot boxes). Si un jour il y en a, Roblox impose d'afficher les probabilités et de vérifier `PolicyService` selon le pays. Plus simple : ne jamais en faire.
- **Pas de FOMO** : les objets d'événement reviennent ou restent obtenables.
- **Progression par l'exploit** : badges (`BadgeService`) comme « survivre à la nuit 5 sans mort » ou « trouver les 5 enregistrements cachés ».
- **Analytique honnête** (`AnalyticsService`) pour voir à quelle nuit les groupes abandonnent et corriger le design, jamais pour placer une boutique au point de frustration.
- **Jeu entièrement jouable gratuitement** : un jeu coop a besoin de groupes.

## 8. Simplicité (RTS)

- **Résister à l'empilement de mécaniques** côté joueur. Le noyau reste : se déplacer, sprinter, lampe, réparer, se cacher, dashcam. Chaque ajout doit en remplacer un ou être vraiment nécessaire.
- **Cible : un groupe d'amis en coop détente**, pas de classement ni de chronomètre à l'écran.
- **L'asymétrie est la force du jeu** : inutile d'équilibrer le monstre comme un joueur.

---

## Pistes à analyser plus tard
- **DÉCOUVERTE - Blair Witch** (https://www.youtube.com/watch?v=elBG1cY8ZyA, 1 h 07) : horreur en forêt avec un caméscope, très proche de notre concept. C'est un let's play commenté, mais les réactions peuvent être utiles.
- **Ces jeux qui m'ont marqué** : Batman Arkham Asylum, Outer Wilds.
