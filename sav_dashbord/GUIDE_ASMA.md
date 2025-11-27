# 🎯 Guide de Travail - ASMA

## 📋 Responsabilités

Tu es responsable de :
- **Page Analyste** (`pages/1_Analyste.py`)
- **Page d'accueil** (`pages/0_Accueil.py`)
- **Landing page** (`app.py`)

## 📁 Fichiers à pusher sur GitHub

### Fichiers obligatoires pour l'app
```
sav_app/
├── app.py                      # Landing page (TON TRAVAIL)
├── requirements.txt            # Dépendances Python
├── .gitignore                  # Fichiers à ignorer
├── pages/
│   ├── 0_Accueil.py           # Menu principal (TON TRAVAIL)
│   ├── 1_Analyste.py          # Écran Analyste (TON TRAVAIL)
│   ├── 2_Manager.py           # Écran Manager (Walid)
│   └── 3_Agent_SAV.py         # Écran Agent (Imad)
├── lib/
│   ├── __init__.py            # Init bibliothèque
│   ├── data.py                # Chargement données
│   ├── state.py               # État session
│   ├── ui.py                  # Helpers UI
│   └── aggrid_utils.py        # Utils AgGrid
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

1. ✓ Teste que ton écran Analyste fonctionne
2. ✓ Vérifie que la page d'accueil affiche correctement
3. ✓ Assure-toi que le CSS est harmonisé (fond blanc/bleu clair)
4. ✓ Vérifie qu'il n'y a pas d'erreurs Altair
5. ✓ Commit avec un message clair : `"Feat: Écran Analyste et pages d'accueil"`

## 🔧 Commandes Git

```bash
cd "c:\Users\hallo\OneDrive\Bureau\IA Free Mobile\sav_app"

# Ajouter tes fichiers
git add app.py pages/0_Accueil.py pages/1_Analyste.py

# Commit
git commit -m "Feat: Pages Analyste, Accueil et Landing par Asma"

# Push
git push origin main
```

## 📝 Notes importantes

- **Layout** : Ton écran Analyste utilise `layout="wide"` + `set_container_wide()` pour être centré
- **CSS** : Le style doit être identique à Manager/Agent (fond dégradé bleu clair)
- **Altair** : Tous les graphiques doivent avoir des vérifications pour éviter les erreurs avec données vides
- **Navigation** : Le bouton "Retour à l'accueil" redirige vers `pages/0_Accueil.py`

## 🤝 Coordination

- Coordonne-toi avec **Walid** pour les styles CSS communs
- Coordonne-toi avec **Imad** pour les helpers de `lib/`
- Assurez-vous que tous les écrans ont le même look & feel

Bon courage ! 💪
