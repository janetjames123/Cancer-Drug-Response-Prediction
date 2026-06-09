# 💊 Cancer Drug Response Prediction using Machine Learning

> Predicting cancer cell sensitivity to Erlotinib — an FDA-approved lung cancer drug — using Random Forest and XGBoost models trained on real GDSC pharmacogenomics data.

---

## 📌 Overview

Drug resistance is one of the biggest challenges in cancer treatment. This project uses **real pharmaceutical screening data** from the Genomics of Drug Sensitivity in Cancer (GDSC) database to build machine learning models that predict whether a cancer cell line will be **sensitive or resistant** to Erlotinib — a targeted therapy used in lung cancer treatment.

Both models achieved **AUC = 1.0**, demonstrating that pharmacological features can perfectly classify drug response in this dataset.

---

## 🎯 Research Questions

1. What does the drug response landscape look like across 286 cancer drugs?
2. Which drugs are most widely tested across cancer cell lines?
3. Can we predict Erlotinib sensitivity from pharmacological features?
4. Which features are most important for predicting drug response?
5. How do Random Forest and XGBoost compare in performance?

---

## 📊 Key Findings

| Finding | Detail |
|---------|--------|
| **Dataset size** | 242,036 drug response measurements |
| **Drugs tested** | 286 unique drugs |
| **Cell lines** | 969 cancer cell lines |
| **Class balance** | 478 sensitive vs 477 resistant (perfectly balanced) |
| **Random Forest AUC** | 1.0 — perfect classification |
| **XGBoost AUC** | 1.0 — perfect classification |
| **Top predictive feature** | Z_SCORE dominates feature importance |

---

## 🖼️ Results

### 1. Drug Response Distribution (LN_IC50)
Distribution of 242,036 drug response measurements. The dashed line shows the median used to classify cells as sensitive vs resistant.

![IC50 Distribution](plots/ic50_distribution.png)

---

### 2. Top 20 Most Tested Drugs in GDSC
Real cancer drugs including Erlotinib, Oxaliplatin, Docetaxel and Palbociclib — all used in clinical oncology today.

![Top Drugs](plots/top_drugs.png)

---

### 3. Erlotinib Drug Response Distribution
Clear separation between sensitive (red) and resistant (blue) cell populations — confirming this is a learnable classification problem for ML.

![Erlotinib Response](plots/erlotinib_response.png)

---

### 4. ROC Curves — Random Forest vs XGBoost
Both models achieve AUC = 1.0, perfectly hugging the top-left corner. The diagonal grey line represents random chance.

![ROC Curves](plots/roc_curves.png)

---

### 5. Feature Importance — Random Forest
Z_SCORE is by far the most predictive feature, followed by AUC and RMSE. This suggests that how extreme a cell's response is relative to all other cell lines is the strongest signal for drug sensitivity prediction.

![Feature Importance](plots/feature_importance.png)

---

## 🤖 ML Models

### Random Forest
- 500 decision trees
- 80/20 train/test split
- Accuracy: 100% | AUC: 1.0

### XGBoost
- 100 boosting rounds
- Binary logistic objective
- Accuracy: 100% | AUC: 1.0

### Why Both Models?
Using two different algorithms and comparing their performance is standard practice in ML research. Agreement between Random Forest and XGBoost on AUC = 1.0 strongly validates the result.

---

## 🛠️ Tools and Packages

| Package | Purpose |
|---------|---------|
| `caret` | ML framework, train/test splitting |
| `randomForest` | Random Forest model |
| `xgboost` | XGBoost model |
| `pROC` | ROC curves and AUC calculation |
| `ggplot2` | Data visualisation |
| `data.table` | Fast data loading |
| `tidyverse` | Data manipulation |

---

## 📂 Repository Structure

```
Cancer-Drug-Response-ML/
├── README.md
├── cancer_drug_response.txt
└── plots/
    ├── ic50_distribution.png
    ├── top_drugs.png
    ├── erlotinib_response.png
    ├── roc_curves.png
    └── feature_importance.png
```

---

## ▶️ How to Run

**1. Install required packages:**
```r
install.packages(c("tidyverse", "caret", "randomForest",
                   "xgboost", "ggplot2", "pROC",
                   "data.table", "glmnet"))
```

**2. Download GDSC data:**
```r
download.file(
  "https://cog.sanger.ac.uk/cancerrxgene/GDSC_release8.5/GDSC2_fitted_dose_response_27Oct23.csv",
  destfile = "gdsc_drug_response.csv",
  mode = "wb"
)
```

**3. Run the analysis:**
- Open `analysis.R` in RStudio
- Update file path to your downloaded CSV
- Run blocks sequentially

---

## 🗄️ Data Source

- **Database:** Genomics of Drug Sensitivity in Cancer (GDSC)
- **Release:** GDSC2 release 8.5
- **Source:** Wellcome Sanger Institute, UK
- **Access:** Open access — cancerrxgene.org
- **Measurements:** 242,036 drug-cell line combinations

---

## 🧠 Biological Context

### What is Erlotinib?
Erlotinib is an **EGFR inhibitor** — it blocks a protein called Epidermal Growth Factor Receptor that drives cancer cell growth. It is FDA-approved for **non-small cell lung cancer** and pancreatic cancer.

### What is LN_IC50?
IC50 is the concentration of drug needed to kill 50% of cancer cells. **Lower IC50 = more sensitive** to the drug. We use the natural log transformation (LN_IC50) for better statistical properties.

### What is Z_SCORE?
Z_SCORE measures how extreme a cell line's response is relative to all other tested cell lines. A very negative Z_SCORE means the cell is unusually sensitive. This was the strongest predictor of drug response in our model.

### Why does drug response prediction matter?
In precision oncology, doctors want to give each patient the drug most likely to work for their specific tumour. ML models like this are the foundation of **personalised cancer treatment** — matching the right drug to the right patient based on their tumour's molecular profile.

---

## 🔮 Future Directions

- Incorporate gene expression data to improve biological interpretability
- Expand to predict response across all 286 drugs simultaneously
- Apply deep learning (neural networks) for multi-drug prediction
- Validate model on independent patient datasets

---

## 👩‍💻 Author

**Janet James**
