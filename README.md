# 💘 Tinder Speed Dating : EDA & Machine Learning Pipeline

[![Python](https://img.shields.io/badge/Python-3.11-blue)](https://python.org)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Machine_Learning-F7931E)](https://scikit-learn.org/)
[![Seaborn](https://img.shields.io/badge/Seaborn-Data_Viz-4C72B0)](https://seaborn.pydata.org/)

> **Projet de Certification RNCP - Concepteur Développeur en Science des données**
> * ✅ **Bloc 2 :** Analyse Exploratoire, Descriptive et Inférentielle (EDA)
> * ✅ **Bloc 3 :** Machine Learning Supervisé (Classification)

---

## 📌 Problématique Métier
L'équipe marketing de Tinder constate une baisse des "Matchs". L'objectif est d'analyser un dataset de +8000 rencontres rapides (Speed Dates) pour identifier les véritables vecteurs de décision comportementale, puis de modéliser une Intelligence Artificielle capable de prédire les futurs matchs.

## 🏗️ Architecture Analytique & Prédictive

### 1. Analyse Exploratoire & Statistique (EDA)
* **Data Cleaning (Imputation) :** Les données manquantes (MNAR) ont été imputées par la **médiane** pour préserver la distribution statistique sans biaiser l'échantillon par des suppressions agressives.
* **Détection d'Outliers :** Visualisation et traitement de la variance via Boxplots (Ex: âge des participants).
* **Corrélations (Pearson) :** Révélation d'un biais de désirabilité sociale. L'attractivité physique ($r=0.49$) surclasse largement les intérêts partagés ($r=0.22$) dans la décision finale.

### 2. Modélisation Machine Learning (Classification)
* **Pipeline de Préparation :** Isolation de la Target binaire (`match`), découpage avec stratification (`stratify=y`) et normalisation des variables prédictives via `StandardScaler`.
* **Algorithme de Classification :** `LogisticRegression` implémentée avec l'hyperparamètre `class_weight='balanced'` pour contrer le fort déséquilibre des classes (16% de matchs réels).
* **Validation & Performances :** 
  * Validation croisée robuste (K-Fold CV = 5) certifiant l'absence d'Overfitting.
  * Évaluation métrique axée sur le **F1-Score** et la **Matrice de Confusion**, écartant volontairement l'Accuracy (paradoxe des données asymétriques).

## 🚀 Reproduction de l'Environnement
```bash
# 1. Cloner le repository
git clone [https://github.com/CarelleNouko/speed-dating-ml.git](https://github.com/CarelleNouko/speed-dating-ml.git)
cd speed-dating-ml

# 2. Créer un environnement virtuel isolé
python3 -m venv .venv
source .venv/bin/activate

# 3. Installer les dépendances
pip install -r requirements.txt

# 4. Lancer le Jupyter Notebook
jupyter notebook
Analyse et ML sur données Speed Dating - Tinder
