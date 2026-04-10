# 🏥 Diabetes Hospital Readmission Prediction

<<<<<<< HEAD
![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange?logo=scikit-learn&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

> A supervised machine learning project that predicts whether a diabetic patient will be **readmitted to hospital within 30 days**, enabling healthcare providers to intervene early and reduce costs.

---

## 📌 Project Overview

Hospital readmissions within 30 days are a key quality metric in healthcare and cost the healthcare system billions annually. This project builds and evaluates classification models on **101,766 real patient encounters** from 130 US hospitals (1999–2008), identifying patients at high risk of early readmission.

**Key question:** *Given a patient's demographics, diagnosis, medications, and visit history; will they be readmitted within 30 days?*

---

## 🎯 Key Results

| Model | Accuracy | AUC-ROC | Notes |
|---|---|---|---|
| K-Nearest Neighbors | 91.0% | 0.56 | Best accuracy across approaches |
| Decision Tree | 90.4% | 0.52 | Consistent across OOP & procedural |
| Random Forest | **91.0%** | **0.61** | Best overall - highest AUC-ROC |

> Trained on 69,980 cleaned patient records · 80/20 train/validation split · evaluated on 13,996 held-out records.
> 
> ⚠️ **Note:** The dataset is class-imbalanced (~91% not readmitted, ~9% readmitted within 30 days). High accuracy reflects this imbalance — AUC-ROC is the more meaningful metric here. Random Forest achieved the best discrimination between classes.

---

## 🛠️ Tech Stack

| Area | Tools |
|---|---|
| Language | Python 3.9+ |
| Data wrangling | pandas, numpy |
| Visualisation | matplotlib, seaborn |
| Modelling | scikit-learn |
| Environment | Google Colab |

---

## 📂 Repository Structure

```
diabetes-readmission-prediction/
├── data/
│   ├── raw/                    # Original, unmodified source data
│   │   ├── diabetic_data.csv
│   │   └── IDs_mapping.csv
│   └── processed/              # Cleaned & feature-engineered data
│       └── diabetic_clean.csv
├── notebooks/
│   ├── 01_eda.ipynb            # Exploratory data analysis
│   ├── 02_cleaning.ipynb       # Cleaning & feature engineering
│   └── 03_modeling.ipynb       # Model training & evaluation
├── reports/
│   ├── technical_report.pdf
│   └── figures/                # Saved plots & charts
└── requirements.txt

```

---

## 🔍 Workflow

### 1. Exploratory Data Analysis (`01_eda.ipynb`)
- Profiled dataset shape, types, and summary statistics
- Detected and visualised missing values across all 50 features
- Investigated target class imbalance in `readmitted`
- Identified key patterns: older patients (60–80) had the highest readmission rates; shorter hospital stays correlated with quicker readmission

### 2. Data Cleaning & Feature Engineering (`02_cleaning.ipynb`)
- Resolved 97% missing `weight`, 53% `medical_specialty`, 52% `payer_code`
- Removed duplicate encounters — retained only each patient's first visit to prevent data leakage
- Excluded expired/hospice discharges (readmission is impossible for these records)
- **Engineered features:**
  - `age` intervals → numeric midpoints (e.g. `[60-70)` → `65`)
  - `total_visits` = outpatient + emergency + inpatient visit counts
  - `total_med_types` = count of distinct medication types prescribed
  - Binary target: `readmitted <30 days` → `1`, otherwise → `0`

### 3. Modelling (`03_modeling.ipynb`)
- Selected 17 clinically meaningful features
- Applied Label Encoding and One-Hot Encoding to categorical variables
- Scaled numeric features with `MinMaxScaler`
- 80/20 stratified train/validation split
- Implemented each of the three models in both **OOP** and **procedural** paradigms for clean, reusable code
- Evaluated with Accuracy, Confusion Matrix, Classification Report, and AUC-ROC
- Serialised final models to `.pkl` for deployment

---

## 📊 Dataset

| Property | Detail |
|---|---|
| Source | [UCI ML Repository](https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008) |
| Records | 101,766 patient encounters |
| Features | 50 (demographics, diagnoses, medications, visit history) |
| Target | Binary — readmitted within 30 days (1) or not (0) |
| Reference | [Strack et al., 2014](https://doi.org/10.1155/2014/781670) |

---

## ⚙️ Setup & Usage

```bash
# Clone the repository
git clone https://github.com/Ezinne-Toanyie/diabetes-readmission-prediction.git
cd diabetes-readmission-prediction

# Install dependencies
pip install -r requirements.txt
```

Open and run the notebooks **in order** in Google Colab or Jupyter:

```
01_eda.ipynb  →  02_cleaning.ipynb  →  03_modeling.ipynb
=======
Predicting 30-day hospital readmission for diabetic patients using machine learning, based on the [UCI Diabetes 130-US Hospitals dataset](https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008) (101,766 encounters, 50 features, 1999–2008).

---

## Project structure

```
diabetes-readmission/
├── data/
│   ├── raw/                    # Original dataset files (unchanged)
│   │   ├── diabetic_data.csv
│   │   └── IDs_mapping.csv
│   └── processed/              # Cleaned & engineered data
│       └── diabetic_clean.csv
├── notebooks/
│   ├── 01_eda.ipynb            # Exploratory data analysis
│   ├── 02_cleaning.ipynb       # Data cleaning & feature engineering
│   └── 03_modeling.ipynb       # Model training & evaluation
├── reports/
│   ├── technical_report.pdf
│   └── figures/
├── requirements.txt
└── .gitignore
```

---

## Dataset

| Property | Value |
|---|---|
| Source | UCI ML Repository |
| Encounters | 101,766 |
| Features | 50 (demographics, diagnoses, medications, visit history) |
| Target | `readmitted` — binary: `1` if readmitted within 30 days, `0` otherwise |
| Missing data | `weight` (97%), `medical_specialty` (53%), `payer_code` (52%) |

> The full data dictionary is available in `data/raw/IDs_mapping.csv`.

---

## Notebooks

### 01 — Exploratory Data Analysis
- Loads the raw dataset and inspects its shape, types, and summary statistics
- Identifies and visualises missing values
- Analyses the target variable (`readmitted`) distribution
- Explores readmission patterns by age, gender, and race
- Examines relationships between hospital stay length, medication count, and readmission using boxplots and a correlation heatmap

### 02 — Data Cleaning & Feature Engineering
- Replaces `?` and `Unknown/Invalid` with `NaN`
- Removes duplicate patient encounters (keeps first visit only)
- Drops high-missing columns: `weight`, `max_glu_serum`, `A1Cresult`
- Imputes remaining missing values (mode for categorical, median for numerical)
- Removes expired/hospice discharge records (cannot be readmitted)
- Maps admission type, discharge disposition, and admission source IDs to readable labels
- **Feature engineering:**
  - Converts age intervals (e.g. `[60-70)`) to numeric midpoints
  - Creates `total_visits` = outpatient + emergency + inpatient visits
  - Creates `total_med_types` = count of distinct medication types prescribed
  - Converts target to binary: `<30` → `1`, `>30` / `NO` → `0`
- Saves cleaned data to `data/processed/diabetic_clean.csv`

### 03 — Modelling
- Loads the cleaned dataset and selects 17 features for training
- Encodes categorical variables using Label Encoding and One-Hot Encoding
- Scales numeric features using `MinMaxScaler`
- Splits data 80/20 into training and validation sets
- Trains and evaluates three classifiers, each implemented in both OOP and procedural approaches:
  - **K-Nearest Neighbors (KNN)**
  - **Decision Tree**
  - **Random Forest**
- Evaluates models using Accuracy, Confusion Matrix, Classification Report, and AUC-ROC

---


## Setup

**Requirements:** Python 3.9+, Google Colab 

```bash
# Clone the repository — do NOT fork
git clone https://github.com/ParoCyber-DS-ML-Project-Team1/diabetes-readmission-prediction.git
cd diabetes-readmission-prediction

# Install dependencies
pip install -r requirements.txt
```

Run the notebooks in order: `01_eda` → `02_cleaning` → `03_modeling`.

---

## Dependencies

```
pandas
numpy
matplotlib
seaborn
scikit-learn
joblib
jupyter
>>>>>>> 44786269d90252e81385bab5913976f3b590b8f3
```

---

<<<<<<< HEAD
## 📄 Technical Report

A full write-up covering methodology, results, and recommendations is available in [`reports/technical_report.pdf`](reports/technical_report.pdf).

---

## 👤 Author

**Ezinne Toanyie**
[LinkedIn](https://linkedin.com/in/ezinne-toanyie) · [GitHub](https://github.com/Ezinne-Toanyie) · [Email](mailto:ce.toanyie@email.com)
=======
## Contributing

1. Clone the repo - do not fork.
2. Create a feature branch before writing any code:
   ```bash
   git checkout -b feature/your-name-task
   ```
3. Open a Pull Request into `main` when done.
4. Never commit directly to `main`.

---
>>>>>>> 44786269d90252e81385bab5913976f3b590b8f3
