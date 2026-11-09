# 07 — La vue debug

Outil réservé au développeur pour **voir ce que l'IA pense** et régler le jeu. Désactivée pour les vrais joueurs.

## La caméra
- **Troisième personne**, derrière et au-dessus du monstre, qui le suit.
- **Vision nocturne pour le développeur** : la scène est éclaircie comme en plein jour, même en pleine nuit. Ça ne concerne **que l'affichage**, pas la perception de l'IA (qui, de toute façon, connaît tout).

## Les informations affichées
- **Tous les joueurs**, en permanence, surlignés.
- Pour chaque joueur : **jauge de tension**, état (caché, en groupe, seul, lampe allumée), et **ce que le monstre a décidé à son sujet** (« ignorer pour l'instant », « faire douter », « traquer », « attaquer »…).
- **Faisceaux des lampes** visibles.
- **Le chemin prévu** par le monstre, tracé au sol.
- **Au-dessus de la tête du monstre** : son intention et la raison. Exemple : « Joueur 2 isolé depuis 40 s → approche discrète ».
- Phase en cours, niveau de menace, délais (cooldowns) restants.
- Panneau des générateurs (état de chacun).

## Commandes
- Touche pour activer/désactiver la vue debug.
- Passer d'un joueur à l'autre pour voir sa tension en détail.
- (Plus tard) Forcer une intention ou une phase pour tester un scénario précis.

## Inspiration
Dans la vidéo, la vue d'Azerr (le monstre) était déjà éclaircie comme en plein jour, avec des panneaux « Generators » et « Noises ». Notre vue debug, c'est ça, mais pour **regarder l'IA travailler** au lieu de jouer soi-même.
