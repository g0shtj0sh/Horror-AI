# AI — Le code de l'IA du monstre

Ce dossier contiendra tout le code de l'IA. **Rien n'est encore codé** : la conception est dans [../docs/](../docs/).

## Structure prévue

```
AI/
├── README.md
├── Director/        ← le cerveau : tension, choix des intentions, phases (Luau, serveur)
├── Behaviors/       ← les comportements : bruit, apparaître, traquer, enlever, mimic...
├── Body/            ← le corps : déplacement, animations, sons, interactions
├── Perception/      ← lecture de l'état des joueurs (position, regard, lampe, chat...)
├── Config/          ← tous les chiffres réglables (phases, délais, distances)
├── Debug/           ← la vue debug (client)
├── Data/            ← l'enregistreur de données des parties
└── Training/        ← (V2) simulation Python, IA joueur, entraînement, export Luau
```

## Documents à lire
- [Architecture de l'IA](../docs/03-ia-monstre.md)
- [Phases](../docs/04-phases.md)
- [Scénarios](../docs/05-scenarios.md)
- [Vue debug](../docs/07-debug.md)
- [Roadmap](../docs/09-roadmap.md)
