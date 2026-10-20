# 🧬 OncoPredict: Chemotherapy Resistance Prediction from Multi-Omics Data

**Predicting chemotherapy resistance in breast cancer patients from combined genomic, transcriptomic and proteomic features, comparing linear, kernel and neural models.**

![Python](https://img.shields.io/badge/Python-scikit--learn-blue)
![Data](https://img.shields.io/badge/Data-Multi--Omics-purple)
![Paper](https://img.shields.io/badge/Report-IEEE%20format-lightgrey)

---

## Problem

Chemotherapy resistance is a major cause of treatment failure in breast cancer. Predicting it **before** treatment would let clinicians choose therapies that work and spare patients toxic drugs that won't help them.

## Data

A **synthetic multi-omics dataset** of 5,000 patients. Each patient has three feature types for key breast-cancer genes (BRCA1, BRCA2, TP53, ATM, CHEK2, PALB2, BARD1, MRE11A, ...):

- **Genomic** (variants)
- **Transcriptomic** (expression)
- **Proteomic** (protein levels)

It also includes clinical features: ethnicity, chemotherapy regimen and tumor stage.

> The data is synthetic, generated for this study. Results show the modelling pipeline and are not clinical performance claims.

## Pipeline

1. Imputation of missing values and one-hot encoding of clinical variables
2. Scaling, plus PCA for feature analysis
3. SMOTE to balance the resistant and sensitive classes
4. Models: **Logistic Regression**, **Linear SVM**, **MLP (16-8, ReLU, Adam)**, and a **soft-voting ensemble**
5. Evaluation: hold-out test set (1,474 samples), 5-fold cross-validation, confusion matrices and ROC curves

## Results (test set)

| Model | Accuracy |
|---|---|
| Logistic Regression | 0.90 |
| Linear SVM | 0.90 |
| Voting ensemble | 0.90 |
| **MLP** | **0.985** |

The MLP clearly beats the linear models, which suggests the interactions between omics layers are non-linear.

## Repository structure

```
├── OncoPredict.ipynb       # Main pipeline: preprocessing → models → evaluation
├── task bonus.ipynb        # Additional experiments
├── ML final project.pdf    # Full report (IEEE format)
└── *.csv                   # Synthetic multi-omics datasets
```

## Running

```bash
pip install pandas numpy scikit-learn imbalanced-learn matplotlib seaborn jupyter
jupyter notebook OncoPredict.ipynb
```

## Future work

- Validate on real cohorts such as **TCGA-BRCA**
- Per-omics ablation to show which layer carries the signal
- SHAP explanations for gene-level interpretability
