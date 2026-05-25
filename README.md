# Cross-Domain-Synthesis
A machine learning pipeline mitigating extreme class imbalance in network security and financial fraud detection using memory-constrained SMOTE and XGBoost.




# Cross-Domain Synthesis

**Mitigating Extreme Class Imbalance in Network Security and Financial Fraud Using SMOTE**

![Python](https://img.shields.io/badge/Python-3.14+-blue.svg)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-Enabled-orange.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-Optimized-green.svg)
![License](https://img.shields.io/badge/License-MIT-purple.svg)

## ⚠️ Problem Statement
As our world becomes increasingly digital, cyberattacks and financial fraud are growing more sophisticated. However, training AI to catch these threats comes with a massive hurdle: real-world data is heavily unbalanced. For every million normal network logins or credit card swipes, there might be only one actual attack. 

If predictive models are trained on this skewed data, the model takes the easy way out. It simply guesses "normal" every single time, achieving a deceptive 99% accuracy while letting the real threats slip right by unnoticed. Extreme class imbalance remains a foundational barrier in both network and financial cybersecurity.

## 📌 Project Overview
This repository contains a robust data engineering and machine learning pipeline designed to solve the accuracy paradox in anomaly detection. By looking at real datasets from both network security and financial fraud, this project first exposes the extreme class imbalance. 

Then, by cleaning the messy data and using the SMOTE algorithm to generate mathematically realistic synthetic attacks, the pipeline balances the scales within local hardware constraints. This standardized environment allows ensemble models (like XGBoost) to actually learn how to hunt down rare threats with exceptional precision and recall.

## 📂 Repository Structure
```text
├── data/
│   ├── raw/                 # Original, unedited datasets (Ignored by Git)
│   └── processed/           # Cleaned, SMOTE-balanced datasets
├── notebooks/
│   ├── EDA.ipynb            # Network data exploration & logarithmic visualization
│   ├── Fraud_EDA.ipynb      # Financial data exploration & cross-domain verification
│   ├── SMOTE_Balancing.ipynb# Memory-constrained synthetic data generation
│   └── Model_Training.ipynb # Baseline initialization & Hyperparameter tuning
├── requirements.txt         # Environment dependencies
└── README.md                # Project documentation
```

### 📊 Datasets
1. **Network Security:** [CICIDS2017 Dataset](https://www.unb.ca/cic/datasets/ids-2017.html) (2.5+ million rows) - *Normal traffic ~83%, Minority attacks <0.01%*
2. **Financial Fraud:** [IEEE-CIS Fraud Detection](https://www.kaggle.com/c/ieee-fraud-detection) (~600,000 rows) - *Fraudulent transactions <3.5%*

### ⚙️ Core Pipeline Methodology
1. **Data Preprocessing:** Rigorous null-imputation (median for numerical columns to resist outlier skewing, 'Unknown' for categorical text) and threshold-based feature dropping for highly corrupted columns (missing >80% data).
2. **Algorithmic Balancing:** Engineered a custom `sampling_strategy` dictionary for SMOTE to hard-cap synthetic generation at 200,000 rows per minority attack type. This mathematically balances the data while actively preventing local RAM overflow.
3. **Model Evaluation:** Utilized parallel processing (`n_jobs=-1`) to train Random Forest and XGBoost classifiers on 2.5 million rows. Evaluated via Confusion Matrices, Precision, and Recall rather than basic accuracy to ensure zero tolerance for false negatives.
4. **Optimization:** Extracted a stratified 10% sample to conduct highly efficient, localized `RandomizedSearchCV` hyperparameter tuning (learning rate, max depth, estimators).

### 🚀 Getting Started

### Prerequisites
Ensure you have Python 3.14+ installed. It is highly recommended to use a virtual environment.

### Installation
1. Clone this repository:
   ```bash
   git clone [https://github.com/ARES0093/Cross-Domain-Synthesis.git](https://github.com/ARES0093/Cross-Domain-Synthesis.git)
   ```
2. Navigate to the project directory:
   ```bash
   cd Cross-Domain-Synthesis
   ```
3. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### Execution
Launch Jupyter Notebook or open the project in VS Code to run the pipeline sequentially:
1. `EDA.ipynb`
2. `Fraud_EDA.ipynb`
3. `SMOTE_Balancing.ipynb`
4. `Model_Training.ipynb`

## 🔮 Future Work
* **Real-Time Stream Processing:** Transitioning from static CSV file analysis to real-time data streaming architectures (e.g., Apache Kafka) for instantaneous threat detection.
* **Deep Learning Implementation:** Exploring Long Short-Term Memory networks (LSTMs) or Autoencoders to identify complex "Zero-Day" attack vectors.
* **Cloud Deployment:** Migrating the SMOTE synthesis and model training pipelines to AWS/GCP to remove local hardware memory caps.
