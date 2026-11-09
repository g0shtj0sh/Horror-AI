# 02 — Gameplay

## Objectif des joueurs
- **Réparer les générateurs** et les garder en marche.
- **Survivre 5 nuits.**
- Multijoueur (plusieurs joueurs contre le monstre IA).

## Cycle jour / nuit
| Période | Durée réelle |
|---|---|
| Jour | **10 minutes** |
| Nuit | **15 minutes** |

Déroulé : Jour 1 → Nuit 1 → Jour 2 → Nuit 2 → … → Jour 5 → Nuit 5. Victoire si au moins un joueur survit à la fin de la nuit 5 (règle exacte à confirmer, voir [10-decisions.md](10-decisions.md)).

Durée totale d'une partie : 5 × (10 + 15) = **125 minutes** maximum.

Le niveau de menace du monstre augmente à chaque période (détail dans [04-phases.md](04-phases.md)).

## La map
- **Une seule map fixe** pour commencer, pas très grande.
- Style **forêt**, comme la map de la vidéo de référence : détails et captures dans [11-map.md](11-map.md). (Les images Backrooms ne servaient qu'à montrer la caméra.)
- Besoins pour l'IA : des zones ouvertes et des cachettes (angles, buissons, rochers, pièces sombres), des endroits isolés pour déposer les joueurs enlevés, des éléments à exploiter (lumières, portes).

## Les générateurs
- **Emplacements prédéfinis** dans la map ; à chaque partie, les générateurs sont placés **aléatoirement** parmi ces emplacements.
- Les joueurs les réparent. Le monstre peut **les casser ou les couper** (outil pour séparer le groupe et attirer des joueurs).
- Un générateur en panne affiche un indicateur visible (« EN PANNE » / « BROKEN » dans la vidéo).
- À définir : que se passe-t-il si trop de générateurs sont en panne ? (voir [10-decisions.md](10-decisions.md))

## Les joueurs
- **Première personne.**
- **Lampe torche** (touche dédiée, ex. F). Faisceau assez étroit : dans le noir, on ne voit que ce qui est éclairé.
- **Endurance (stamina)** pour sprinter (ex. Shift), avec une barre à l'écran.
- **Vie** : le monstre peut blesser (frapper, commencer à dévorer). **Aucun malus** de vitesse ou autre après une blessure.
- Interface : nom, statut (vivant/mort), heure ou période, barre d'endurance.

## Caméra et style visuel (système déjà existant chez le créateur)
- Style **le plus réaliste possible**.
- Effet **« dashcam »** : vignettage sombre, objectif légèrement déformé, léger balancement et inclinaison de la tête en marchant, exposition qui écrase les zones sombres en noir.
- **Bandes noires** sur les côtés (format presque carré) : **désactivées par défaut, réactivables dans les paramètres**.
- Lampe torche avec bras visibles (view model).

> L'IA devra pouvoir lire l'état de la lampe de chaque joueur (allumée/éteinte, direction). À brancher sur le système existant le moment venu.

## Générateurs : nombre
- **5 générateurs** par partie, compteur **« 0/5 »** à l'écran.

## Mort et spectateurs
- **Revive (payant)** : possible **autant de fois qu'on veut**, **sauf en nuit 5**. Le joueur a **1 minute** après sa mort pour l'acheter ; passé ce délai, il reste spectateur. Le corps d'un joueur revive disparaît.
- Quand un joueur meurt, **son corps reste dans la map** à l'endroit de la mort (sauf si le monstre l'utilise pour le mimic, voir [05-scenarios.md](05-scenarios.md)).
- Les morts deviennent **spectateurs** et regardent les joueurs encore en vie.
- Les morts ont un **chat réservé aux morts**. Ils ne peuvent **plus parler aux vivants** (indispensable pour le mimic).
- Limite connue : impossible d'empêcher un appel vocal externe (Discord) entre amis.
