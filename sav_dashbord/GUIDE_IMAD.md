# 🎯 Guide de Travail - IMAD

## 📋 Responsabilités

Tu es responsable de :
- **Page Agent SAV** (`pages/3_Agent_SAV.py`)
- **Gestion des données** (`data/`)
- **Tests et validation finale**

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
│   ├── 2_Manager.py           # Écran Manager (Walid)
│   └── 3_Agent_SAV.py         # Écran Agent (TON TRAVAIL)
├── lib/
│   ├── __init__.py            # Init bibliothèque
│   ├── data.py                # Chargement données
│   ├── state.py               # État session
│   ├── ui.py                  # Helpers UI
│   └── aggrid_utils.py        # Utils AgGrid
└── data/
    ├── sav_edits.csv          # Éditions persistées (TON TRAVAIL)
    └── last_dataset.txt       # Dernier dataset chargé (TON TRAVAIL)
```

## 🚫 Fichiers à NE PAS pusher

- `data/uploads/*` (fichiers uploadés temporaires) ⚠️ IMPORTANT
- `old/*` (archives)
- `__pycache__/`, `*.pyc`
- `.env`, fichiers de config locaux
- Fichiers CSV volumineux de test

## ✅ Checklist avant de pusher

1. ✓ Teste que ton écran Agent SAV fonctionne
2. ✓ Vérifie que la file d'attente s'affiche correctement
3. ✓ Assure-toi que les actions (Clore, Réaffecter, etc.) fonctionnent
4. ✓ Teste que les modifications sont persistées dans `sav_edits.csv`
5. ✓ Vérifie que le style est harmonisé (fond blanc/bleu clair)
6. ✓ Commit avec un message clair : `"Feat: Écran Agent SAV et gestion données"`

## 🔧 Commandes Git

```bash
cd "c:\Users\hallo\OneDrive\Bureau\IA Free Mobile\sav_app"

# Ajouter tes fichiers
git add pages/3_Agent_SAV.py data/sav_edits.csv data/last_dataset.txt

# Commit
git commit -m "Feat: Page Agent SAV et gestion données par Imad"

# Push
git push origin main
```

## 📝 Notes importantes

- **CSS** : Utilise le même CSS que Manager/Analyste (fond dégradé bleu clair)
- **Icônes** : Les icônes SVG doivent être blanches (`color: #FFFFFF !important`)
- **Tables blanches** : Fonction `show_white_table()` à utiliser (déjà présente si tu as annulé mes edits)
- **Persistence** : Les modifications de tickets sont sauvegardées dans `data/sav_edits.csv`
- **Filtres** : Système de versioning (`filters_ver`) pour reset propre
- **Sélection sticky** : Les tickets sélectionnés restent en haut de la liste

## 🤝 Coordination

- Coordonne-toi avec **Walid** pour utiliser les fonctions de `lib/data.py`
- Coordonne-toi avec **Asma** pour que le CSS soit identique partout
- Assure-toi que l'écran Agent peut charger les données depuis `last_dataset.txt`

## ⚠️ Points d'attention

- **Ne pas pusher les fichiers volumineux** dans `data/uploads/`
- Créer un fichier `.gitignore` si absent :
```
data/uploads/*
__pycache__/
*.pyc
.env
old/*
```

Bon courage ! 💪
