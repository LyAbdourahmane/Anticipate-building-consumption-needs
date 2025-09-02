# Prédiction de la Consommation Énergétique et des Émissions de CO₂ des Bâtiments Non Résidentiels – Seattle

## Contexte

Seattle s’est fixé un objectif ambitieux : **atteindre la neutralité carbone d’ici 2050**.
Pour y parvenir, la ville s’appuie sur une meilleure compréhension de la consommation énergétique et des émissions de gaz à effet de serre (GES) de ses bâtiments.

Les relevés manuels étant coûteux, ce projet vise à **prédire la consommation totale d’énergie et les émissions de CO₂** des bâtiments non résidentiels à partir de leurs caractéristiques structurelles (surface, usage, année de construction, localisation, etc.).

---

## Objectifs du projet

* Réaliser une **analyse exploratoire des données (EDA)** afin de mieux comprendre les patterns et anomalies.
* Construire et comparer plusieurs **modèles de Machine Learning** pour la prédiction :

  * Consommation énergétique (`SiteEnergyUseWN(kBtu)`)
  * Émissions de CO₂ (`TotalGHGEmissions`)
* Identifier les **facteurs principaux** influençant les prédictions.
* Fournir des **recommandations stratégiques** pour la ville de Seattle.

---

## Structure du projet

```
├── Analyse_Exploratoire.ipynb         # Notebook d’analyse exploratoire
├── Modelisation_ConsommationEnergy.ipynb  # Notebook prédiction consommation énergétique
├── Modelisation_EmissionC02.ipynb     # Notebook prédiction émissions de CO₂
├── Présentation_Final.pdf             # Présentation synthétique des résultats
├── requirements_poetry/               # Gestion des dépendances via Poetry
│   ├── pyproject.toml
│   └── poetry.lock
└── README.md
```

---

##  Données

* **Source** : City of Seattle – 2016 Building Energy Benchmarking
* **Dimensions initiales** : 3376 lignes × 46 colonnes
* **Filtrage** : seulement les bâtiments **non résidentiels** (≈ 1546 lignes)
* **Dataset final** : 1083 bâtiments après nettoyage et suppression des colonnes redondantes

---

## Analyse exploratoire (EDA)

* **Variables cibles** :

  * `SiteEnergyUseWN(kBtu)` → consommation énergétique normalisée météo
  * `TotalGHGEmissions` → émissions de CO₂
* **Insights clés** :

  * Corrélation **très forte** entre consommation et émissions (r ≈ 0.89).
  * Les hôpitaux et laboratoires sont les plus énergivores.
  * L’année de construction influence la consommation (pics années 1990–2000).
  * Surface totale (GFA) = facteur structurant majeur.

---

## Modélisation

### Consommation énergétique

* **Meilleur modèle** : **Random Forest**
* **Performances** :

  * R² = 0.82
  * RMSE = 9.63M kBtu
  * MAE = 4.40M kBtu

### Émissions de CO₂

* **Meilleur modèle** : **XGBoost**
* **Performances** :

  * R² = 0.95
  * RMSE = 194.55
  * MAE = 103.48

### Méthodologie

* Pipelines avec **RobustScaler** (numérique) & **LabelEncoder** (catégoriel).
* Comparaison de plusieurs algorithmes :

  * Régression Linéaire
  * SVR
  * Random Forest
  * Gradient Boosting
  * XGBoost
* Validation croisée & courbes d’apprentissage.
* Exclusion du score **ENERGY STAR** -> amélioration des performances (évite bruit et fuite d’information).

---

## Facteurs d’influence

* **Superficie totale (GFA)** = facteur le plus déterminant.
* **Type de bâtiment (PrimaryPropertyType)** impacte fortement consommation & émissions.
* Variables dérivées des consommations **exclues** pour éviter le *data leakage*.

---

## Installation & utilisation

### Prérequis

* Python 3.10+
* [Poetry](https://python-poetry.org/) pour la gestion des dépendances

### Installation

```bash
# Cloner le repo
git clone https://github.com/LyAbdourahmane/Anticipate-building-consumption-needs.git
cd <Anticipate-building-consumption-needs>

# Installer les dépendances via Poetry
cd requirements_poetry
poetry install
poetry shell
```

Ouvrir ensuite :

* `Analyse_Exploratoire.ipynb`
* `Modelisation_ConsommationEnergy.ipynb`
* `Modelisation_EmissionC02.ipynb`

---

## Résultats principaux

* La **superficie** et le **type de bâtiment** sont les déterminants majeurs.
* **Random Forest** est le plus fiable pour la consommation énergétique.
* **XGBoost** atteint une précision remarquable pour les émissions de CO₂ (R² = 0.95).
* Les modèles permettent à Seattle de réduire ses **coûts de mesure** et d’orienter ses **politiques énergétiques**.

---

## Auteur

Projet réalisé par **Abdourahamane LY**
Dans le cadre d’une mission de Data Science pour la ville de Seattle.

---
