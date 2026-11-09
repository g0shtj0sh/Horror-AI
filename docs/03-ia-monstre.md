# 03 — L'IA du monstre

## Architecture générale

L'IA est découpée en trois couches :

```
┌──────────────────────────────────────────┐
│  DIRECTEUR (le cerveau, metteur en scène) │  ← décide QUOI faire et QUAND
│  - lit l'état de la partie                │
│  - mesure la tension de chaque joueur     │
│  - choisit une intention                  │
└───────────────────┬──────────────────────┘
                    │ intention (ex. "apparaître à Joueur 2")
┌───────────────────▼──────────────────────┐
│  COMPORTEMENTS (les actions)              │  ← COMMENT le faire
│  traquer, se montrer, enlever, mimic...   │
└───────────────────┬──────────────────────┘
                    │ ordres simples
┌───────────────────▼──────────────────────┐
│  CORPS (le monstre physique)              │  ← déplacement, animations, sons
│  pathfinding, ramper/marcher, attaques    │
└──────────────────────────────────────────┘
```

- **V1** : le Directeur fonctionne avec des **règles** réglables (chiffres simples).
- **V2** : le Directeur peut être remplacé ou assisté par une **IA entraînée** (réseau de neurones entraîné hors de Roblox, en Python, puis exporté en Luau). Voir [09-roadmap.md](09-roadmap.md).

## Principe clé : il sait tout, il fait semblant
- Le monstre **connaît en permanence** : position de chaque joueur, direction de son regard, état de sa lampe, son endurance, sa vie, s'il est seul ou en groupe, depuis combien de temps il ne s'est rien passé pour lui.
- Il **choisit** d'agir ou non. Exemples :
  - Un joueur éteint sa lampe et se cache : le monstre sait où il est, passe à côté, s'arrête, renifle… et repart. Faux sentiment de sécurité. Il revient plus tard.
  - Un joueur se cache toujours au même endroit : le monstre finit par l'**y attendre**.

## Ce que l'IA perçoit (entrées)
Pour chaque joueur :
- position, vitesse, en train de sprinter ou non ;
- direction de la caméra ; **le monstre est-il visible pour lui ?** (dans l'angle de vue + pas de mur entre eux + zone éclairée ou dans le faisceau de la lampe) ;
- lampe allumée/éteinte ;
- endurance, vie ;
- distance au joueur le plus proche (isolé ou en groupe) ;
- est-il en train de réparer un générateur ? caché ?
- messages dans le chat (pour le mimic) ;
- historique : cachettes habituelles, dernière frayeur, nombre de frayeurs reçues.

Pour la partie : période (jour/nuit, numéro), temps restant, état des générateurs, joueurs morts et emplacement des corps.

## La jauge de tension (par joueur)
Chaque joueur a une **tension** de 0 à 100 que l'IA estime en continu.

Ça **monte** quand : bruit proche, apparition, monstre vu, chasse, blessure, ami enlevé ou tué, joueur seul, dans le noir, endurance vide.
Ça **descend** avec le temps calme, en groupe, en lumière, près d'un générateur en marche.

Rythme recherché, comme dans un film d'horreur :

```
tension
 100 |            /\                 /\
     |      /\   /  \          /\   /  \
     |     /  \_/    \        /  \_/    \___
   0 |____/           \______/
     └──────────────────────────────────────→ temps
       montée   pic   répit   montée   pic
```

Règles :
- Un joueur **déjà terrifié** a droit à un **répit** (sinon il s'habitue ou s'énerve).
- Un joueur **trop détendu** reçoit une **surprise**.
- Viser des pics de plus en plus intenses au fil des nuits.

## Le Directeur : comment il choisit
À intervalle régulier (ex. toutes les 1 à 3 secondes), le Directeur :
1. met à jour la tension de chaque joueur ;
2. regarde ce que la **phase actuelle autorise** ([04-phases.md](04-phases.md)) ;
3. choisit une **cible** (souvent : le joueur isolé, le plus détendu, ou celui qui se méfie du mimic) ;
4. choisit une **intention** parmi celles autorisées en donnant un score à chacune (intérêt pour la peur, risque d'être répétitif, temps depuis la dernière fois, situation) ;
5. respecte des **délais** (cooldowns) pour ne pas spammer.

Intentions possibles :

| Intention | Description |
|---|---|
| Observer | Rester à distance, invisible, et étudier |
| Silence | Ne rien faire du tout pendant un long moment, surtout après une attaque |
| Bruit | Jouer un son à un endroit choisi (proche ou loin) |
| Apparaître | Se montrer brièvement (au loin, derrière un arbre, dans le faisceau) puis disparaître |
| Traquer | Suivre un joueur à distance, en rampant (silencieux) |
| Faire semblant | Passer à côté d'un joueur caché sans l'attaquer |
| Saboter | Casser/couper un générateur, faire grésiller une lumière |
| Leurre | Imiter les pas ou la lampe d'un joueur pour attirer un autre joueur |
| Chasser | Poursuite ouverte, bruyante |
| Blesser | Frapper ou commencer à dévorer, puis lâcher |
| Enlever | Attraper un joueur et l'emmener loin |
| Tuer | Mise à mort (laisse un corps) |
| Mimic | Prendre l'apparence d'un mort (nuit 5) |
| Battre en retraite | Partir, laisser un répit |

## Capacités du corps du monstre
- **Marcher** : rapide, **pas lourds et bruyants** (les joueurs l'entendent arriver).
- **Ramper** : plus lent, **silencieux**, idéal pour approcher et les screamers.
- **Courir** en chasse.
- **Fantôme** : disparaître quand il est regardé (surtout en début de partie), réapparaître ailleurs.
- **Grimper** : aucune cachette n'est sûre à 100 % (tour, hauteurs).
- **Attraper et porter** un joueur.
- **Blesser / dévorer**, **tuer**.
- **Jouer des sons** à sa position ou dans l'environnement.
- **Interagir** : générateurs, lumières, portes.
- **Imiter** : apparence, pas, lampe d'un joueur.

## Règles d'équité
- Toujours des indices avant une vraie attaque (bruits, grognements, lumières qui grésillent).
- Le joueur a toujours une chance de fuir (cachette, chemin).
- Pas d'acharnement : délais entre deux grosses actions sur le même joueur.
- Le monstre ne doit jamais être bloqué de façon absurde ni « tricher » visiblement (traverser les murs devant un joueur, etc.).

## Le monstre physique
- **Pas encore de modèle** : un modèle provisoire (silhouette sombre) servira pour les tests.
- Design final : **original**, à créer.

## Règles ajoutées (voir [13-lecons-ia-jeu-video.md](13-lecons-ia-jeu-video.md))
- **Signaux constants** : chaque son du monstre a toujours le même sens (grognement long = chasse, lumières qui grésillent = tout proche…).
- **Annoncer ses intentions** par le son (reniflement, grognement, bruit avant de se déplacer).
- **Contre-mesures débloquées** selon les habitudes des joueurs (cachette fixe, cabane, tour, lampe éteinte…).
- **Pitié cachée** : rater de justesse un joueur qui fuit à bout de souffle, surtout dans les premières nuits.
- **Rencontres assez longues** pour que le joueur voie l'intelligence du monstre.
- **Fenêtres de réaction** : changements de direction lents et sonores.
- **Difficulté adaptative** gérée par le Directeur, pas de modes de difficulté séparés.

## Règles ajoutées (voir [15-lecons-bazar-du-grenier.md](15-lecons-bazar-du-grenier.md))
- **Le silence est un outil** : après une attaque, ne rien faire pendant un bon moment fait monter la tension (intention « Silence »). Pas de stimulus obligatoire.
- **Niveau d'alerte de groupe** progressif et réversible selon l'imprudence du groupe.
- **Bruit des pas selon le sol** : mêmes valeurs pour le son entendu par le joueur et le rayon d'écoute du monstre.
- **Les sons d'animaux se taisent** près du monstre (aucun animal visible, signal purement sonore).
- **Enquêter sur les changements** (porte ouverte, générateur relancé, objet déplacé).
- **Ne pas montrer ses capacités à l'avance** : les joueurs les découvrent quand il agit ; les signaux préviennent du danger, pas de la capacité.
- Intention « Spectacle » (se montrer au loin occupé à autre chose) : en réserve, à voir.
- **Points de révélation** : apparitions placées là où le joueur découvre le paysage.
- **Aucun traitement de faveur** pour les joueurs qui ont payé (infrarouge, revive) : le monstre les chasse comme les autres.
- **Joueur en infrarouge** : aussi repérable qu'un joueur lampe éteinte.
