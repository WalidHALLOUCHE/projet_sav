# 📋 Guide des Commandes - SAV Tweets

## 🚀 Lancement de l'Application

### Méthode 1 : Raccourci Bureau (Recommandé)
```
Double-cliquez sur "lancer_sav_app.bat" sur votre Bureau
```

### Méthode 2 : Ligne de commande
```bash
# Depuis le dossier sav_app
streamlit run app.py
```

### Méthode 3 : PowerShell
```powershell
.\lancer_sav_app.ps1
```

---

## 🔧 Gestion de l'Environnement Virtuel

### Activer l'environnement virtuel

**PowerShell :**
```powershell
.\venv\Scripts\Activate.ps1
```

**CMD :**
```cmd
venv\Scripts\activate.bat
```

### Désactiver l'environnement virtuel
```bash
deactivate
```

### Vérifier que l'environnement est activé
```bash
# Vous devriez voir (venv) au début de votre ligne de commande
# Exemple : (venv) PS C:\Users\hallo\...\sav_app>
```

---

## 📦 Installation et Mise à Jour des Dépendances

### Installer toutes les dépendances
```bash
pip install -r requirements.txt
```

### Mettre à jour une dépendance spécifique
```bash
pip install --upgrade streamlit
pip install --upgrade pandas
```

### Voir les packages installés
```bash
pip list
```

### Voir les packages obsolètes
```bash
pip list --outdated
```

### Créer/Mettre à jour requirements.txt
```bash
pip freeze > requirements.txt
```

---

## 🐛 Dépannage et Diagnostic

### Vérifier la version de Python
```bash
python --version
```

### Vérifier la version de Streamlit
```bash
streamlit version
```

### Nettoyer le cache de Streamlit
```bash
streamlit cache clear
```

### Voir les logs en temps réel
```bash
# L'application affiche les logs dans le terminal où elle est lancée
streamlit run app.py --logger.level=debug
```

### Lancer sur un port spécifique
```bash
streamlit run app.py --server.port 8502
```

### Désactiver l'ouverture automatique du navigateur
```bash
streamlit run app.py --server.headless true
```

---

## 📂 Gestion des Fichiers

### Voir les fichiers uploadés
```bash
dir uploads\
# ou
ls uploads/
```

### Supprimer les anciens uploads
```bash
# Attention : supprime TOUS les fichiers du dossier uploads
del uploads\*
# ou
rm uploads/*
```

### Voir le dataset actuel
```bash
type data\last_dataset.txt
# ou
cat data/last_dataset.txt
```

### Sauvegarder les données
```bash
# Copier le fichier CSV actuel
copy data\sav_edits.csv data\sav_edits_backup.csv
```

---

## 🔄 Git - Gestion de Version

### Voir l'état actuel
```bash
git status
```

### Voir l'historique des commits
```bash
git log --oneline
```

### Voir les modifications non commitées
```bash
git diff
```

### Ajouter tous les changements
```bash
git add .
```

### Créer un commit
```bash
git commit -m "Description de vos modifications"
```

### Voir les branches
```bash
git branch
```

### Créer une nouvelle branche
```bash
git checkout -b nom-de-la-branche
```

### Revenir à un commit précédent (lecture seule)
```bash
git checkout <commit-hash>
```

### Revenir à la branche principale
```bash
git checkout master
```

### Annuler les modifications non commitées
```bash
# Annuler les modifications d'un fichier
git checkout -- <nom-du-fichier>

# Annuler TOUTES les modifications
git reset --hard HEAD
```

---

## 🗂️ Navigation dans les Dossiers

### Aller dans le dossier de l'application
```bash
cd "C:\Users\hallo\OneDrive\Bureau\IA Free Mobile\sav_app"
```

### Revenir au dossier parent
```bash
cd ..
```

### Lister les fichiers du dossier actuel
```bash
# PowerShell/CMD
dir

# Git Bash
ls -la
```

---

## 🔍 Recherche et Filtrage

### Rechercher un fichier
```bash
# Dans le dossier actuel et sous-dossiers
dir /s <nom-du-fichier>
```

### Compter les lignes dans un fichier CSV
```bash
# PowerShell
(Get-Content "data\sav_edits.csv").Count
```

### Voir les 10 premières lignes d'un fichier
```bash
# PowerShell
Get-Content "data\sav_edits.csv" | Select-Object -First 10
```

---

## 🧪 Tests et Validation

### Tester l'import d'un module Python
```bash
python -c "import streamlit; print(streamlit.__version__)"
python -c "import pandas; print(pandas.__version__)"
```

### Vérifier la syntaxe d'un fichier Python
```bash
python -m py_compile app.py
```

### Lancer Python en mode interactif
```bash
python
# Puis tapez vos commandes Python
# Pour quitter : exit()
```

---

## 📊 Commandes Utiles Streamlit

### Ouvrir la documentation Streamlit
```bash
streamlit docs
```

### Voir les exemples Streamlit
```bash
streamlit hello
```

### Configuration Streamlit
```bash
streamlit config show
```

### Créer un fichier de config personnalisé
```bash
# Le fichier sera créé dans .streamlit/config.toml
mkdir .streamlit
```

---

## 🔐 Sécurité et Backup

### Créer une sauvegarde complète
```bash
# PowerShell
$date = Get-Date -Format "yyyy-MM-dd_HH-mm"
Compress-Archive -Path . -DestinationPath "..\sav_app_backup_$date.zip"
```

### Exclure les fichiers sensibles avant backup
```bash
# Assurez-vous que .gitignore contient :
# .env
# venv/
# data/sav_edits.csv
# uploads/
```

---

## 📱 Accès à l'Application

### URLs d'accès
- **Local** : http://localhost:8501
- **Réseau local** : http://192.168.x.x:8501 (affichée au lancement)

### Partager l'application sur le réseau local
```bash
streamlit run app.py --server.address 0.0.0.0
```

---

## 🛑 Arrêt de l'Application

### Arrêter l'application en cours
```
Ctrl + C (dans le terminal)
```

### Ou simplement fermer la fenêtre du terminal

---

## 💡 Astuces Pratiques

### Relancer automatiquement à chaque modification
```bash
# Streamlit le fait automatiquement !
# Sauvegardez simplement vos fichiers .py
```

### Voir l'utilisation mémoire
```bash
# PowerShell
Get-Process python | Format-Table Id, ProcessName, @{Name="Memory(MB)";Expression={[int]($_.WS/1MB)}}
```

### Tuer tous les processus Streamlit
```bash
# PowerShell
Get-Process | Where-Object {$_.ProcessName -like "*streamlit*"} | Stop-Process
```

---

## 📞 Support et Logs

### Emplacement des logs
- **Logs Streamlit** : Affichés dans le terminal
- **Logs Twitter** (si activé) : `twitter_logs/activity.log`
- **Logs système** : Selon votre OS

### Créer un rapport de bug
1. Noter la commande exécutée
2. Copier le message d'erreur complet du terminal
3. Vérifier `git status` pour voir les fichiers modifiés
4. Noter la version : `streamlit version` et `python --version`

---

## 🎯 Workflow Typique

### Workflow quotidien
```bash
# 1. Aller dans le dossier
cd "C:\Users\hallo\OneDrive\Bureau\IA Free Mobile\sav_app"

# 2. Activer l'environnement (optionnel, le script le fait automatiquement)
.\venv\Scripts\Activate.ps1

# 3. Lancer l'application
streamlit run app.py

# 4. Travailler dans l'interface web
# ...

# 5. Arrêter l'application
# Ctrl + C
```

### Workflow de mise à jour
```bash
# 1. Sauvegarder les modifications
git add .
git commit -m "Description des changements"

# 2. Mettre à jour les dépendances si nécessaire
pip install --upgrade -r requirements.txt

# 3. Tester
streamlit run app.py
```

---

**© 2025 SAV Tweets — Aide-mémoire des Commandes**
