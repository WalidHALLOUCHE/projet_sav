# Documentation Technique - SAV Tweets

## Architecture de l'Application

### Vue d'Ensemble

L'application SAV Tweets suit une architecture modulaire basée sur Streamlit avec une séparation claire des responsabilités :

```
┌─────────────────────────────────────────────┐
│           Interface Streamlit               │
│  (app.py + pages/*.py)                      │
├─────────────────────────────────────────────┤
│           Couche Logique                    │
│  (lib/data.py, lib/state.py, lib/ui.py)    │
├─────────────────────────────────────────────┤
│           Couche Données                    │
│  (CSV, Excel, Persistance)                  │
└─────────────────────────────────────────────┘
```

## Modules Principaux

### 1. lib/data.py
**Responsabilité** : Gestion des données et opérations CRUD

**Fonctions clés** :
- `load_df()` : Chargement du dataset principal
- `apply_edits()` : Application des modifications
- `persist_ticket_updates()` : Sauvegarde des changements
- `normalize_status_empty()` : Normalisation des statuts
- `filter_by_status_like_agent()` : Filtrage par statut
- `count_open_like_agent()` : Comptage des tickets ouverts

### 2. lib/state.py
**Responsabilité** : Gestion de l'état de l'application

**Fonctions clés** :
- `get_cfg()` : Récupération de la configuration
- Gestion de session_state Streamlit
- Configuration des chemins de fichiers

### 3. lib/ui.py
**Responsabilité** : Composants d'interface utilisateur

**Fonctions clés** :
- `inject_style()` : Injection CSS personnalisé
- `set_container_wide()` : Mode large
- `inject_sticky_css()` : Headers fixes
- `hide_sidebar()` : Masquage de la sidebar

### 4. lib/aggrid_utils.py
**Responsabilité** : Configuration AgGrid

**Fonctions clés** :
- Configuration des grilles de données
- Options d'édition et de sélection
- Formatage des colonnes

## Pages de l'Application

### Page d'Accueil (app.py)
- Point d'entrée
- Navigation vers les différentes interfaces
- Design moderne avec gradient

### Page Analyste (1_Analyste.py)
**Fonctionnalités** :
- Visualisation complète des données
- Filtres avancés (status, période, agent)
- Graphiques Altair interactifs
- Export de données
- AgGrid pour manipulation

**Sections** :
1. Header avec KPI principaux
2. Filtres dynamiques
3. Graphiques de tendances
4. Grille de données éditable

### Page Manager (2_Manager.py)
**Fonctionnalités** :
- Dashboard KPI
- Métriques de performance
- Analyse temporelle
- Comparaison agents

**Sections** :
1. KPI globaux (cartes)
2. Graphiques de distribution
3. Analyse par agent
4. Tendances temporelles

### Page Agent SAV (3_Agent_SAV.py)
**Fonctionnalités** :
- File de tickets
- Édition en ligne
- Changement de statut
- Recherche et filtres

**Sections** :
1. Filtres rapides
2. Grille AgGrid éditable
3. Actions en masse
4. Détails du ticket

## Flux de Données

### Chargement Initial
```
1. app.py démarre
2. lib/state.py initialise la configuration
3. lib/data.py lit last_dataset.txt
4. Chargement du CSV référencé
5. Application des éditions (sav_edits.csv)
6. Affichage dans l'interface
```

### Édition de Données
```
1. Utilisateur modifie dans AgGrid
2. Capture de l'événement grid_response
3. Détection des changements (diff)
4. Appel à persist_ticket_updates()
5. Sauvegarde dans sav_edits.csv
6. Mise à jour du session_state
7. Rerun de la page
```

### Filtrage
```
1. Utilisateur sélectionne des filtres
2. Mise à jour du session_state
3. Appel aux fonctions filter_*()
4. Recalcul des métriques
5. Mise à jour des graphiques
6. Actualisation de la grille
```

## Gestion de l'État

### Session State Streamlit
Variables principales :
- `m_filters_ver` : Version des filtres (Manager)
- `a_filters_ver` : Version des filtres (Analyste)
- `data_edits` : Éditions en mémoire
- `current_dataset` : Dataset actif

### Persistance
- `sav_edits.csv` : Modifications utilisateur
- `last_dataset.txt` : Chemin du dataset actif
- `uploads/` : Fichiers uploadés

## Patterns et Conventions

### Pattern de Filtrage
```python
# Versioning pour reset
st.session_state.setdefault("filters_ver", 1)
ver = st.session_state["filters_ver"]

# Widgets avec key versionnée
status = st.multiselect("Statut", options, key=f"status_{ver}")

# Reset
if st.button("Reset"):
    st.session_state["filters_ver"] += 1
    st.rerun()
```

### Pattern AgGrid
```python
# Configuration
gb = GridOptionsBuilder.from_dataframe(df)
gb.configure_default_column(editable=True)
gb.configure_selection("multiple")
grid_options = gb.build()

# Affichage
response = AgGrid(
    df,
    gridOptions=grid_options,
    update_mode=GridUpdateMode.VALUE_CHANGED
)

# Récupération
edited_df = response["data"]
```

### Pattern de Visualisation
```python
# Altair chart
chart = alt.Chart(df).mark_bar().encode(
    x=alt.X("column:N"),
    y=alt.Y("count():Q"),
    color=alt.Color("category:N")
).properties(
    width="container",
    height=400
)

st.altair_chart(chart, use_container_width=True)
```

## Performance

### Optimisations
1. **Cache Streamlit** : Utilisation de @st.cache_data
2. **Lazy Loading** : Chargement différé des gros datasets
3. **Filtrage Pandas** : Utilisation d'indexation efficace
4. **Altair** : Graphiques déclaratifs performants

### Bonnes Pratiques
- Éviter les loops Python sur DataFrames
- Utiliser les opérations vectorisées Pandas
- Limiter les rerun inutiles
- Optimiser les requêtes de données

## Sécurité

### Données
- Pas d'authentification (projet démo)
- Validation des entrées utilisateur
- Sanitisation des chemins de fichiers

### Uploads
- Vérification des extensions
- Limitation de taille (implicite Streamlit)
- Stockage local sécurisé

## Déploiement

### Local
```bash
streamlit run app.py
```

### Production (Streamlit Cloud)
1. Push sur GitHub
2. Connecter Streamlit Cloud
3. Configurer secrets.toml si nécessaire
4. Déployer

### Docker (optionnel)
```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["streamlit", "run", "app.py"]
```

## Tests

### Tests Manuels
- Navigation entre pages
- Édition de données
- Filtres et recherche
- Export de données

### Tests Recommandés
- Tests unitaires (lib/*)
- Tests d'intégration (pages/*)
- Tests de charge
- Tests UI (Selenium)

## Maintenance

### Logs
- Streamlit affiche les logs dans le terminal
- Utiliser `st.write()` pour debug
- Exceptions capturées avec try/except

### Backup
- Sauvegarder sav_edits.csv régulièrement
- Versionner avec Git
- Exporter les données critiques

## Troubleshooting

### Problème : AgGrid ne s'affiche pas
**Solution** : L'app utilise un fallback automatique vers st.dataframe

### Problème : Données ne se chargent pas
**Solution** : Vérifier last_dataset.txt et le chemin CSV

### Problème : Modifications non sauvegardées
**Solution** : Vérifier les permissions sur sav_edits.csv

### Problème : Performance lente
**Solution** : Réduire le volume de données ou optimiser les filtres

## Évolutions Futures

### Court Terme
- [ ] Tests unitaires
- [ ] Documentation API
- [ ] Logging structuré

### Moyen Terme
- [ ] Base de données SQL
- [ ] API REST
- [ ] Authentification

### Long Terme
- [ ] Microservices
- [ ] Real-time updates
- [ ] ML avancé
