# Prompt Vibestarter — Étape 1 : déplacements et sons de pas

```
Tu travailles sur mon jeu Roblox d'horreur multijoueur en première personne, hyper-réaliste, dans Roblox Studio.

## 1. Lis d'abord la documentation (obligatoire, avant de toucher à quoi que ce soit)
Dépôt GitHub : https://github.com/g0shtj0sh/Horror-AI
Branche : claude/elegant-thompson-8cnt9v (toute la doc est sur cette branche, pas sur main)

Lis au minimum :
- README.md (sommaire)
- docs/01-vision.md, docs/02-gameplay.md (le jeu, les joueurs, la caméra)
- docs/06-sons-et-effets.md (règles audio, sources de sons libres de droits, liste de courses)
- docs/15-lecons-bazar-du-grenier.md, section 5 « Discrétion et alerte » (bruit des pas selon le sol)
- docs/10-decisions.md (toutes les décisions prises : elles sont prioritaires)
Survole le reste pour comprendre le projet (l'IA du monstre viendra plus tard, n'y touche pas).

## 2. Comment on travaille
- On avance ÉTAPE PAR ÉTAPE. Cette session ne concerne QUE l'étape décrite ci-dessous. Ne commence pas d'autres systèmes (HUD, générateurs, monstre, map…).
- Avant de modifier, INSPECTE ce qui existe déjà dans le place et explique-moi brièvement comment c'est organisé.
- Ne casse pas l'existant : modifie le système actuel plutôt que de tout réécrire, sauf si c'est vraiment nécessaire (dans ce cas, explique pourquoi avant).
- Mets toutes les valeurs réglables (vitesses, intensités, volumes…) dans un ModuleScript de configuration unique, bien commenté en français, pour que je puisse les ajuster moi-même sans lire le code.
- Code propre en Luau, commenté en français, séparé client / serveur correctement.
- À la fin : fais-moi un récap clair (ce que tu as changé, où sont les scripts, quelles valeurs je peux régler, comment tester) et liste ce qui reste à faire.

## 3. Ce qui existe déjà
Un système de caméra première personne avec :
- les animations de marche, de course (sprint) et d'accroupissement ;
- la lampe torche.
Il n'y a PAS encore de HUD (ne pas en créer pour l'instant).

## 4. L'étape à faire maintenant

### A. Réglages de déplacement
- Marche un peu plus rapide qu'actuellement.
- Sprint nettement plus rapide qu'actuellement.
- Accroupi : garder lent et discret.
- Mets ces trois vitesses dans le module de configuration.

### B. Caméra moins « cinématique »
La caméra est actuellement trop smooth, trop cinématique. Je veux un rendu plus brut, plus « vraie personne qui filme » (effet dashcam / found footage réaliste) :
- moins de lissage / d'inertie sur les mouvements de la caméra ;
- balancement de tête (head bob) plus naturel et lié à la vitesse (léger en marche, plus marqué en sprint, très faible accroupi) ;
- garde l'effet réaliste mais sans le côté « travelling de film ».
- Toutes les intensités dans le module de configuration.

### C. Sons de pas selon la surface
- Détecte la surface sous le joueur (Humanoid.FloorMaterial, et/ou un attribut personnalisé sur les parts pour les cas spéciaux : planches de la cabane, gravier, etc.).
- Un jeu de sons différent par type de surface : herbe, terre/boue, gravier, feuilles/branches, bois (cabane), roche, eau peu profonde (si possible).
- Plusieurs variantes par surface (3 à 5), jouées au hasard avec une légère variation de hauteur (PlaybackSpeed ±5 à 10 %) pour éviter la répétition.
- Rythme des pas synchronisé avec l'animation / la vitesse : marche, sprint (plus fort et rapide), accroupi (très faible).
- Sons spatialisés en 3D (mono), audibles par les AUTRES joueurs à proximité, pas seulement par le joueur lui-même.
- Sources : utilise les sites indiqués dans docs/06-sons-et-effets.md (Freesound filtré CC0, bibliothèque audio Roblox…). Respecte les règles de licence (CC0 en priorité, jamais de NC). Prépare les sons (silence de début coupé, volume normalisé, mono). Note chaque son utilisé (nom, site, lien, licence, ID Roblox) dans un fichier/liste que tu me donneras à la fin pour que je l'ajoute à docs/assets.md.

### D. Préparer le terrain pour l'IA (très important, mais SANS coder l'IA)
Le monstre devra plus tard « entendre » les pas. Pour ça :
- Chaque surface a un « niveau de bruit » (ex. gravier/branches = fort, mousse/terre = faible), et chaque allure un multiplicateur (accroupi < marche < sprint). Mets ces valeurs dans le module de configuration.
- Le volume des pas entendus en jeu doit découler de CES MÊMES valeurs (le joueur entend son propre niveau de bruit : c'est une règle d'équité du jeu).
- À chaque pas, côté serveur, émets un événement de bruit (BindableEvent ou équivalent) contenant : le joueur, la position, le rayon/niveau de bruit. Personne ne l'écoute encore : c'est pour l'IA plus tard. Documente-le dans ton récap.

## 5. Ne fais PAS
- Pas de HUD, pas de barre d'endurance à l'écran (l'endurance sera montrée plus tard par la respiration).
- Pas de musique.
- Pas de monstre, pas d'IA, pas de générateurs, pas de map.
- Ne modifie pas la lampe torche, sauf si un bug t'en empêche (dans ce cas, demande-moi).

Si quelque chose n'est pas clair ou si une décision m'appartient, pose-moi la question plutôt que de deviner.
```
