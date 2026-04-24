# Power BI - Dashboard Astreintes SNCF

Dashboard Power BI pour la visualisation en temps réel des KPI et alertes de gestion des astreintes SNCF.

## 📊 Vue d'ensemble

Dashboard interactif affichant :

### **1. KPI Principaux (4 indicateurs)**
- **Coverage %** - Taux de couverture des astreintes (82.5%)
  - Tendance : ↑ +5% vs mois précédent
  - Seuil cible : 80%

- **Absence Rate %** - Taux d'absence des agents (12.3%)
  - Tendance : ↓ -2.5% vs mois précédent
  - Seuil acceptable : 10%

- **Turnover %** - Taux de rotation du personnel (5.2%)
  - Tendance : → Stable
  - Benchmark : 15%

- **Zone Coverage %** - Couverture par zone géographique (88%)
  - Tendance : → Stable
  - Objectif : 90%

---

### **2. Alertes Prioritaires (3 alertes)**

#### 🔴 HAUTE PRIORITÉ
- **Agent** : AG001 - Pierre Dupont
- **Type** : Visite médicale obligatoire
- **Deadline** : 10/05/2026 (16 jours)
- **Action** : À planifier immédiatement

#### 🟡 PRIORITÉ MOYENNE
- **Agent** : AG003 - Jean Lacroix
- **Type** : Renouvellement de contrat
- **Deadline** : 02/10/2026 (130 jours)
- **Action** : Suivi à programmer

#### 🟢 PRIORITÉ BASSE
- **Agent** : AG002 - Marie Martin
- **Type** : Certification annuelle
- **Deadline** : 25/01/2027 (265 jours)
- **Action** : À intégrer au calendrier

---

### **3. Graphiques Analytiques**

#### Coverage par Gare
```
GA001 (Gare de Lyon)      ████████░░ 85%
GA002 (Gare du Nord)      ███████░░░ 75%
GA003 (Montparnasse)      ██████████ 95%
GA004 (Saint Lazare)      ████░░░░░░ 45%
GA005 (Gare de l'Est)     ███████░░░ 78%
```

#### Tendance 3 Mois (Février - Avril 2026)
```
Coverage %:
  Février  : 75%
  Mars     : 80%
  Avril    : 82.5%
  → Progression ↑

Absence %:
  Février  : 15%
  Mars     : 14%
  Avril    : 12.3%
  → Amélioration ↓
```

#### Distribution Agents par Compétence
```
Quai           : 3 agents
Accueil        : 3 agents
Sécurité       : 2 agents
Maintenance    : 2 agents
```

---

### **4. Détail Affectations (Tableau)**

| Agent | Nom | Gare | Astreinte | Statut | Compétences |
|-------|-----|------|-----------|--------|-------------|
| AG001 | Pierre | GA001 | AST001 | ACTIF | Quai, Accueil |
| AG002 | Marie | GA002 | AST002 | ACTIF | Accueil |
| AG003 | Jean | GA001 | AST001 | ACTIF | Quai, Sécurité |
| AG004 | Sophie | GA003 | AST003 | ACTIF | Maintenance |

---

## 🔗 Connexion aux Données

### Source de données
- **Fichier** : 03_Reporting_Mensuel_Automatise.xlsm
- **Feuilles Excel** : KPICalcules, AlertesEchances, DonneesMois

### Rafraîchissement
- **Fréquence** : Temps réel (lié aux modifications Excel)
- **Mode** : DirectQuery (données directes du fichier)

---

## 📈 Fonctionnalités Interactives

### **Filtres Disponibles**
- Par Mois (février-avril 2026)
- Par Gare (GA001-GA005)
- Par Agent (AG001-AG004)
- Par Statut Alerte (HAUTE, MOYENNE, BASSE)

### **Drill-Through**
- Cliquer un KPI → Détail affectations
- Cliquer une gare → Agents affectés
- Cliquer une alerte → Historique agent

---

## 🎨 Design

- **Thème** : Corporate SNCF (bleu/blanc)
- **Layout** : 1 page unique
- **Visualisations** : KPI cards, Bar charts, Line charts, Tables
- **Responsive** : Desktop et Tablet

---

## 🔄 Intégration avec Projets Excel

```
Projet 3 (Reporting Excel)
    ↓ ExportPowerBI
Power BI Dashboard
    ↓ Visualisation
Décideurs/RH
```

---

## 📊 Données de Test Incluses

**Période** : Février - Avril 2026
- 4 agents
- 5 gares
- 3 astreintes
- 4 KPI
- 3 alertes

---

## 🚀 Utilisation

### Ouvrir le Dashboard
```
1. Ouvrir : SNCF-Astreintes-Dashboard.pbix
2. Power BI Desktop se lance
3. Sélectionner le fichier Excel source
4. Les données se chargent automatiquement
```

### Mettre à jour les données
```
1. Modifier les données dans Projet 3 (03_Reporting_Mensuel_Automatise.xlsm)
2. Sauvegarder le fichier Excel
3. Dans Power BI : Refresh (Ctrl+R)
4. Dashboard se met à jour
```

---

## 💡 Cas d'Usage en Entretien

**Démonstration suggérée** :

```
1. Montrer le Projet 1 (Opérationnel)
2. Montrer le Projet 2 (Qualité)
3. Montrer le Projet 3 (Reporting avec ExportPowerBI)
4. Ouvrir Power BI
5. "Comme vous voyez, les données Excel 
   sont automatiquement visualisées dans Power BI.
   C'est un dashboard en temps réel."
6. Filtrer les données interactivement
```

**Points à souligner** :
- ✅ Intégration Excel → Power BI
- ✅ Dashboard temps réel
- ✅ Filtres interactifs
- ✅ Design professionnel
- ✅ Outil décisionnel complet

---

## 📝 Notes Techniques

- **Outil** : Power BI Desktop
- **Format** : .pbix (Power BI Project)
- **Connexion** : Excel File (Live Connection)
- **Modèle de données** : 4 tables principales (Agents, Gares, KPI, Alertes)

---

**Créé le 24/04/2026**

Projet candidature SNCF - Portfolio professionnel
