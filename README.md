# Projet de fin d'etude - IA, RAG et BI pour le SAV

Ce depot regroupe les principaux livrables de mon projet de fin d'etude autour de l'analyse et de l'automatisation du service apres-vente.

L'objectif est de montrer une chaine complete autour des donnees SAV : ingestion et preparation de tweets clients, analyse NLP/LLM, assistant conversationnel RAG, dashboard Streamlit et restitution Power BI.

## Vue d'ensemble

Le projet est organise en trois modules principaux :

| Module | Description | Technologies |
| --- | --- | --- |
| [`LLM_tweet`](LLM_tweet/) | Pipeline d'analyse de tweets SAV : nettoyage, classification, enrichissement RAG et generation de reponses | Python, Streamlit, Mistral, Ollama, RAG, Pandas |
| [`chatboot_app_sav`](chatboot_app_sav/) | Assistant conversationnel SAV base sur une architecture RAG | Streamlit, LangChain, ChromaDB, ChatGroq, Ollama |
| [`tableau de bord de sauvegarde`](tableau%20de%20bord%20de%20sauvegarde/) | Dashboard SAV pour le suivi operationnel et managerial | Streamlit, Pandas, visualisation de donnees |

Le tableau de bord Power BI associe au memoire est separe dans un depot dedie :

[`power-bi-memoire-sav`](https://github.com/WalidHALLOUCHE/power-bi-memoire-sav)

## Objectifs metier

- Identifier automatiquement les demandes clients issues de tweets SAV.
- Classifier les messages par theme, sentiment, urgence et gravite.
- Proposer des reponses contextualisees avec un assistant RAG.
- Fournir aux equipes SAV une vue de pilotage via dashboard.
- Produire des exports exploitables dans Power BI.

## Competences mises en avant

- Data analysis et preparation de donnees avec Python/Pandas.
- NLP et classification de messages clients.
- Architecture RAG avec base de connaissances vectorielle.
- Utilisation de LLM via Mistral, Ollama et ChatGroq.
- Creation d'applications Streamlit.
- Dashboarding, KPI et restitution BI.
- Securisation des secrets via fichiers d'exemple et variables d'environnement.
- Organisation de projet GitHub avec documentation.

## Structure du depot

```text
projet_sav/
|-- LLM_tweet/                      # Pipeline NLP, LLM et RAG sur tweets clients
|-- chatboot_app_sav/               # Chatbot RAG pour support client
|-- tableau de bord de sauvegarde/  # Dashboard Streamlit SAV
`-- README.md                       # Presentation globale du projet
```

## Donnees et securite

Les donnees publiees dans ce depot sont destinees a un usage de demonstration. Les secrets, cles API, caches, environnements virtuels et fichiers sensibles ne doivent pas etre versionnes.

Chaque module contient sa propre documentation avec les instructions d'installation, de configuration et d'utilisation.

## Liens utiles

- [Pipeline LLM/RAG tweets SAV](LLM_tweet/)
- [Chatbot RAG SAV](chatboot_app_sav/)
- [Dashboard SAV Streamlit](tableau%20de%20bord%20de%20sauvegarde/)
- [Dashboard Power BI du memoire](https://github.com/WalidHALLOUCHE/power-bi-memoire-sav)
