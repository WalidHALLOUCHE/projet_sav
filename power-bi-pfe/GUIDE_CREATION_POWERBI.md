# Comment créer le fichier Power BI

## Étape 1 : Prérequis
- Power BI Desktop installé (gratuit)
- Fichier Excel : 03_Reporting_Mensuel_Automatise.xlsm
- Fichier CSV : Donnees_Affectations.csv (optionnel)

## Étape 2 : Créer le Dashboard

1. Ouvrir Power BI Desktop
2. Cliquer "Obtenir les données"
3. Sélectionner "Fichier Excel"
4. Charger : 03_Reporting_Mensuel_Automatise.xlsm
5. Importer les feuilles :
   - KPICalcules
   - AlertesEchances
   - DonneesMois
   - TableauxSynthese

## Étape 3 : Créer les Visuels

### Page 1 : KPI Dashboard
- 4 cartes KPI (Coverage, Absence, Turnover, Zone Coverage)
- 2 graphiques en barres (Coverage par gare, Tendance mensuelle)
- Table des alertes

### Page 2 : Détail Affectations
- Tableau des affectations
- Filtres : Gare, Agent, Statut
- Drill-through vers détail agent

## Étape 4 : Sauvegarder
- Fichier → Enregistrer sous
- Nom : SNCF-Astreintes-Dashboard.pbix
- Localisation : Ce dossier

## Étape 5 : Publier (optionnel)
- Fichier → Publier
- Connecter compte Power BI
- Partager le lien avec recruteurs

---

Le fichier SNCF-Astreintes-Dashboard.pbix sera créé automatiquement.
