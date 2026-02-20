# 📊 Analyse Churn — Freebox Revolution

> Cas pratique Data Scientist — iliad Group

---

## 📌 Contexte

Ce projet analyse le comportement de **20 000 abonnés Freebox Revolution** recrutés en janvier 2016 ou janvier 2017, sur la base d'un snapshot arrêté au **13 janvier 2022**.

L'objectif est d'analyser le churn (résiliation), la facturation, l'impact des offres de rétention, et de construire un modèle prédictif pour anticiper les départs.

---

## 📁 Contenu du repo

| Fichier | Description |
|---|---|
| `CasFree.ipynb` | Notebook Jupyter contenant l'intégralité de l'analyse |
| `presentation_churn_freebox.pptx` | Présentation PowerPoint des résultats pour l'oral |
| `fake_liste_users_revo_130122.yaml` | Dataset (à placer dans le même dossier) |

---

## 📦 Installation

```bash
pip install pyyaml pandas numpy matplotlib seaborn scikit-learn
```

---

## ▶️ Lancement

1. Cloner le repo
2. Placer le fichier `fake_liste_users_revo_130122.yaml` dans le même dossier que le notebook
3. Ouvrir `CasFree.ipynb` dans Jupyter
4. Adapter le `DATA_PATH` à ton chemin local :

```python
DATA_PATH = r'C:\ton\chemin\fake_liste_users_revo_130122.yaml'
```

5. Exécuter toutes les cellules

---

## 🔍 Structure de l'analyse

### 1. Chargement & Nettoyage
- Chargement du fichier YAML
- Création des variables `churned`, `duration`, `cohort`
- Calcul de la durée pour les clients encore actifs

### 2. Analyse du Churn
- Taille des cohortes 2016 et 2017
- Courbes de survie par cohorte, type de connexion et rétention
- Taux de churn mensuel avec identification des pics à 12/24/36 mois

### 3. Analyse de la Facturation
- Facture moyenne globale et par groupe
- Évolution de la facture totale et mensuelle avec le tenure

### 4. Impact des Offres de Rétention
- Comparaison churn rate / durée / facture avec et sans rétention
- Recommandation business

### 5. Modèle Prédictif du Churn
- Encodage des variables catégorielles
- Entraînement d'un Gradient Boosting Classifier
- Évaluation par courbe ROC et AUC

---

## 📈 Résultats clés

| Métrique | Valeur |
|---|---|
| Taux de churn global | 67.2% |
| Clients actifs en janvier 2022 | 6 569 (32.8%) |
| Facture totale moyenne | 1 612 € |
| Churn AVEC offre de rétention | 25.5% |
| Churn SANS offre de rétention | 68.2% |
| ROC-AUC du modèle prédictif | 0.743 |

---

## 🤖 Modèle ML

**Algorithme** : Gradient Boosting Classifier

**Paramètres** :
```python
GradientBoostingClassifier(
    n_estimators=200,   # 200 arbres de décision
    learning_rate=0.05, # vitesse d'apprentissage faible pour éviter le surapprentissage
    max_depth=4,        # profondeur max de chaque arbre (4 questions max)
    random_state=42     # reproductibilité des résultats
)
```

**Variables utilisées** : type de connexion, cohorte, canal d'acquisition, sous-offre, rétention

**Split** : 80% entraînement / 20% test (stratifié)

---

## 💡 Recommandations

1. **Cibler les fins d'engagement** : les pics de churn à 12, 24 et 36 mois sont des moments d'action prioritaires
2. **Généraliser la rétention** : seulement 2.5% des clients couverts alors que la rétention divise le churn par 2.7
3. **Accélérer la migration fibre** : les abonnés fibre churent moins et génèrent plus de revenus
4. **Déployer le modèle ML** : scorer les clients à risque chaque mois pour déclencher des offres proactives

---

## ⚠️ Limites

- Données synthétiques basées sur un cas réel
- Pas de données comportementales (appels SAV, usage internet...)
- Echantillon de 20k sur 100k clients éligibles → biais de sélection possible
- Le modèle devrait être ré-entraîné régulièrement en production

---

## 👤 Auteur

Youcef Hamadache
