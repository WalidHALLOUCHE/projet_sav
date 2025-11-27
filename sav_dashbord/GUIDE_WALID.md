# 🎯 Guide de Travail - WALID

## 📋 Responsabilités

Tu es responsable de :
- **Page Manager** (`pages/2_Manager.py`)
- **Bibliothèques partagées** (`lib/*.py`)
- **Configuration et helpers UI**

## 📁 Fichiers à pusher sur GitHub

### Fichiers obligatoires pour l'app
```
sav_app/
├── app.py                      # Landing page (Asma)
├── requirements.txt            # Dépendances Python
├── .gitignore                  # Fichiers à ignorer
├── pages/
│   ├── 0_Accueil.py           # Menu principal (Asma)
│   ├── 1_Analyste.py          # Écran Analyste (Asma)
│   ├── 2_Manager.py           # Écran Manager (TON TRAVAIL)
│   └── 3_Agent_SAV.py         # Écran Agent (Imad)
├── lib/
│   ├── __init__.py            # Init bibliothèque (TON TRAVAIL)
│   ├── data.py                # Chargement données (TON TRAVAIL)
│   ├── state.py               # État session (TON TRAVAIL)
│   ├── ui.py                  # Helpers UI (TON TRAVAIL)
│   └── aggrid_utils.py        # Utils AgGrid (TON TRAVAIL)
└── data/
    ├── sav_edits.csv          # Éditions persistées
    └── last_dataset.txt       # Dernier dataset chargé
```

## 🚫 Fichiers à NE PAS pusher

- `data/uploads/*` (fichiers uploadés temporaires)
- `old/*` (archives)
- `__pycache__/`, `*.pyc`
- `.env`, fichiers de config locaux

## ✅ Checklist avant de pusher

1. ✓ Teste que ton écran Manager fonctionne
2. ✓ Vérifie que les filtres et KPI s'affichent correctement
3. ✓ Assure-toi que l'export CSV/JSON fonctionne (correction colonnes dupliquées)
4. ✓ Vérifie que tous les helpers de `lib/` sont fonctionnels
5. ✓ Commit avec un message clair : `"Feat: Écran Manager et bibliothèques partagées"`

## 🔧 Commandes Git

```bash
cd "c:\Users\hallo\OneDrive\Bureau\IA Free Mobile\sav_app"

# Ajouter tes fichiers
git add pages/2_Manager.py lib/*.py

# Commit
git commit -m "Feat: Page Manager et bibliothèques (lib/) par Walid"

# Push
git push origin main
```

## 📝 Notes importantes

- **CSS** : Le Manager a le CSS le plus complet (fond dégradé bleu, glassmorphism)
- **Thème Altair** : Fonction `_altair_light_theme()` à partager avec les autres écrans
- **Helper `show_white_table`** : Utilisé pour afficher les tableaux blancs stylisés
- **Exports** : Correction ajoutée pour dédupliquer les colonnes avant export JSON
- **Bibliothèques `lib/`** :
  - `data.py` : Fonctions de chargement et persistence (load_df, apply_edits, upsert_edits)
  - `state.py` : Gestion de l'état session (get_cfg)
  - `ui.py` : Helpers CSS (inject_style, set_container_wide, hide_sidebar)
  - `aggrid_utils.py` : Configuration AgGrid

## 🤝 Coordination

- Coordonne-toi avec **Asma** pour que le CSS soit identique partout
- Coordonne-toi avec **Imad** pour que l'Agent SAV utilise les mêmes helpers
- Assure-toi que les fonctions de `lib/` sont bien documentées

Bon courage ! 💪
