# 09 — Roadmap

## Comment on travaille
- Claude écrit les scripts **Luau** dans le dossier [AI/](../AI/) (et d'autres dossiers si besoin).
- Pour chaque script : où le placer dans Roblox Studio (ServerScriptService, ReplicatedStorage…) et quels objets créer dans la map.
- Le créateur teste dans Roblox Studio et fait un retour. On ajuste.

## Étape 0 — Conception ✅
Toute la documentation de ce dossier `docs/`.

## Étape 1 — Les fondations
- Cycle jour/nuit (10 min / 15 min, 5 jours) et système de phases.
- Générateurs : emplacements prédéfinis, placement aléatoire, réparation, panne.
- Mort, corps, spectateurs, chat des morts.
- Intégration avec la caméra, la lampe et l'endurance déjà existantes (lecture de l'état de la lampe).

## Étape 2 — Le corps du monstre
- Modèle provisoire (silhouette).
- Déplacement avec PathfindingService : marcher, ramper, courir, grimper.
- Apparaître / disparaître (fantôme).
- Jouer des sons spatialisés.

## Étape 3 — Le Directeur V1 (à règles)
- Perception : état de chaque joueur, visibilité du monstre.
- Jauge de tension par joueur.
- Choix d'intentions selon la phase, avec scores et délais.
- Comportements : observer, bruit, apparaître, traquer, faire semblant, saboter, chasser, blesser, battre en retraite.

## Étape 4 — La vue debug
- Caméra 3e personne, vision nocturne, surimpressions (tension, intentions, chemin).

## Étape 5 — Les scénarios
- Enlèvement, piège du corps, leurres d'imitation.
- Mimic : apparence, chat préécrit, détection de la méfiance.

## Étape 6 — Réglages et tests
- Parties de test, réglage des chiffres (fréquences, distances, durées).
- **Enregistreur de données** : positions, frayeurs, réactions, morts, durées. Indispensable pour l'étape 7.

## Étape 7 — L'IA entraînée (V2)
- Simulation simplifiée de la map en Python.
- **IA joueur simulée** (profils : peureux, téméraire, curieux), calibrée sur les données réelles.
- Entraînement du Directeur par apprentissage par renforcement (récompense = indices de peur, pénalité si mort trop rapide ou répétition).
- Export du réseau en Luau et exécution côté serveur Roblox.
- Comparaison V1 vs V2 sur de vraies parties.

## Étape 8 — Contenu final
- Map définitive, modèle et animations du monstre original, sons définitifs, menus, paramètres (bandes noires…).
