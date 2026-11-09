# 06 — Sons et effets de peur

Les sons sont l'arme principale du monstre dans les premières phases. Le Directeur choisit **quel son**, **où** (à quelle distance de quel joueur) et **quand**.

## Bibliothèque de sons (à créer ou trouver, libres de droits)

| Catégorie | Exemples | Phases |
|---|---|---|
| Ambigus | Branche qui craque, brindille, feuilles, herbe qui bouge, caillou qui roule | Dès le Jour 1 |
| Présence | Pas lourds (marche), respiration, reniflement | Nuit 1+ |
| Menace | Grognement court, grognement long, cri lointain | Jour 2+ |
| Environnement | Lumière qui grésille, générateur qui s'étouffe, porte | Nuit 1+ |
| Attaque | Coups, craquements, « sang », dévoration (doivent **porter loin**) | Nuit 3+ |
| Imitation | Pas d'un joueur, son de lampe qui s'allume, voix ou bruits d'un joueur | Nuit 4+ |
| Screamer | Cri soudain très fort, coup de son sec | Jour 3+ |

Dans la vidéo de référence, le panneau « Noises » du monstre contenait : Blood 1/2/3, Growl, Long Growl, Cut, Twig. **Les joueurs reconnaissaient le grognement** et paniquaient dès qu'ils l'entendaient : c'est un signal à exploiter.

## Pas de musique en partie
- **Aucune musique pendant la partie** : seulement dans le lobby.
- L'ambiance vient du vent, de la forêt, des **sons d'animaux (aucun animal visible)** qui **se taisent près du monstre**, et du **silence**.

## Règles pour les sons
- **Spatialisés** (3D) : le joueur doit pouvoir deviner la direction.
- Joués **proches** d'un joueur pour le faire douter (« c'était quoi ? »), sans que ça devienne une alarme évidente au début.
- **Pas de répétition** du même son trop souvent.
- Marcher = bruyant, ramper = silencieux.

## Effets visuels
- **Écran rouge sombre + flou** quand le joueur est attrapé, blessé ou dévoré.
- **Secousse de caméra** à la capture et aux screamers.
- **Lampe qui tombe** pendant un enlèvement.
- **Lumières qui grésillent ou s'éteignent** à l'approche du monstre.
- **Screamer** : gros plan soudain du monstre, souvent dans le faisceau de la lampe.

## Ce que la vidéo montre sur les screamers
- Le plus efficace : **le monstre qui surgit dans le faisceau de la lampe** ou derrière un tronc.
- Les pics de frayeur augmentent nettement en fin de nuit (voir [08-reference-video.md](08-reference-video.md)).

## Sources de sons libres de droits (pour le Claude de Vibestarter)

Même principe que pour les textures ([11-map.md](11-map.md)) : le Claude connecté via Vibestarter télécharge et uploade lui-même ; le créateur vérifie à l'oreille et remplace ce qui ne lui plaît pas.

### Avec API (à utiliser en automatique)
| Site | API | Licence | Remarques |
|---|---|---|---|
| **Freesound** — https://freesound.org | https://freesound.org/docs/api/ (APIv2) | **Filtrer sur CC0** (`filter=license:"Creative Commons 0"`) | La plus grosse banque de bruitages (branches, pas dans les feuilles, respirations, craquements, grognements). **Clé API gratuite** à créer sur le compte du créateur. Avec une simple clé, on récupère les **aperçus haute qualité** (MP3/OGG) ; le fichier original demande une connexion OAuth2. |
| **Roblox Creator Store** (audio) | Recherche dans Studio / Toolbox | Sons **déjà licenciés par Roblox** pour les jeux Roblox | Pratique : aucun upload, aucune modération à attendre. Vérifier que le son est bien utilisable dans tous les jeux (sons publics Roblox). |

### Sans API (téléchargement manuel par le créateur)
- **Sonniss – GDC Game Audio Bundle** — https://sonniss.com/gameaudiogdc : des dizaines de Go de bruitages professionnels, **gratuits et utilisables commercialement** (pas de revente des sons seuls). Excellent pour la forêt, le vent, les impacts.
- **Kenney** — https://kenney.nl/assets?q=audio : packs **CC0**.
- **OpenGameArt** — https://opengameart.org (filtrer CC0) : qualité variable.
- **Mixkit** — https://mixkit.co/free-sound-effects/ : licence gratuite, usage commercial autorisé.
- ⚠️ À éviter : **BBC Sound Effects** (licence non commerciale) et tout son marqué **CC-BY-NC** sur Freesound.

### Règles
- **Licences acceptées** : CC0 en priorité. CC-BY possible **seulement** si l'auteur est crédité (écran des crédits du jeu). **Jamais de NC** (NonCommercial) : le jeu est monétisé.
- **Tenir la liste** des sons utilisés (nom, site, lien, licence, auteur, ID Roblox) dans `docs/assets.md`.
- **Upload Roblox** : formats `.mp3` ou `.ogg` (aussi `.wav` / `.flac`), fichiers courts, passage par la **modération** (prévoir un délai) et une **limite mensuelle d'uploads audio** par compte.
- **Préparer les sons** avant l'upload : couper les silences au début (un screamer doit partir instantanément), normaliser le volume, **mono** pour les sons spatialisés 3D (le monstre, les pas), stéréo seulement pour l'ambiance non spatialisée.
- **Varier** : plusieurs prises de chaque son (3 à 5 craquements de branche, 4 grognements…) jouées au hasard avec une légère variation de hauteur.

### Liste de courses (à chercher en priorité)
| Catégorie | Mots-clés Freesound |
|---|---|
| Ambiance forêt de nuit | `night forest ambience`, `wind trees`, `crickets night`, `owl` |
| Signaux ambigus | `twig snap`, `branch break`, `leaves rustle`, `footsteps leaves` |
| Monstre | `growl creature`, `breathing monster`, `sniffing`, `low growl`, `wet flesh` |
| Attaque | `bone crack`, `flesh tear`, `gore squelch`, `scream` |
| Environnement | `generator start`, `generator failure`, `electric buzz`, `light flicker`, `door creak` |
| Joueur | `footsteps gravel`, `footsteps grass`, `heavy breathing`, `heartbeat`, `flashlight click` |
