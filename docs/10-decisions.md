# 10 — Décisions et questions ouvertes

## Décisions prises ✅
| Sujet | Décision |
|---|---|
| Approche IA | V1 à **règles** (Directeur), puis V2 **entraînée** sur les données réelles |
| Objectif joueurs | Réparer les générateurs et survivre **5 nuits** |
| Durées | Jour **10 min**, nuit **15 min** |
| Map | Une map fixe, pas très grande, générateurs aléatoires parmi des emplacements prédéfinis. Style **forêt** comme dans la vidéo de référence (voir [11-map.md](11-map.md)) |
| Direction artistique | **Hyper-réalisme** (textures PBR, éclairage réaliste) ; la caméra « mauvaise qualité » amplifie le réalisme (effet found footage) |
| Construction de la map | Un Claude via **Vibestarter** (connecté à Roblox Studio et au web) télécharge et uploade lui-même les ressources CC0 (Poly Haven, ambientCG), en **1024×1024 max** ; vérification manuelle par le créateur |
| Musique | **Aucune en partie**, seulement dans le lobby |
| Faune | **Aucun animal visible**, uniquement des sons (qui se taisent près du monstre) |
| Tutoriel | **Aucun** : joueurs déposés à la cabane, compteur « 0/4 » des générateurs, générateurs en panne qui fument, « E » + temps + QTE simple |
| Capacités du monstre | **Jamais montrées à l'avance**, les joueurs les découvrent |
| Silence | Outil de peur à part entière, pas de stimulus obligatoire |
| Monétisation | Gamepass **infrarouge**, **revive** pas cher, **loot boxes de cosmétiques** ; aucun traitement de faveur du monstre |
| Vue | Première personne, lampe torche, endurance, effet dashcam (système existant) |
| Bandes noires | Désactivées par défaut, activables dans les paramètres |
| Connaissance du monstre | **Omniscient** : il sait tout, mais choisit de faire semblant |
| Jour 1 | Bruits **proches** mais ambigus (branches, feuilles) |
| Dégâts | Frapper / dévorer puis lâcher, **sans malus** |
| Morts | Corps qui restent ; morts = spectateurs avec **chat réservé aux morts** |
| Enlèvement | À partir de la nuit 4, avec règles d'équité |
| Mimic | Jour/Nuit 5, **phrases préécrites**, n'attaque jamais le jour en mimic |
| Vue debug | **3e personne**, vision nocturne pour le développeur, pensées de l'IA affichées |
| Monstre | Design **original** (pas de copie de Vita Carnis ou autre) ; modèle provisoire en attendant |

## Questions ouvertes ❓
1. **Conditions de défaite** : que se passe-t-il si trop de générateurs sont en panne ? Tous les joueurs morts = défaite, d'accord, mais les générateurs ?
2. **Victoire** : suffit-il d'un survivant à la fin de la nuit 5 ?
3. **Mise à mort avant la nuit 4** : le monstre peut-il tuer en nuit 3, ou seulement blesser ?
4. **Nombre de joueurs** : minimum et maximum par partie ?
5. **Nombre de générateurs** et d'emplacements possibles.
6. **Les joueurs peuvent-ils se défendre** ? (lampe qui fait reculer le monstre au début, objets, cachettes, safe zone ?)
7. **Soins** : la vie remonte-t-elle avec le temps ?
11. **Revive** : combien de fois par partie, où réapparaît-on, autorisé en nuit 5 ?
12. **Nombre de générateurs** : le compteur « 0/4 » suggère 4 par nuit, à confirmer.
8. **La map** : plan précis et nom des zones (forêt hyper-réaliste validée).
9. **Le monstre** : apparence, nom, taille.
10. **Le chat de proximité / voix** : chat vocal Roblox activé ou non ?
