# 🐦 Guide d'Intégration Twitter pour SAV Tweets

## 📋 Vue d'ensemble

Ce guide décrit les étapes nécessaires pour connecter l'application SAV Tweets au compte Twitter officiel de Free, permettant ainsi de répondre automatiquement aux tweets des clients directement depuis l'interface Agent SAV.

---

## ⚠️ Prérequis

Avant de commencer, Free doit fournir :

- ✅ Accès au **compte Twitter Developer** de Free
- ✅ Les **clés API Twitter** (API Key, API Secret, Access Token, etc.)
- ✅ Un accès **Elevated** ou **Premium** à l'API Twitter (requis pour publier des tweets)
- ✅ Autorisation officielle pour utiliser le compte @Free via l'application

---

## 🚀 Étapes d'Intégration

### Étape 1 : Obtenir les Identifiants Twitter API

1. **Accéder au portail développeur Twitter**
   - Se connecter sur https://developer.twitter.com avec le compte Free
   - Aller dans "Projects & Apps"
   - Créer une nouvelle App ou utiliser une existante

2. **Récupérer les clés suivantes :**
   ```
   - API Key (Consumer Key)
   - API Secret (Consumer Secret)
   - Access Token
   - Access Token Secret
   - Bearer Token
   ```

3. **Configurer les permissions de l'App**
   - Aller dans "App Settings" > "User authentication settings"
   - Activer "OAuth 1.0a"
   - Permissions : **Read and Write** (pour lire et publier)
   - Callback URL : `http://localhost:8501` (pour tests locaux)

---

### Étape 2 : Installer les Dépendances Python

1. **Ajouter à `requirements.txt` :**
   ```txt
   tweepy>=4.14.0
   python-dotenv>=1.0.0
   ```

2. **Installer les packages :**
   ```bash
   pip install tweepy python-dotenv
   ```

---

### Étape 3 : Créer le Fichier de Configuration

1. **Créer un fichier `.env` à la racine du projet :**
   ```bash
   TWITTER_API_KEY=votre_api_key_ici
   TWITTER_API_SECRET=votre_api_secret_ici
   TWITTER_ACCESS_TOKEN=votre_access_token_ici
   TWITTER_ACCESS_TOKEN_SECRET=votre_access_token_secret_ici
   TWITTER_BEARER_TOKEN=votre_bearer_token_ici
   ```

2. **⚠️ IMPORTANT : Ajouter `.env` au `.gitignore` :**
   ```gitignore
   # Secrets Twitter
   .env
   config/twitter_config.py
   ```

---

### Étape 4 : Créer le Module de Configuration

**Créer `config/twitter_config.py` :**

```python
import os
from dotenv import load_dotenv

# Charger les variables d'environnement
load_dotenv()

# Clés API Twitter (à ne JAMAIS commiter dans Git)
TWITTER_API_KEY = os.getenv("TWITTER_API_KEY")
TWITTER_API_SECRET = os.getenv("TWITTER_API_SECRET")
TWITTER_ACCESS_TOKEN = os.getenv("TWITTER_ACCESS_TOKEN")
TWITTER_ACCESS_TOKEN_SECRET = os.getenv("TWITTER_ACCESS_TOKEN_SECRET")
TWITTER_BEARER_TOKEN = os.getenv("TWITTER_BEARER_TOKEN")

# Vérification que toutes les clés sont présentes
def check_twitter_credentials():
    """Vérifie que toutes les clés Twitter sont configurées"""
    required_keys = [
        TWITTER_API_KEY,
        TWITTER_API_SECRET,
        TWITTER_ACCESS_TOKEN,
        TWITTER_ACCESS_TOKEN_SECRET,
        TWITTER_BEARER_TOKEN
    ]
    return all(required_keys)
```

---

### Étape 5 : Créer le Gestionnaire Twitter

**Créer `lib/twitter_api.py` :**

```python
import tweepy
import streamlit as st
from datetime import datetime
import logging
from config.twitter_config import *

# Configuration du logging
logging.basicConfig(
    filename='twitter_logs/activity.log',
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

class TwitterManager:
    """Gestionnaire des interactions avec l'API Twitter"""
    
    def __init__(self, test_mode=True):
        """
        Initialise la connexion à l'API Twitter
        
        Args:
            test_mode (bool): Si True, simule les envois sans publier réellement
        """
        self.test_mode = test_mode
        self.connected = False
        
        try:
            # Authentification OAuth 1.0a (pour publier)
            auth = tweepy.OAuthHandler(TWITTER_API_KEY, TWITTER_API_SECRET)
            auth.set_access_token(TWITTER_ACCESS_TOKEN, TWITTER_ACCESS_TOKEN_SECRET)
            
            # Client API v2
            self.client = tweepy.Client(
                bearer_token=TWITTER_BEARER_TOKEN,
                consumer_key=TWITTER_API_KEY,
                consumer_secret=TWITTER_API_SECRET,
                access_token=TWITTER_ACCESS_TOKEN,
                access_token_secret=TWITTER_ACCESS_TOKEN_SECRET
            )
            
            # API v1.1 (fallback)
            self.api = tweepy.API(auth)
            
            self.connected = True
            logging.info("✅ Connexion Twitter établie")
            
        except Exception as e:
            logging.error(f"❌ Erreur de connexion Twitter : {str(e)}")
            st.error(f"❌ Erreur de connexion Twitter : {str(e)}")
            self.connected = False
    
    def reply_to_tweet(self, tweet_id: str, response_text: str, author: str = None) -> dict:
        """
        Répond à un tweet spécifique
        
        Args:
            tweet_id: ID du tweet à répondre
            response_text: Texte de la réponse
            author: Nom d'utilisateur de l'auteur (optionnel, ajouté automatiquement)
            
        Returns:
            dict: {'success': bool, 'response_id': str, 'message': str}
        """
        if not self.connected:
            return {
                'success': False,
                'response_id': None,
                'message': "❌ Pas de connexion Twitter"
            }
        
        # Ajouter le @ de l'auteur si nécessaire
        if author and not response_text.startswith(f"@{author}"):
            final_text = f"@{author} {response_text}"
        else:
            final_text = response_text
        
        # Limiter à 280 caractères
        if len(final_text) > 280:
            final_text = final_text[:277] + "..."
        
        # Mode test : simulation
        if self.test_mode:
            log_msg = f"🧪 MODE TEST - Réponse simulée au tweet {tweet_id}"
            logging.info(log_msg)
            logging.info(f"📝 Texte : {final_text}")
            return {
                'success': True,
                'response_id': f"test_{tweet_id}_{datetime.now().timestamp()}",
                'message': f"🧪 Simulation réussie : {final_text[:50]}..."
            }
        
        # Mode production : publication réelle
        try:
            response = self.client.create_tweet(
                text=final_text,
                in_reply_to_tweet_id=tweet_id
            )
            
            response_id = response.data['id']
            log_msg = f"✅ Réponse envoyée - Tweet ID: {tweet_id} → Response ID: {response_id}"
            logging.info(log_msg)
            
            return {
                'success': True,
                'response_id': response_id,
                'message': f"✅ Réponse publiée avec succès ! ID: {response_id}"
            }
            
        except tweepy.errors.Forbidden as e:
            error_msg = f"❌ Accès refusé : {str(e)}"
            logging.error(error_msg)
            return {'success': False, 'response_id': None, 'message': error_msg}
            
        except tweepy.errors.TooManyRequests:
            error_msg = "❌ Limite de requêtes atteinte. Réessayez plus tard."
            logging.warning(error_msg)
            return {'success': False, 'response_id': None, 'message': error_msg}
            
        except Exception as e:
            error_msg = f"❌ Erreur lors de l'envoi : {str(e)}"
            logging.error(error_msg)
            return {'success': False, 'response_id': None, 'message': error_msg}
    
    def get_tweet_details(self, tweet_id: str):
        """Récupère les détails d'un tweet"""
        try:
            tweet = self.client.get_tweet(
                tweet_id,
                tweet_fields=['author_id', 'created_at', 'public_metrics', 'conversation_id']
            )
            return tweet.data
        except Exception as e:
            logging.error(f"❌ Erreur récupération tweet {tweet_id}: {str(e)}")
            return None
    
    def check_rate_limits(self):
        """Vérifie les limites de l'API"""
        try:
            limits = self.api.rate_limit_status()
            tweet_limits = limits['resources']['statuses']['/statuses/update']
            return {
                'remaining': tweet_limits['remaining'],
                'limit': tweet_limits['limit'],
                'reset': datetime.fromtimestamp(tweet_limits['reset'])
            }
        except Exception as e:
            logging.error(f"❌ Erreur vérification limites : {str(e)}")
            return None
```

---

### Étape 6 : Intégrer dans la Page Agent SAV

**Modifier `pages/3_Agent_SAV.py` :**

Ajouter au début du fichier :
```python
from lib.twitter_api import TwitterManager
from config.twitter_config import check_twitter_credentials
```

Ajouter après les imports :
```python
# Initialiser le Twitter Manager
if 'twitter_manager' not in st.session_state:
    # Mode test activé par défaut pour sécurité
    st.session_state.twitter_manager = TwitterManager(test_mode=True)

twitter_mgr = st.session_state.twitter_manager
```

Ajouter dans la sidebar :
```python
# Statut Twitter
with st.sidebar:
    st.markdown("---")
    st.subheader("🐦 Connexion Twitter")
    
    if check_twitter_credentials():
        if twitter_mgr.connected:
            st.success("✅ Connecté au compte @Free")
            
            # Mode test/production
            test_mode = st.checkbox(
                "🧪 Mode Test", 
                value=st.session_state.twitter_manager.test_mode,
                help="Activé : simule les publications. Désactivé : publie réellement"
            )
            
            if test_mode != st.session_state.twitter_manager.test_mode:
                st.session_state.twitter_manager = TwitterManager(test_mode=test_mode)
                st.rerun()
            
            # Vérifier les limites
            if st.button("📊 Limites API"):
                limits = twitter_mgr.check_rate_limits()
                if limits:
                    st.info(f"Tweets restants : {limits['remaining']}/{limits['limit']}")
                    st.caption(f"Reset : {limits['reset'].strftime('%H:%M:%S')}")
        else:
            st.error("❌ Échec connexion Twitter")
    else:
        st.warning("⚠️ Clés Twitter non configurées")
        st.caption("Configurez le fichier .env")
```

Ajouter dans la section de validation des réponses :
```python
# Bouton pour publier la réponse
if st.button("✅ Accepter et publier", key=f"publish_{row_id}"):
    tweet_id = selected_row["tweet_id"]
    llm_response = selected_row.get("llm_reply_suggestion", "")
    author = selected_row.get("author", "")
    
    if not llm_response:
        st.error("❌ Aucune réponse LLM disponible")
    else:
        # Publier sur Twitter
        with st.spinner("📤 Publication en cours..."):
            result = twitter_mgr.reply_to_tweet(tweet_id, llm_response, author)
            
            if result['success']:
                st.success(result['message'])
                
                # Mettre à jour le statut
                # (code existant de mise à jour du statut)
                
                st.rerun()
            else:
                st.error(result['message'])
```

---

### Étape 7 : Créer le Dossier de Logs

```bash
mkdir twitter_logs
```

Ajouter au `.gitignore` :
```gitignore
# Logs Twitter
twitter_logs/
*.log
```

---

### Étape 8 : Tests de Validation

**Tests en Mode Test :**

1. Lancer l'application : `streamlit run app.py`
2. Aller sur la page "Agent SAV"
3. Vérifier que "🧪 Mode Test" est activé
4. Sélectionner un ticket
5. Cliquer sur "Accepter et publier"
6. Vérifier que le message de simulation s'affiche

**Tests en Mode Production (quand autorisé) :**

1. Désactiver "🧪 Mode Test"
2. ⚠️ **ATTENTION** : Les tweets seront publiés réellement
3. Tester avec un compte Twitter de test d'abord
4. Vérifier les logs dans `twitter_logs/activity.log`

---

## 🔒 Sécurité et Bonnes Pratiques

### ✅ À FAIRE :
- Toujours commencer en mode test
- Ne jamais commiter les fichiers `.env` ou `config/twitter_config.py`
- Consulter les logs régulièrement
- Mettre en place une validation à deux niveaux (Agent + Manager)
- Limiter l'accès aux clés API (uniquement personnel autorisé)

### ❌ À NE PAS FAIRE :
- Ne jamais partager les clés API
- Ne jamais commiter les secrets dans Git
- Ne jamais désactiver le mode test sans validation
- Ne jamais publier depuis un compte personnel

---

## 📊 Monitoring et Limites

### Limites de l'API Twitter (par 24h) :
- **Tweets** : 300 par 3 heures (compte standard)
- **Réponses** : Incluses dans la limite des tweets
- **Lectures** : Variable selon le niveau d'accès

### Recommandations :
- Vérifier les limites API régulièrement
- Espacer les publications si volume important
- Prévoir un système de file d'attente si nécessaire

---

## 🐛 Résolution de Problèmes

### Erreur "Forbidden" :
- Vérifier que l'app a les permissions "Read and Write"
- Vérifier que les tokens sont valides
- S'assurer que le compte Twitter est vérifié

### Erreur "Too Many Requests" :
- Attendre la réinitialisation des limites
- Consulter les logs pour voir le timestamp de reset

### Connexion échoue :
- Vérifier que toutes les clés sont dans `.env`
- Vérifier qu'il n'y a pas d'espaces dans les valeurs
- Tester les clés sur le portail développeur Twitter

---

## 📝 Changelog

- **Version 1.0** (22/11/2025) : Documentation initiale de l'intégration Twitter

---

## 📞 Support

Pour toute question concernant cette intégration :
1. Consulter la documentation Twitter : https://developer.twitter.com/en/docs
2. Vérifier les logs dans `twitter_logs/activity.log`
3. Contacter l'équipe technique de Free

---

**© 2025 SAV Tweets — Intégration Twitter pour Free**
