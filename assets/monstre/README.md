# Modèles 3D du monstre (Meshy AI)

Deux versions à comparer en jeu.

| | `monstre-A-rigge-anime.glb` | `monstre-B-remesh-texture.glb` |
|---|---|---|
| Taille du fichier | 25 Mo | 24 Mo |
| Triangles | 10 300 ✅ (limite Roblox ~20 000) | 10 300 ✅ |
| Hauteur | **2,5 m** | 1,9 m (à mettre à l'échelle) |
| Squelette | ✅ Rigify « basic human », 24 os | ❌ aucun |
| Animations | `Walking`, `Running` | aucune |
| Textures | couleur + métal/rugosité, **4096×4096** | couleur + métal/rugosité, **4096×4096** |

## À savoir pour l'import dans Roblox
- **Import** : Roblox Studio accepte le `.glb` via l'**importateur 3D** (Avatar / 3D Importer).
- **Textures trop grandes** : Roblox les réduit à **1024×1024**. Les redimensionner soi-même avant l'upload pour garder le contrôle de la qualité (voir [docs/11-map.md](../../docs/11-map.md)).
- **Métal/rugosité combinés** : le glTF met la **rugosité dans le canal vert** et le **métal dans le canal bleu** d'une seule image. Roblox (`SurfaceAppearance`) veut **deux images séparées** (`RoughnessMap`, `MetalnessMap`) : il faut extraire ces canaux.
- **Pas de carte normale** dans ces exports : les détails de muscles sont seulement peints dans la couleur. Une `NormalMap` (générée dans Meshy ou à partir de la couleur) rendrait la chair bien plus réaliste sous la lampe torche.
- **Version B** : sans squelette, elle ne peut pas être animée telle quelle. Il faudra la rigger (Meshy « Animer » ou Blender) si c'est celle qui est retenue.
- **Animations manquantes** pour l'IA : ramper, grimper, se baisser sous une porte, attraper/porter, frapper, dévorer (voir [docs/12-monstre.md](../../docs/12-monstre.md)).
