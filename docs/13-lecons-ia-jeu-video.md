# 13 — Leçons : « Mais pourquoi l'IA est pourrie ? »

Source : vidéo du **Bazar du Grenier** (34 min, 2024) — https://www.youtube.com/watch?v=VEeukZBgNFA
Avec des interventions de développeurs (Ubisoft, Wolfeye Studios). Analyse faite sur la transcription complète.

## Résumé de la vidéo
1. L'IA de jeu vidéo, c'est surtout des **règles « si… alors »** organisées (machines à états, arbres de comportement, IA à utilité, IA à objectifs). Elle **perçoit** (rayons, zones, distances) puis **choisit un comportement**.
2. **Une IA existe pour donner du plaisir au joueur**, pas pour gagner. Les bonnes IA, « on sait les faire, mais on décide de ne pas les faire ».
3. Les IA trop fortes d'*Uncharted* et *The Last of Us* (contournements, grenades, tirs de couverture) ont été **détestées en playtest** et rendues plus faibles.
4. Trucs invisibles : les ennemis **ratent exprès un joueur qui fuit** ; zones mortes dans le dos en infiltration ; ennemis de *Batman Arkham* qui ne se retournent presque jamais.
5. **Prévisibilité** : une même action doit toujours produire le même résultat (la pièce de *Hitman*), sinon le joueur ne peut plus faire de plan.
6. ***F.E.A.R.*** paraît génial car l'IA **annonce ce qu'elle fait** par radio (« je le prends à revers »). C'est cosmétique, mais ça crée la sensation d'intelligence. *The Last of Us 2* : les voix des ennemis donnent leur position au joueur.
7. ***Metal Gear Solid 5*** s'adapte aux habitudes (casques contre les headshots, protections des générateurs). ***Alien: Isolation*** **débloque des comportements** selon le joueur (s'il se cache toujours dans les casiers, l'alien finit par les ouvrir).
8. **Donner plus de PV** aux ennemis les fait paraître plus intelligents : ils vivent assez longtemps pour **montrer** leurs comportements.
9. **Deep learning** : problème de l'œuf et de la poule. Il faut des milliers de parties de joueurs, donc sortir d'abord avec une IA classique, puis entraîner. Et « ne pas imiter le joueur, mettre en scène ».
10. **PNJ avec ChatGPT** : impressionnant mais incontrôlable (briser le 4e mur, propos non validés).
11. Chaque comportement ajouté doit être **testé dans toutes les situations** : la complexité coûte cher.
12. **Pas de vrai plaisir sans un peu de frustration**, mais jamais d'**injustice** : le joueur doit se dire « j'aurais dû faire attention », pas « c'est injuste ».

## Ce qui confirme nos choix ✅
| Leçon | Notre choix |
|---|---|
| L'IA sert le plaisir (la peur), pas la victoire | Directeur « metteur en scène », peur > mise à mort ([03](03-ia-monstre.md)) |
| Jamais d'injustice, signaux avant le danger | Règles d'équité, indices avant toute attaque |
| Alien: Isolation débloque des comportements | Phases qui débloquent les actions nuit après nuit ([04](04-phases.md)) |
| Deep learning : d'abord IA classique, données ensuite | Roadmap V1 à règles, puis V2 entraînée sur les vraies parties ([09](09-roadmap.md)) |
| LLM incontrôlables | Phrases **préécrites** pour le mimic |
| L'IA sait tout mais choisit de « rater » | Monstre omniscient qui fait semblant |

## Ce qu'on ajoute au design ➕

### 1. Des signaux constants (prévisibilité)
Le monstre peut être imprévisible dans ses **choix**, mais **ses signaux veulent toujours dire la même chose** :
- **grognement long = il va chasser** (toujours) ;
- **lumières qui grésillent = il est tout proche** (toujours) ;
- **pas lourds = il marche vers toi**, silence = il rampe ou il est loin ;
- branche qui craque, feuilles = présence, **jamais d'attaque immédiate**.

Les joueurs apprennent ce langage et peuvent faire des plans. La peur vient de **savoir ce que ça veut dire**. Les fausses alertes restent possibles (bruit de présence sans apparition), mais **jamais un signal « sûr » suivi d'une mort**.

### 2. L'IA qui « annonce » (effet F.E.A.R.)
Le monstre **laisse deviner ses intentions** par le son, ce qui le rend plus intelligent aux yeux des joueurs :
- reniflement quand il « cherche » un joueur caché ;
- grognement satisfait quand il repère quelqu'un ;
- bruit dans une direction **avant** de s'y rendre.
Coût très faible, effet énorme.

### 3. Débloquer des contre-mesures selon les habitudes (MGS5 / Alien: Isolation)
Le Directeur compte les habitudes de chaque joueur et du groupe, et **débloque une réponse** au-delà d'un seuil :

| Habitude détectée | Contre-mesure débloquée |
|---|---|
| Se cache toujours au même endroit | Le monstre fouille ou attend à cette cachette |
| Reste toujours dans la cabane | Il entre dans la cabane, coupe la lumière |
| Monte toujours sur la tour | Il grimpe la tour |
| Éteint toujours sa lampe pour se cacher | Il renifle et trouve les joueurs dans le noir |
| Le groupe ne se sépare jamais | Il coupe deux générateurs éloignés en même temps |
| Répare toujours le même générateur en premier | Il l'attend là-bas |

Le joueur doit **remarquer** que ça a changé et **s'adapter** : surprise sans injustice.

### 4. La « pitié » cachée
- Un joueur qui **fuit à bout d'endurance** se fait parfois rater de justesse (griffe qui frôle, saut qui manque) au lieu de mourir.
- Pas toujours, sinon ce serait prévisible, mais suffisamment pour créer des **survies héroïques** qu'on raconte.
- Réglable par phase : beaucoup de pitié au début, presque plus en nuit 5.

### 5. Laisser le temps de voir l'intelligence (effet « plus de PV »)
Les rencontres ne doivent pas se terminer trop vite :
- une apparition dure assez longtemps pour être **vue et comprise** ;
- une chasse laisse le temps au monstre de montrer qu'il contourne, grimpe, coupe la route ;
- sinon le joueur pense que le monstre « ne sait rien faire ».

### 6. Des « fenêtres » laissées au joueur (Batman / The Last of Us 2)
- Quand le monstre se retourne ou change de direction, il le fait **lentement**, avec un son, pour laisser au joueur le temps de réagir.
- Le joueur doit pouvoir dire « je l'ai vu venir et j'ai réussi à m'en sortir » : c'est une récompense.

### 7. Pas de difficulté « à part »
La vidéo montre que les modes de difficulté coûtent cher pour peu de joueurs. Chez nous, **c'est le Directeur qui adapte la difficulté en temps réel** (tension, pitié, fréquence), pour tout le monde.

### 8. Tester chaque comportement
Chaque nouveau comportement multiplie les situations à tester. On ajoute les comportements **un par un**, chacun testé avant le suivant, avec la vue debug ([07](07-debug.md)).

## Ce qu'on garde en tête pour la V2 (IA entraînée)
- **Ne pas apprendre à imiter un joueur humain** : on entraîne le monstre à **mettre en scène la peur** (récompense = indices de peur + équité), pas à jouer « comme un humain ».
- Les données réelles viendront de la V1 (enregistreur de données, étape 6 de la roadmap).
