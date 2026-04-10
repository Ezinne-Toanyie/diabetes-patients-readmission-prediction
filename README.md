#  Diabetes Hospital Readmission Prediction


> A supervised machine learning project that predicts whether a diabetic patient will be **readmitted to hospital within 30 days**, enabling healthcare providers to intervene early and reduce costs.

---

##  Project Overview

Hospital readmissions within 30 days are a key quality metric in healthcare and cost the healthcare system billions annually. This project builds and evaluates classification models on **101,766 real patient encounters** from 130 US hospitals (1999–2008), identifying patients at high risk of early readmission.

**Key question:** *Given a patient's demographics, diagnosis, medications, and visit history; will they be readmitted within 30 days?*

---

##  Key Results

| Model | Accuracy | AUC-ROC | Notes |
|---|---|---|---|
| K-Nearest Neighbors | 91.0% | 0.56 | Best accuracy across approaches |
| Decision Tree | 90.4% | 0.52 | Consistent across OOP & procedural |
| Random Forest | **91.0%** | **0.61** | Best overall - highest AUC-ROC |

> Trained on 69,980 cleaned patient records · 80/20 train/validation split · evaluated on 13,996 held-out records.
> 
>  **Note:** The dataset is class-imbalanced (~91% not readmitted, ~9% readmitted within 30 days). High accuracy reflects this imbalance — AUC-ROC is the more meaningful metric here. Random Forest achieved the best discrimination between classes.

---

##  Tech Stack

| Area | Tools |
|---|---|
| Language | Python 3.9+ |
| Data wrangling | pandas, numpy |
| Visualisation | matplotlib, seaborn |
| Modelling | scikit-learn |
| Environment | Google Colab |

---

##  Repository Structure

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
| Reference |[Tayal, S. Diabetic Patients Readmission Prediction [dataset]](https://www.kaggle.com/datasets/saurabhtayal/diabetic-patients-readmission-prediction) |

---

##  Setup & Usage

```bash
### Clone the repository
git clone https://github.com/Ezinne-Toanyie/diabetes-readmission-prediction.git
cd diabetes-patients-readmission-prediction

### Install dependencies
pip install -r requirements.txt
```

Open and run the notebooks **in order** in Google Colab or Jupyter:

```
01_eda.ipynb  →  02_cleaning.ipynb  →  03_modeling.ipynb
=======


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

```

---

##  Technical Report

A full write-up covering methodology, results, and recommendations is available in [`reports/technical_report.pdf`](reports/technical_report.pdf).

---

##  Author

**Ezinne Toanyie**
[LinkedIn](https://linkedin.com/in/ezinne-toanyie) · [GitHub](https://github.com/Ezinne-Toanyie) · [Email](mailto:ce.toanyie@email.com)
