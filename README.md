# VIES TVA Validator - Batch Excel

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://your-app-url.streamlit.app)

Une application web Streamlit pour la vérification en masse de numéros de TVA européens via l'API VIES (Validation Information Exchange System) de la Commission Européenne.

## 🎯 Fonctionnalités

- **Validation en masse** : Traitement de fichiers Excel contenant plusieurs numéros TVA
- **Interface intuitive** : Interface web simple et claire avec Streamlit
- **Gestion d'erreurs robuste** : Retry automatique, gestion des timeouts, traitement par lots
- **Export multiple formats** : Téléchargement des résultats en Excel et CSV
- **Statistiques en temps réel** : Suivi de la progression et statistiques de validation
- **Configuration avancée** : Paramètres personnalisables pour les délais et tentatives

## 📋 Format du fichier Excel

### Colonnes requises
- `MS Code` : Code pays à 2 lettres (FR, DE, IT, ES, etc.)
- `VAT Number` : Numéro de TVA à valider

### Colonnes optionnelles
- `Requester MS Code` : Code pays du demandeur
- `Requester VAT Number` : Numéro TVA du demandeur

Si les colonnes optionnelles sont absentes, les valeurs par défaut configurées dans l'interface seront utilisées.

### Exemple de fichier
```
MS Code | VAT Number  | Requester MS Code | Requester VAT Number
FR      | 12345678901 | FR               | 98765432109
DE      | 123456789   |                  |
IT      | 12345678901 |                  |
```

## 🚀 Utilisation

1. **Charger un fichier Excel** avec les colonnes requises
2. **Configurer les paramètres** dans la barre latérale (optionnel)
3. **Lancer la vérification** et suivre la progression
4. **Consulter les résultats** et statistiques
5. **Télécharger** les résultats en Excel ou CSV

## ⚙️ Configuration

### Paramètres essentiels
- **Requester MS** : Code pays par défaut du demandeur (défaut: FR)
- **Requester VAT** : Numéro TVA par défaut du demandeur

### Paramètres avancés
- **Delay** : Délai entre les requêtes API (défaut: 1.5s)
- **Retries** : Nombre de tentatives en cas d'échec (défaut: 2)
- **Chunk size** : Taille des lots de traitement (défaut: 10)
- **Chunk pause** : Pause entre les lots (défaut: 3s)
- **Timeout** : Timeout des requêtes HTTP (défaut: 10s)

## 🛠️ Installation locale

### Prérequis
- Python 3.8+
- pip

### Installation
```bash
# Cloner le repository
git clone https://github.com/votre-username/smdlabtech-vat-vies-validator-batch-excel.git
cd smdlabtech-vat-vies-validator-batch-excel

# Installer les dépendances
pip install -r requirements.txt

# Lancer l'application
streamlit run app/main.py
```

L'application sera disponible sur `http://localhost:8501`

## 🌐 API VIES

Cette application utilise l'API REST VIES officielle de la Commission Européenne :
- **URL** : `https://ec.europa.eu/taxation_customs/vies/rest-api/check-vat-number`
- **Méthode** : POST
- **Format** : JSON
- **Limite de taux** : Respect nécessaire des limites (d'où les délais configurables)

### Pays supportés
Tous les pays membres de l'Union Européenne :
AT, BE, BG, CY, CZ, DE, DK, EE, ES, FI, FR, GR, HR, HU, IE, IT, LT, LU, LV, MT, NL, PL, PT, RO, SE, SI, SK

## 📊 Résultats

### Colonnes de sortie
- **MS Code** : Code pays d'origine
- **VAT Number** : Numéro TVA vérifié
- **valid** : Statut de validation (True/False)
- **name** : Nom de l'entreprise (si disponible)
- **address** : Adresse de l'entreprise (si disponible)
- **Requester MS Code** : Code pays du demandeur
- **Requester VAT Number** : Numéro TVA du demandeur
- **Attempts** : Nombre de tentatives effectuées
- **timestamp** : Horodatage de la vérification
- **error** : Message d'erreur (si applicable)

## 🔧 Structure du projet

```
smdlabtech-vat-vies-validator-batch-excel/
├── app/
│   └── main.py                    # Application Streamlit principale
├── requirements.txt               # Dépendances Python
├── .streamlit/
│   └── config.toml               # Configuration Streamlit
├── README.md                     # Documentation
├── LICENSE                       # Licence MIT
└── Test_Check_VAT.xlsx          # Fichier de test
```

## 📝 Licence

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

## ⚠️ Limitations et bonnes pratiques

### Limitations
- **Timeout Streamlit Cloud** : Sessions limitées à quelques minutes
- **Taille de fichier** : Limité par la mémoire disponible
- **Pas de stockage persistant** : Les données ne sont pas sauvegardées entre les sessions

### Bonnes pratiques
- **Fichiers volumineux** : Diviser en plusieurs fichiers plus petits
- **Erreurs 429** : Augmenter les délais entre requêtes
- **Timeouts** : Augmenter la valeur du timeout pour les connexions lentes
- **Traitement par lots** : Ajuster la taille des chunks selon les performances

## 🐛 Problèmes connus

- L'API VIES peut être temporairement indisponible
- Certains numéros TVA valides peuvent être rejetés par l'API
- Les réponses peuvent varier selon la charge du serveur VIES

## 📞 Support

Pour signaler un bug ou demander une fonctionnalité :
1. Ouvrir une issue sur GitHub
2. Fournir un fichier de test Excel
3. Inclure les paramètres utilisés et les messages d'erreur

## 🎉 Contribution

Les contributions sont les bienvenues ! Merci de :
1. Fork le projet
2. Créer une branche pour votre fonctionnalité
3. Commiter vos changements
4. Pousser vers la branche
5. Ouvrir une Pull Request