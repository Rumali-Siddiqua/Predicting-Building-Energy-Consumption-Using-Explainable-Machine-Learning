# Predicting-Building-Energy-Consumption-Using-Explainable-Machine-Learning

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.0%2B-orange)](https://scikit-learn.org/)

## Overview

Buildings account for nearly 40% of global energy consumption, with HVAC systems as the largest contributor. Accurately forecasting energy demands is critical for reducing waste, lowering costs, and cutting carbon emissions.

This project develops and compares four machine learning models to predict **Heating Load (HL)** and **Cooling Load (CL)** from structural building parameters, with a focus on **explainability** — understanding *why* buildings consume more energy, not just predicting that they do.

**Key results:**
- Random Forest & Gradient Boosting: R²=0.998 for Heating Load
- MLP Neural Network: R²=0.980 for Cooling Load
- All nonlinear models significantly outperform Linear Regression (R²=0.905)
- Feature importance analysis reveals **Relative Compactness** and **Overall Height** as dominant energy drivers

---

## Table of Contents

- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Models](#models)
- [Results](#results)
- [Reproducibility](#reproducibility)
- [Citation](#citation)

---

## Dataset

This project uses the **UCI Energy Efficiency Dataset**, a publicly available dataset of 768 simulated residential buildings.

| Property | Value |
|---|---|
| Samples | 768 |
| Features | 8 structural parameters |
| Targets | Heating Load, Cooling Load (kWh/m²) |
| Train/Test Split | 80% / 20% |

**Features:**
1. Relative Compactness
2. Surface Area
3. Wall Area
4. Roof Area
5. Overall Height
6. Orientation
7. Glazing Area
8. Glazing Area Distribution

**Download the dataset:**
- UCI Repository: https://archive.ics.uci.edu/ml/datasets/energy+efficiency
- Direct download: https://archive.ics.uci.edu/ml/machine-learning-databases/00242/ENB2012_data.xlsx

> After downloading, rename the file to `energy.xlsx` and place it in the root project folder alongside the notebook.

**Citation for dataset:**
> Tsanas, A. & Xifara, A. (2012). Accurate quantitative estimation of energy performance of residential buildings. *Energy and Buildings*, 49, 560–567. DOI: 10.1016/j.enbuild.2012.03.003

---

## Project Structure

```
building-energy-prediction/
│
├── Energy_Consumption_Prediction.ipynb   # Main Jupyter notebook (full analysis)
├── energy.xlsx                           # Dataset (download from UCI — see above)
├── requirements.txt                      # Python dependencies
└── README.md
```

---

## Installation

**1. Clone the repository:**
```bash
git clone https://github.com/Rumali-Siddiqua/building-energy-prediction.git
cd building-energy-prediction
```

**2. Create a virtual environment (recommended):**
```bash
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate
```

**3. Install dependencies:**
```bash
pip install -r requirements.txt
```

**4. Download the dataset:**

Download the dataset from the [UCI Repository](https://archive.ics.uci.edu/ml/datasets/energy+efficiency), rename it to `energy.xlsx`, and place it in the root project folder.

---

## Usage

**Run the Jupyter notebook:**
```bash
jupyter notebook Energy_Consumption_Prediction.ipynb
```

Run all cells in order. The notebook walks through the complete pipeline:
1. Data loading and preprocessing
2. Feature standardization and train/test split
3. Model training (Linear Regression, Random Forest, Gradient Boosting, MLP)
4. Model evaluation (MSE, RMSE, R², MAE, MAPE)
5. Feature importance analysis
6. Visualization of results

---

## Models

Four models are trained and compared for both Heating Load and Cooling Load prediction:

| Model | Type | Key Hyperparameters |
|---|---|---|
| Linear Regression | Baseline | — |
| Random Forest | Ensemble | random_state=42 |
| Gradient Boosting | Sequential Ensemble | random_state=42 |
| MLP Neural Network | Neural Network | random_state=42 |

All models use **standardized features** (StandardScaler) and an **80/20 train/test split** with `random_state=42`.

**Explainability:** Feature importance scores are extracted from Random Forest and Gradient Boosting using scikit-learn's built-in `feature_importances_` attribute.

---

## Results

### Model Performance

| Model | Target | MSE | RMSE | R² |
|---|---|---|---|---|
| MLP | Cooling | 2.15 | 1.47 | **0.980** |
| Gradient Boosting | Cooling | 2.25 | 1.50 | 0.979 |
| Random Forest | Cooling | 2.95 | 1.72 | 0.972 |
| Linear Regression | Cooling | 9.85 | 3.14 | 0.907 |
| Random Forest | Heating | 0.17 | 0.41 | **0.998** |
| Gradient Boosting | Heating | 0.19 | 0.43 | **0.998** |
| MLP | Heating | 1.06 | 1.03 | 0.988 |
| Linear Regression | Heating | 8.90 | 2.98 | 0.905 |

### Key Findings

- **Relative Compactness** and **Overall Height** are the dominant predictors of both heating and cooling loads across all models
- More compact buildings require significantly less energy — a directly actionable insight for architects
- Increasing Overall Height from 3.5m to 7.0m raises cooling load by ≈12 kWh/m² and heating load by ≈14 kWh/m²
- Orientation and Glazing Area Distribution contribute near zero to both targets
- All nonlinear models far outperform Linear Regression, confirming that building energy relationships are fundamentally nonlinear

---

## Reproducibility

This project is fully reproducible:

- **Fixed random seeds:** `random_state=42` used across all models and train/test splits
- **Public dataset:** UCI Energy Efficiency Dataset freely available at archive.ics.uci.edu
- **Pinned dependencies:** all package versions specified in `requirements.txt`
- **Self-contained notebook:** running all cells in order reproduces every figure and metric in the poster

---

## Requirements

```
numpy>=1.21.0
pandas>=1.3.0
scikit-learn>=1.0.0
matplotlib>=3.4.0
seaborn>=0.11.0
jupyter>=1.0.0
openpyxl>=3.0.0
```

---

## Citation

If you use this work, please cite:

**Dataset:**
```
Tsanas, A. & Xifara, A. (2012). Accurate quantitative estimation of energy performance 
of residential buildings. Energy and Buildings, 49, 560–567.
```

**Related references:**
```
Amasyali, K. & El-Gohary, N. (2018). A review of data-driven building energy consumption 
prediction studies. Renewable and Sustainable Energy Reviews, 81.

Pedregosa, F. et al. (2011). Scikit-learn: Machine learning in Python. 
Journal of Machine Learning Research, 12, 2825–2830.

Chen, T. & Guestrin, C. (2016). XGBoost: A scalable tree boosting system. 
Proc. 22nd ACM SIGKDD, 785–794.
```

---
