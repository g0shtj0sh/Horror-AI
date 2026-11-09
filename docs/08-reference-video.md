# 08 — Analyse de la vidéo de référence

- **Titre** : « I Made a Roblox Game To HUNT Youtubers »
- **Auteur** : Azerr — https://www.youtube.com/watch?v=6nqiEeuaBZI
- **Durée** : 31 min 28 s
- **Concept** : Azerr joue lui-même le monstre en faisant croire à 5 YouTubers que c'est une IA.
- **Inspiration déclarée** : la série analog *Vita Carnis*. ⚠️ On ne reprend **ni la créature, ni son nom, ni son design**.

Analyse faite à partir de la transcription, de la description, des images et d'une mesure du volume sonore seconde par seconde.

## Le jeu dans la vidéo
- Map : forêt avec une cabane et une tour de guet, 5 zones reliées par des chemins, cachettes (buissons, rochers).
- 5 générateurs, un par zone, pour séparer les joueurs. Indicateur « BROKEN » quand ils sont en panne.
- Une nuit de 1 h à 9 h en jeu = 45 minutes réelles.
- Interface joueur : nom + statut (Alive), heure, barre d'endurance, « [F] for Flashlight », « [Shift] to Sprint ».
- Lampe torche avec bras visibles (view model).

## Capacités du monstre (joué par un humain)
1. **Fantôme** : disparaît quand on le regarde.
2. **Ramper** : silencieux, contrairement à la marche (pas lourds).
3. **Attraper** un joueur et l'emmener n'importe où.
4. **Mimic** : imiter un joueur (pas, lampe, apparence), même mort.
5. **Blesser** au clic quand un joueur est proche.
6. Couper les générateurs à volonté.
7. Grimper (la tour n'était pas sûre).

Sa vue de monstre : éclairée comme en plein jour, avec panneaux « Generators » (Gen 1–5) et « Noises » (Blood 1/2/3, Growl, Long Growl, Cut, Twig).

## Ce qui a fait peur (d'après les réactions)
- **Les bruits avant toute apparition** : « j'ai entendu une branche craquer », grognements, herbe.
- **Un seul joueur voit le monstre**, les autres ne le croient pas.
- **Le corps retrouvé** : « j'ai tourné au coin et j'ai vu Cash en morceaux ».
- **Être emporté vivant** sans savoir où : « la pire expérience de ma vie ».
- **Les sons d'attaque entendus de loin** : « j'ai entendu un bruit de sang », « un crunch ».
- **Le corps qui disparaît** juste avant le mimic.
- Le mimic a été **démasqué** car le joueur imité était mort depuis longtemps et tout le monde le savait.
- Phrases du mimic qui ont fait réagir (« let's be friends », « I love spending time with you »).

## Chronologie de la peur (pics sonores pendant la partie)
| Heure en jeu | Ce qui se passe |
|---|---|
| 2 h | Calme. Le monstre observe à découvert, invisible pour les joueurs. |
| 3 h | Premières apparitions au loin dans le faisceau, derrière un tronc. Premier screamer en gros plan. |
| 4 h | Enlèvement (écran rouge sombre, flou), chasses, réparations sous pression. |
| 5 h | **Pic** : screamers rapprochés, monstre qui surgit dans la lampe, écran rouge pendant les mises à mort. |
| 7 h | Fin : dernière chasse, mimic. |

Pics de volume détectés (temps dans la vidéo) : 14:25, 14:40, 15:42, 16:57, 17:11, 18:18, 19:50, 20:03–20:21 (série), 21:13, 22:32, 22:54, 23:02, 24:25, 25:07, 27:56, 29:53.

## Leçons pour notre IA
- La peur suit une courbe : observer → bruits → apparitions → chasse → morts → mimic.
- Le **son** fait autant que l'image.
- Le **faisceau de lampe** est la scène idéale des screamers.
- Le mimic doit choisir un mort **dont la mort n'est pas connue** de tous.
- Les attaques doivent s'**entendre de loin** pour terrifier aussi ceux qui ne voient rien.
- Un humain improvise : notre IA doit avoir **assez de variété** pour ne pas être prévisible.
