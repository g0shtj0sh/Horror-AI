# Horror-AI

Jeu d'horreur Roblox multijoueur en première personne où **le monstre est joué par une IA** spécialisée pour faire peur aux joueurs.

Les joueurs doivent **réparer des générateurs et survivre 5 nuits**. Le monstre, lui, sait tout de la partie et choisit à chaque instant *comment* faire le plus peur : bruits, apparitions, traque, enlèvement, mise à mort, imitation d'un joueur mort.

> Statut : **phase de conception**. Tout est documenté ici, le code viendra ensuite.

## Sommaire de la documentation

| Fichier | Contenu |
|---|---|
| [docs/01-vision.md](docs/01-vision.md) | L'idée du jeu, les principes, ce qui le rend unique |
| [docs/02-gameplay.md](docs/02-gameplay.md) | Cycle jour/nuit, générateurs, joueurs, caméra, lampe, mort et spectateurs |
| [docs/03-ia-monstre.md](docs/03-ia-monstre.md) | Le cerveau du monstre : le Directeur, la tension, les capacités |
| [docs/04-phases.md](docs/04-phases.md) | Ce que le monstre a le droit de faire, jour par jour et nuit par nuit |
| [docs/05-scenarios.md](docs/05-scenarios.md) | Les « coups » scénarisés : enlèvement, piège du corps, mimic |
| [docs/06-sons-et-effets.md](docs/06-sons-et-effets.md) | Bibliothèque de sons et effets visuels de peur |
| [docs/07-debug.md](docs/07-debug.md) | La vue debug du développeur (3e personne, vision nocturne, pensées de l'IA) |
| [docs/08-reference-video.md](docs/08-reference-video.md) | Analyse de la vidéo de référence (Azerr) |
| [docs/09-roadmap.md](docs/09-roadmap.md) | Les étapes de développement, de la V1 à l'IA entraînée |
| [docs/10-decisions.md](docs/10-decisions.md) | Toutes les décisions prises et les questions encore ouvertes |
| [docs/11-map.md](docs/11-map.md) | La map : style forêt de la vidéo, lieux, cachettes, besoins de l'IA (avec captures) |
| [docs/12-monstre.md](docs/12-monstre.md) | Le design du monstre et sa génération avec Meshy AI |
| [docs/13-lecons-ia-jeu-video.md](docs/13-lecons-ia-jeu-video.md) | Leçons de la vidéo « Mais pourquoi l'IA est pourrie ? » appliquées à notre monstre |
| [docs/14-navigation.md](docs/14-navigation.md) | Navigation du monstre : navmesh, pathfinding, liens et coûts dans Roblox |
| [docs/15-lecons-bazar-du-grenier.md](docs/15-lecons-bazar-du-grenier.md) | Leçons des autres vidéos du Bazar du Grenier : map, son, immersion, alerte, intro, monétisation |
| [docs/prompts/](docs/prompts/) | Prompts prêts à l'emploi pour le Claude de Vibestarter (Roblox Studio), étape par étape |
| [AI/](AI/) | Le dossier où sera codée l'IA du monstre |

## Organisation du dépôt

```
Horror-AI/
├── README.md        ← ce fichier
├── docs/            ← toute la conception du jeu
└── AI/              ← le code de l'IA (à venir)
```
