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

> **Décisions du créateur (prioritaires sur le reste du document)**
> - Le **silence** fait aussi peur : pas de stimulus obligatoire toutes les N secondes.
> - **Aucune musique en partie** (seulement dans le lobby).
> - **Aucun animal visible** : la faune n'existe que par le son.
> - **Pas de tutoriel**, et le monstre **ne montre pas ses capacités à l'avance** : les joueurs les découvrent.
> - **Monétisation** : gamepass **infrarouge**, **revive** pas cher, **loot boxes de cosmétiques**. Aucun traitement de faveur du monstre envers les joueurs qui ont payé.

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

- ~~Règle des 60 s~~ **Rejetée.** Le silence fait aussi peur : juste après une attaque, **il ne se passe rien pendant un bon moment**, et c'est ce vide qui fait monter la tension. Le Directeur utilise le silence comme un outil à part entière (intention « Silence »), pas comme un trou à combler. Les trajets entre générateurs restent son terrain de jeu, mais il choisit librement d'y agir ou non.
- **Pas de remplissage** : des nuits denses, et **une variation par nuit** pour ne jamais rejouer la même :
  - brouillard ;
  - carburant à porter jusqu'au générateur ;
  - plusieurs générateurs éloignés en panne en même temps ;
  - panne de la lumière de la cabane.
- **Varier la réparation** d'une nuit à l'autre pour ne pas refaire 15 fois le même mini-jeu.
- **Les moments calmes ont de la valeur** : réparer en écoutant la forêt fait partie de l'expérience.

## 3. Le son et la musique

- **Aucune musique en partie.** La musique n'existe que dans le **lobby**, avant de lancer une partie. En jeu, tout passe par les **sons du monde** (vent, forêt, pas, monstre) et le silence.
- ~~Nappe qui accélère, musique en couches~~ : abandonnées avec la musique. Éventuellement, la **respiration et le cœur du personnage** (sons du corps, pas de la musique) peuvent s'accélérer quand le joueur court ou a peur.
- **Occlusion du son** : un rayon entre la source et l'oreille ; s'il touche un mur ou un rocher, un `EqualizerSoundEffect` étouffe le son. Réverbération différente dans la cabane et dans la forêt (`ReverbSoundEffect`). Les joueurs localisent mieux le monstre, ce qui rend le jeu plus juste.
- **Un échantillon, mille variantes** : sons d'ambiance ponctuels (vent, oiseaux, branches) à des positions et intervalles aléatoires, avec une hauteur qui varie de ±5 à 10 %. Jamais de boucle reconnaissable. Même principe pour les cris du monstre.
- **Précharger tous les sons de peur** (`ContentProvider:PreloadAsync`) au début de la nuit : un screamer en retard de 300 ms est raté.
- **Garder le monstre audible** : l'ambiance baisse légèrement quand un son du monstre joue.

## 4. Immersion et interface

- **Interface intégrée au monde au maximum**, sans barres :
  - endurance : respiration plus forte et flou ;
  - batterie de la lampe : faisceau qui faiblit et clignote ;
  - blessure : boiterie et vignette ;
  - générateur : son et lumière qui montent.
  La dashcam porte sa propre interface (REC, heure, batterie).
- **Faune uniquement sonore et silence.** **Aucun animal visible** dans le jeu, mais l'ambiance contient des sons d'animaux (oiseaux, hiboux, insectes, branches). **Près du monstre, ces sons se taisent** : c'est un **nouveau signal constant**, purement sonore, à ajouter à la liste du doc [13](13-lecons-ia-jeu-video.md).
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
- **Mode infrarouge de la dashcam (gamepass payant)** : voir dans le noir **sans émettre de lumière**, avec un écran granuleux, un champ réduit et une batterie limitée. La lampe éclaire mais trahit ; l'infrarouge est discret mais pauvre. Voir la section monétisation.
- **Le monstre enquête sur les changements** : porte laissée ouverte, générateur relancé, objet déplacé. En option, un objet à lancer pour faire diversion.
- **Garder l'identité** : pas d'armes, pas de virage action. Se cacher et attendre reste une stratégie valable, dans la limite des contre-mesures.

## 6. Introduction et narration (Half-Life)

- **Pas de tutoriel, aucune explication.** Les joueurs apparaissent directement à un endroit (la cabane par exemple) et comprennent seuls.
- **Seul guidage : les générateurs.**
  - un compteur discret **« 0/5 »** (générateurs réparés / total) ;
  - les générateurs en panne sont **éteints ou cassés, avec de la fumée**, et un indicateur « en panne » ;
  - en s'approchant : **« E » pour réparer / allumer**, une durée de réparation, et un **QTE très simple**.
  Tout le monde comprend sans explication.
- **Le monstre ne montre pas ses capacités à l'avance.** C'est aux joueurs d'apprendre de quoi il est capable en le voyant agir. Les signaux sonores constants ([13](13-lecons-ia-jeu-video.md)) suffisent pour que ce soit juste : on prévient du **danger**, pas de la **capacité**. C'est l'équilibre recherché : trop d'explications rendraient le jeu trop simple.
- **Scènes « spectacle »** (le monstre aperçu au loin en train de faire autre chose) : **à voir**, idée en réserve, pas prioritaire.
- **Montrer plutôt qu'écrire** : pas de notes ou d'enregistrements comme source principale de l'histoire.

## 7. Monétisation (décision du créateur)

Le jeu doit rapporter sur Roblox. Ce qui est décidé :

| Achat | Type | Effet |
|---|---|---|
| **Mode infrarouge** de la dashcam | Gamepass | Voir dans le noir sans lumière (champ réduit, grain, batterie limitée) |
| **Revive** | Achat (prix bas) | Revenir en jeu après la mort : **illimité**, **impossible en nuit 5**, à acheter **dans la minute** qui suit la mort |
| **Loot boxes** | Achat | **Cosmétiques uniquement** |

Règles :
- **Aucun traitement de faveur** : le monstre chasse et tue les joueurs qui ont payé exactement comme les autres. L'argent n'est jamais une donnée du Directeur.
- **Loot boxes = cosmétiques seulement**, rien qui aide contre le monstre. Roblox **impose** d'afficher les **probabilités** de chaque objet, et de vérifier `PolicyService:GetPolicyInfoForPlayerAsync()` (`ArePaidRandomItemsRestricted`) : dans certains pays, les loot boxes payantes doivent être désactivées pour le joueur.
- **Les cosmétiques ne changent pas la visibilité** (même faisceau de lampe quelle que soit la skin).
- **Le jeu reste jouable gratuitement** du début à la fin.
- **Analytique** (`AnalyticsService`) pour voir à quelle nuit les groupes abandonnent et corriger le design.
- **Badges** d'exploit (`BadgeService`) : « survivre à la nuit 5 sans mort »…

Points d'attention :
- **Revive et mimic.** Le mimic ment en disant « j'ai été revive ». Si le revive existe vraiment, **le mensonge devient crédible**, ce qui rend le mimic encore plus efficace. À l'inverse, il faut que le vrai revive ait des **règles claires** (où réapparaît-on, combien de fois par partie) pour que les joueurs ne puissent pas démasquer le mimic trop facilement ni trop difficilement.
- **Règles du revive (décidées)** : autant de fois qu'on veut, **sauf en nuit 5** où c'est impossible ; le joueur a **1 minute** après sa mort pour l'acheter, sinon il reste spectateur.
- **Revive et corps** : quand un joueur est revive, **son corps disparaît**. Le mimic ne peut donc utiliser que les morts qui n'ont **pas** été revive (fenêtre d'une minute passée).
- **Revive et mimic en nuit 5** : comme le revive est impossible en nuit 5, un mimic qui dit « j'ai été revive » **pendant la nuit 5** se trahit pour un joueur attentif. Le Directeur doit donc :
  - faire arriver le mimic **pendant le jour 5** (où le revive est encore possible), ou juste avant la tombée de la nuit ;
  - en nuit 5, utiliser une **autre excuse** (« j'étais caché », « je me suis perdu », « j'avais pas de lampe ») ;
  - un joueur qui remarque l'incohérence a **gagné à la réflexion** : c'est le bon équilibre.
- **Infrarouge** : le monstre doit rester redoutable face à un joueur en infrarouge (il peut le voir aussi bien qu'avec une lampe éteinte ; la gamepass aide à voir, pas à être invisible).

## 8. Simplicité (RTS)

- **Résister à l'empilement de mécaniques** côté joueur. Le noyau reste : se déplacer, sprinter, lampe, réparer (E + QTE simple), se cacher, dashcam. Chaque ajout doit en remplacer un ou être vraiment nécessaire.
- **Cible : un groupe d'amis en coop détente**, pas de classement ni de chronomètre à l'écran.
- **L'asymétrie est la force du jeu** : inutile d'équilibrer le monstre comme un joueur.

---

## Pistes à analyser plus tard
- **DÉCOUVERTE - Blair Witch** (https://www.youtube.com/watch?v=elBG1cY8ZyA, 1 h 07) : horreur en forêt avec un caméscope, très proche de notre concept. C'est un let's play commenté, mais les réactions peuvent être utiles.
- **Ces jeux qui m'ont marqué** : Batman Arkham Asylum, Outer Wilds.
