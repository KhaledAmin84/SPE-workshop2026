[README.md](https://github.com/user-attachments/files/26596409/README.md)
# 🛢️ Machine Learning for Well Log Analysis
### SPE Practical Workshop — Beginner Sessions

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.x-orange)
![XGBoost](https://img.shields.io/badge/XGBoost-2.x-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 📖 Overview

This repository contains two hands-on Jupyter notebooks developed for SPE beginner practical sessions on applying machine learning to well log data. Both notebooks follow a clean, step-by-step workflow — from raw data loading to blind well prediction — using open-source Python tools only.

| Notebook | Problem Type | Target | Dataset |
|---|---|---|---|
| `DTC_Log_Prediction_SPE.ipynb` | Regression | DT — Compressional Slowness (µs/ft) | FORCE 2020 North Sea wells |
| `Lithology_Classification_SPE.ipynb` | Classification | LITH — Rock type | FORCE 2020 North Sea wells |

---

## 📂 Repository Structure

```
├── DTC_Log_Prediction_SPE.ipynb          # Sonic log prediction (regression)
├── Lithology_Classification_SPE.ipynb    # Lithology classification
└── README.md
```

> **Data note:** The CSV data files (`Wells.csv`, `Wells_Lith.csv`) are sourced from the [FORCE 2020 Machine Learning Competition](https://github.com/bolgebrygg/Force-2020-Machine-Learning-competition). Download them separately and place in your Google Drive or local path as shown in the notebooks.

---

## 🗂️ Notebook 1 — DTC Log Prediction

**File:** `DTC_Log_Prediction_SPE.ipynb`

Predicts compressional sonic slowness (DT) from conventional well logs using supervised regression.

### Wells
| Role | Wells |
|---|---|
| Training | `15/9-F-11 A`, `15/9-F-1 A` |
| Blind test | `15/9-F-1 B` |

### Features & Target
- **Input logs:** GR · RHOB · NPHI · PEF
- **Target:** DT (µs/ft)

### Workflow
1. Load CSV data (LAS reader also included as reference)
2. Separate blind well before any processing
3. Data cleaning — NaN removal + physical range filters
4. Exploratory visualization — histograms, boxplots per well, correlation heatmap, pairplot, log tracks
5. Feature scaling with `StandardScaler`
6. 80/20 train/validation split
7. Compare 8 regression models (LazyPredict-style)
8. Retrain best model on full training data — feature importance + scatter plot
9. Blind well prediction — R², MAE, RMSE + actual vs predicted log track

### Models Compared
`Linear Regression` · `Ridge` · `Lasso` · `KNN` · `Decision Tree` · `Random Forest` · `XGBoost` · `MLP Neural Network`

### Evaluation Metrics
| Metric | Meaning |
|---|---|
| R² | Proportion of variance explained (1.0 = perfect) |
| MAE | Mean absolute error in µs/ft (lower = better) |
| RMSE | Root mean square error in µs/ft (lower = better) |

---

## 🗂️ Notebook 2 — Lithology Classification

**File:** `Lithology_Classification_SPE.ipynb`

Predicts rock type (lithology) from well logs using supervised classification.

### Wells
| Role | Wells |
|---|---|
| Training | All wells except blind well |
| Blind test | `15/9-13` |

### Features & Target
- **Input logs:** GR · RHOB · NPHI · PEF · RDEP · DTC
- **Target:** LITH (Shale, Sandstone, Limestone, Chalk, Marl, …)

### Workflow
1. Load CSV data
2. Separate blind well before any processing
3. Data cleaning — NaN removal + physical range filters
4. Exploratory visualization — class balance bar chart, histograms, boxplots per lithology, log tracks with lithology color fill
5. Label encoding (text → integer) + `StandardScaler`
6. Stratified 80/20 train/validation split
7. Compare 7 classification models (LazyPredict-style)
8. Retrain best model — feature importance
9. Blind well prediction — accuracy, F1, classification report, normalized confusion matrix, actual vs predicted log track

### Models Compared
`Logistic Regression` · `Naive Bayes` · `KNN` · `Decision Tree` · `Random Forest` · `XGBoost` · `Gradient Boosting`

### Evaluation Metrics
| Metric | Meaning |
|---|---|
| Accuracy | Overall % correct predictions |
| F1 (weighted) | Balances precision and recall — preferred with class imbalance |
| Confusion matrix | Which lithologies the model confuses with each other |

> **Note:** Shale dominates the dataset — weighted F1 is used as the primary ranking metric to account for class imbalance.

---

## ⚙️ Requirements

```
numpy
pandas
matplotlib
seaborn
scikit-learn
xgboost
lasio
```

Install all dependencies:
```bash
pip install numpy pandas matplotlib seaborn scikit-learn xgboost lasio
```

Or in Google Colab, run at the top of each notebook:
```python
!pip install lasio
```
(All other libraries are pre-installed in Colab.)

---

## 🚀 Getting Started

### Option 1 — Google Colab (recommended)
1. Open the notebook directly in Colab using the badge at the top
2. Mount your Google Drive: `drive.mount('/content/drive')`
3. Upload `Wells.csv` / `Wells_Lith.csv` to your Drive under `MyDrive/SPE/`
4. Run all cells from top to bottom

### Option 2 — Local (Jupyter)
1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>
   ```
2. Install dependencies (see above)
3. Place data files in the path referenced in the notebooks
4. Launch Jupyter:
   ```bash
   jupyter notebook
   ```

---

## 🧠 Key Concepts Covered

| Concept | Covered in |
|---|---|
| Regression vs Classification | Both notebooks |
| Physical range filters for QC | Both notebooks |
| Blind well validation | Both notebooks |
| StandardScaler — fit on train only | Both notebooks |
| Feature importance (tree-based models) | Both notebooks |
| Class imbalance — F1 vs Accuracy | Lithology notebook |
| Label encoding | Lithology notebook |
| Stratified splitting | Lithology notebook |
| Confusion matrix | Lithology notebook |
| Correlation heatmap & pairplot | DTC notebook |
| LAS file reading with `lasio` | DTC notebook |

---

## 📊 Dataset

Both notebooks use data from the **FORCE 2020 Well Log & Lithology Machine Learning Competition** (North Sea wells, Norway).

- **Citation:** Bormann P., Aursand P., Dilib F., Manral S., Dischington P., and Strand J. (2020). FORCE Machine Learning Competition.
- **License:** CC BY 4.0
- **Source:** 

---

## 👤 Author

**Khaled Amin**
Geoscientist — Belayim Petroleum Company (Petrobel), Egypt

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/)

---

## 📄 License

This project is licensed under the MIT License — feel free to use and adapt for educational purposes with attribution.
