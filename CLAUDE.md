# Pollen Time Series Analysis — France

Modelling and forecasting daily pollen concentrations across 4 climatically contrasted French cities (2022–2024).

## Tech Stack
- **Language:** Python 3.11+
- **Notebooks:** Jupyter (main deliverable)
- **Time Series:** statsmodels, pmdarima, scikit-learn
- **Data Fetching:** openmeteo-requests, requests-cache, retry-requests
- **Data Processing:** pandas, numpy
- **Visualization:** matplotlib, seaborn
- **Statistical Tests:** scipy, statsmodels (ADF, KPSS, Ljung-Box, etc.)

## Project Structure
```
.
├── CLAUDE.md
├── Data/                  # Raw + processed CSV files
│   ├── raw/               # Direct API downloads
│   └── processed/         # Cleaned, resampled, merged datasets
├── Notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_modelling.ipynb
│   ├── 04_forecasting_comparison.ipynb
│   ├── 05_hpi_analysis.ipynb
│   └── 06_historical_evolution.ipynb
├── figures/               # Exported PNG plots
└── tasks/
    ├── todo.md
    └── lessons.md
```

## Development Commands
```bash
# Install dependencies
pip install openmeteo-requests requests-cache retry-requests pandas numpy matplotlib seaborn statsmodels pmdarima scikit-learn scipy jupyter

# Launch notebooks
jupyter notebook Notebooks/

# Run a notebook headless (for reproducibility check)
jupyter nbconvert --to notebook --execute Notebooks/01_data_collection.ipynb
```

## Architecture & Key Conventions
- **Reproducibility:** All random seeds fixed (42). Relative paths only. Each notebook is self-contained.
- **Code language:** English comments and variable names
- **Report language:** English
- **Data granularity:** Hourly pollen and air quality → daily mean. Weather already daily.
- **Cities:** Paris (oceanic/continental), Marseille (Mediterranean), Strasbourg (continental), Bordeaux (oceanic)
- **Pollen species:** birch, alder, grass, olive, mugwort, ragweed
- **Weather covariates:** temp mean/max/min, precipitation, wind speed max, sunshine duration (h), relative humidity
- **Air-quality covariates:** ozone, nitrogen_dioxide, pm2_5
- **HPI notebook:** `Notebooks/05_hpi_analysis.ipynb` builds HPI as `temperature_2m_max_norm * mean(ozone_norm, nitrogen_dioxide_norm)` with MinMax-scaled components, then validates summer seasonality, Paris > Bordeaux, ARIMA+Fourier residuals vs HPI, and ARIMAX HPI lags 0/1/3/7.
- **Period:** 2022-01-01 to 2024-12-31
- **Model constraints:** No Prophet. No deep learning unless quantitatively justified. Progressive benchmarking simple → complex.
- **Math:** Every model choice justified with LaTeX in markdown cells.
- **Figures:** All exportable as PNG to `figures/`.

## Data Sources
- **Pollen:** Open-Meteo Air Quality API — `https://air-quality-api.open-meteo.com/v1/air-quality`
- **Air quality:** Open-Meteo Air Quality API — `https://air-quality-api.open-meteo.com/v1/air-quality`
- **Weather:** Open-Meteo Historical Weather API — `https://archive-api.open-meteo.com/v1/archive`
- Both free

---

## DÉMARRAGE DE SESSION
1. Lire tasks/lessons.md — appliquer toutes les leçons avant de toucher quoi que ce soit
2. Lire tasks/todo.md — comprendre l'état actuel
3. Si aucun des deux n'existe, les créer avant de commencer

## WORKFLOW

### 1. Planifier d'abord
- Passer en mode plan pour toute tâche non triviale (3+ étapes)
- Écrire le plan dans tasks/todo.md avant d'implémenter
- Si quelque chose ne va pas, STOP et re-planifier — ne jamais forcer

### 2. Stratégie sous-agents
- Utiliser des sous-agents pour garder le contexte principal propre
- Une tâche par sous-agent
- Investir plus de compute sur les problèmes difficiles

### 3. Boucle d'auto-amélioration
- Après toute correction : mettre à jour tasks/lessons.md
- Format : [date] | ce qui a mal tourné | règle pour l'éviter
- Relire les leçons à chaque démarrage de session

### 4. Standard de vérification
- Se demander : « Est-ce qu'un staff engineer validerait ça ? »

### 5. Exiger l'élégance
- Pour les changements non triviaux : existe-t-il une solution plus élégante ?
- Si un fix semble bricolé : le reconstruire proprement
- Ne pas sur-ingénieriser les choses simples

### 6. Correction de bugs autonome
- Quand on reçoit un bug : le corriger directement
- Aller dans les logs, trouver la cause racine, résoudre
- Pas besoin d'être guidé étape par étape

## PRINCIPES FONDAMENTAUX
- Simplicité d'abord — toucher un minimum de code
- Pas de paresse — causes racines uniquement, pas de fixes temporaires
- Ne jamais supposer — vérifier chemins, APIs, variables avant utilisation
- Demander une seule fois — une question en amont si nécessaire, ne jamais interrompre en cours de tâche

## GESTION DES TÂCHES
1. Planifier → tasks/todo.md
2. Vérifier → confirmer avant d'implémenter
3. Suivre → marquer comme terminé au fur et à mesure
4. Expliquer → résumé de haut niveau à chaque étape
5. Apprendre → tasks/lessons.md après corrections

## APPRENTISSAGES
(Claude remplit cette section au fil du temps)
