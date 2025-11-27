# 📊 SAV Tweets - Plateforme d'Analyse et Gestion du Support Client

## 🎯 Description du Projet

**SAV Tweets** est une solution complète de gestion et d'analyse du service après-vente propulsée par l'IA. Elle permet d'analyser les sentiments des clients sur les réseaux sociaux, de piloter les KPI du support en temps réel et d'accélérer le traitement des demandes clients via une interface Streamlit moderne et intuitive.

### Solution Professionnelle SAV

Cette plateforme offre une solution complète pour les équipes de support client :
- **Analyse en temps réel** des messages clients sur les réseaux sociaux
- **Détection automatique** des sentiments et de l'urgence
- **Tableaux de bord interactifs** pour les managers et analystes
- **Interface de gestion** optimisée pour les agents SAV
- **Visualisations avancées** pour le pilotage de la performance

---

## 🚀 Fonctionnalités Principales

### 1. **Interface Analyste** 📈
- Visualisation complète des données de support client
- Analyse des sentiments (positifs, négatifs, neutres)
- Filtres avancés par statut, période, thème, agent
- Graphiques interactifs des tendances temporelles
- Réseau thématique avec analyse approfondie
- Export et manipulation de données en temps réel

### 2. **Tableau de bord Manager** 📊
- Vue d'ensemble des KPI du service client
- Suivi des performances par agent et par équipe
- Analyse temporelle avec filtres par année
- Statistiques en temps réel (% urgent, % négatif)
- Métriques de satisfaction et d'urgence
- Identification des heures et thèmes critiques

### 3. **File Agent SAV** 🎧
- Interface de traitement optimisée des tickets
- Gestion du statut des demandes (Ouvert, En cours, Résolu, Fermé)
- Priorisation automatique des tickets urgents (urgence ≥ 2 + sentiment négatif)
- Suggestions de réponse générées par IA
- Historique complet des interventions
- Édition et mise à jour en temps réel via AgGrid

### 4. **Upload de Données** 📤
- Import de fichiers CSV depuis la page d'accueil
- Intégration avec les outputs du traitement LLM (`C:\Users\hallo\OneDrive\Bureau\IA Free Mobile\LLM-Tweet-Pipeline`)
- Suivi automatique du dernier dataset chargé
- Support des formats variés de colonnes

---

## 📦 Installation

### Prérequis
- Python 3.8 ou supérieur
- pip (gestionnaire de paquets Python)

### Étapes d'installation

1. **Cloner le dépôt**
```bash
git clone <url-du-repo>
cd sav_app
```

2. **Créer un environnement virtuel** (recommandé)
```bash
python -m venv venv
# Sur Windows
venv\Scripts\activate
# Sur macOS/Linux
source venv/bin/activate
```

3. **Installer les dépendances**
```bash
pip install -r requirements.txt
```

---

## 🎮 Utilisation

### Lancement de l'application

**Option 1 : Raccourci Bureau (Recommandé)**
```
Double-cliquez sur le raccourci "lancer_sav_app.bat" sur votre Bureau
```
L'application se lancera automatiquement et s'ouvrira dans votre navigateur par défaut.

**Option 2 : Ligne de commande**
```bash
streamlit run app.py
```

**Option 3 : Script PowerShell**
```powershell
.\lancer_sav_app.ps1
```

L'application sera accessible à l'adresse : `http://localhost:8501`

### Création d'un raccourci Bureau

1. Localisez le fichier `lancer_sav_app.bat` dans le dossier du projet
2. Clic droit > Copier
3. Collez-le sur votre Bureau
4. Pour personnaliser l'icône :
   - Clic droit sur le raccourci > Propriétés
   - Onglet "Raccourci" > Bouton "Changer d'icône..."
   - Parcourir vers `logo_sav.ico` dans le dossier du projet
   - Appliquer > OK

### Navigation

1. **Page d'accueil** : Point d'entrée de l'application
2. **Analyste** : Accès à l'analyse détaillée des données
3. **Manager** : Tableau de bord des indicateurs de performance
4. **Agent SAV** : Interface de gestion des tickets

---

## 📁 Structure du Projet

```
sav_app/
├── app.py                      # Point d'entrée principal
├── lancer_sav_app.bat         # Script de lancement Windows (raccourci)
├── lancer_sav_app.ps1         # Script PowerShell alternatif
├── logo_sav.png               # Logo de l'application (PNG)
├── logo_sav.ico               # Icône pour raccourci Windows
├── pages/                      # Pages Streamlit
│   ├── 0_Accueil.py           # Page d'accueil
│   ├── 1_Analyste.py          # Interface analyste
│   ├── 2_Manager.py           # Tableau de bord manager
│   └── 3_Agent_SAV.py         # Interface agent SAV
├── lib/                        # Modules utilitaires
│   ├── __init__.py
│   ├── data.py                # Gestion des données
│   ├── state.py               # Gestion de l'état
│   ├── ui.py                  # Composants UI
│   └── aggrid_utils.py        # Utilitaires AgGrid
├── data/                       # Données de l'application
│   ├── sav_edits.csv          # Éditions persistées
│   └── last_dataset.txt       # Dataset actif
├── uploads/                    # Fichiers uploadés
├── requirements.txt            # Dépendances Python
├── .gitignore                 # Fichiers ignorés par Git
└── README.md                  # Ce fichier
```

---

## 🛠️ Technologies Utilisées

### Backend & Framework
- **Python 3.x** : Langage principal
- **Streamlit** : Framework web pour interfaces interactives
- **Pandas** : Manipulation et analyse de données
- **NumPy** : Calculs numériques

### Visualisation
- **Altair** : Graphiques interactifs déclaratifs
- **AgGrid** : Grilles de données avancées
- **Matplotlib/Plotly** : Visualisations complémentaires

### Traitement de Données
- **CSV/Excel** : Formats de données supportés
- **JSON** : Configuration et échanges de données

---

## 📊 Fonctionnalités Détaillées

### Analyse de Sentiments
- Classification automatique des messages clients
- Détection des émotions (positif, négatif, neutre)
- Visualisation de la répartition des sentiments
- Tendances temporelles

### Gestion des Tickets
- Statuts multiples : Ouvert, En cours, Résolu, Fermé
- Assignation automatique et manuelle aux agents
- Priorisation automatique basée sur l'urgence et le sentiment
- Filtres intelligents (tickets urgents négatifs)
- Historique complet avec traçabilité

### KPI et Métriques
- Pourcentage de tickets urgents (urgence ≥ 2)
- Taux de sentiment négatif en temps réel
- Urgence moyenne par thème et par période
- Performance par agent et par équipe
- Volume de tickets par période (jour, heure, année)
- Analyse des heures critiques

---

## 🔧 Configuration

### Variables d'Environnement
L'application utilise un système de configuration via `lib/state.py` pour gérer :
- Chemins des fichiers de données
- Paramètres d'affichage
- Options de filtrage

### Personnalisation
Vous pouvez personnaliser l'apparence et le comportement via :
- `lib/ui.py` : Styles CSS et composants UI
- `lib/state.py` : Configuration globale

---

## 📝 Données

### Format des Données
L'application supporte les formats suivants :
- **CSV** : Format principal
- **Excel** : Format alternatif

### Colonnes Attendues
- `tweet_id` : Identifiant unique du tweet
- `created_at_dt` : Date de création
- `text_display` : Contenu du message client
- `sentiment_label` : Sentiment détecté (positif, neutre, negatif)
- `primary_label` : Thème principal du ticket
- `llm_urgency_0_3` : Score d'urgence (0-3)
- `llm_severity_0_3` : Score de sévérité (0-3)
- `author` : Auteur du tweet
- `status` : Statut actuel (Ouvert, En cours, Résolu, Fermé)
- `assigned_to` : Agent assigné
- `routing_team` : Équipe de routage

---

## 🤝 Contribution

### Workflow Git
```bash
# Créer une branche pour vos modifications
git checkout -b feature/ma-nouvelle-fonctionnalite

# Faire vos modifications et commits
git add .
git commit -m "Description de vos modifications"

# Pousser vers le dépôt
git push origin feature/ma-nouvelle-fonctionnalite
```

### Bonnes Pratiques
- Faire des commits atomiques et descriptifs
- Tester avant de pousser
- Documenter les nouvelles fonctionnalités
- Respecter la structure du projet

---

## 🐛 Résolution de Problèmes

### AgGrid ne s'affiche pas
Si `st_aggrid` n'est pas disponible, l'application bascule automatiquement sur `st.dataframe`.

### Erreurs de chargement de données
- Vérifier le chemin dans `data/last_dataset.txt`
- S'assurer que les fichiers CSV sont bien formatés
- Consulter les logs dans le terminal

### Performance
- Pour de gros volumes, utiliser les filtres
- Limiter la période d'analyse
- Optimiser les requêtes de données

---

## 📄 Licence

Ce projet est développé dans un cadre éducatif/académique.

---

## 👥 Auteurs

Projet développé dans le cadre d'une soutenance académique.

---

## 📞 Support

Pour toute question ou problème :
1. Consulter la documentation
2. Vérifier les issues existantes
3. Créer une nouvelle issue si nécessaire

---

## 🎓 Utilisation en Entreprise

### Cas d'Usage
- **Opérateurs télécom** : Gestion du SAV clients sur les réseaux sociaux
- **E-commerce** : Traitement des réclamations et demandes
- **Services B2B** : Support client multicanal
- **Grandes entreprises** : Centralisation du service après-vente

### Avantages Business
✅ Réduction du temps de traitement des tickets  
✅ Priorisation automatique des urgences  
✅ Visibilité en temps réel sur la satisfaction client  
✅ Amélioration de la productivité des agents  
✅ Pilotage data-driven du service client  
✅ Détection précoce des crises  

---

## 🔄 Historique des Versions

### Version Actuelle (v1.0)
- Interface multi-rôles (Analyste, Manager, Agent)
- Analyse de sentiments avec IA
- Tableau de bord interactif avec filtres par année
- Gestion complète des tickets avec statuts
- Upload de fichiers CSV
- Calcul automatique des KPIs (urgence, sentiment négatif)
- Réseau thématique avec analyses approfondies
- Export des données filtrées

---

## 🚀 Améliorations Futures

- [ ] Authentification multi-utilisateurs avec rôles
- [ ] API REST pour intégrations externes (CRM, Zendesk)
- [ ] Notifications push en temps réel pour tickets urgents
- [ ] Export PDF/PowerPoint des rapports
- [ ] Dashboard mobile responsive
- [ ] Intégration avec bases de données SQL/PostgreSQL
- [ ] Système de chatbot pour réponses automatiques
- [ ] Machine Learning pour prédiction de satisfaction
- [ ] Analyse multilingue des sentiments

---

## 🐦 Intégration Twitter (En Attente)

L'application est **prête pour l'intégration Twitter** qui permettra de répondre directement aux tweets des clients depuis l'interface Agent SAV.

**⚠️ Cette fonctionnalité nécessite :**
- Un accès au compte Twitter Developer de Free
- Les clés API Twitter (API Key, API Secret, Access Token, etc.)
- Un accès Elevated ou Premium à l'API Twitter

**📖 Documentation complète disponible :** [`INTEGRATION_TWITTER.md`](INTEGRATION_TWITTER.md)

Une fois que Free fournira l'accès à son compte Twitter, suivez les étapes du guide d'intégration pour finaliser cette fonctionnalité. L'implémentation est prête et documentée, il ne reste plus qu'à configurer les identifiants API.

**Fonctionnalités prévues :**
- ✅ Publication automatique de réponses depuis l'interface Agent
- ✅ Mode Test pour sécuriser les publications
- ✅ Monitoring des limites API
- ✅ Logging complet de toutes les interactions
- ✅ Gestion d'erreurs robuste

---

**© 2025 SAV Tweets — Solution Professionnelle de Gestion du Support Client**
