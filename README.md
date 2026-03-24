#  Drug Sensitivity Prediction for Breast Cancer
> Capstone project — Al Akhawayn University | Supervised by Dr. Mouna Kettani  
> Research proposal submitted to **IEEE BIBM 2024** (International Conference on Bioinformatics and Biomedicine)

---

##  Problem

Cancer treatment outcomes vary drastically between patients due to genetic diversity. Standard therapies often fail to account for individual tumor profiles, leading to trial-and-error prescribing that is costly and harmful. This project addresses that gap by building a machine learning pipeline to predict **drug sensitivity (AUC)** from genomic and molecular data — enabling more precise, personalized treatment strategies for breast cancer patients.

---

##  Approach

An end-to-end ML pipeline trained on the **GDSC (Genomics of Drug Sensitivity in Cancer)** dataset, integrating three data sources: drug response metrics, cancer cell line profiles, and compound annotations. After preprocessing 13,106 samples across 18 features, **XGBoost** was selected as the primary model via automated benchmarking (LazyPredict, 42 models evaluated) and optimized with Grid Search.

---

## Results

| Metric | Training | Test |
|--------|----------|------|
| R² Score | **0.9716** | **0.9272** |
| RMSE | **0.0228** | **0.0373** |

Key predictors identified: `TARGET_PATHWAY`, `Z_SCORE`, `DRUG_NAME`, `TARGET`, `DRUG_ID`

---

## 🛠️ Pipeline

### 1. Data Integration
- Merged GDSC drug response data, cell line details (CNA, gene expression, methylation), and compound annotations using `COSMIC_ID` and `DRUG_ID`

### 2. Preprocessing
- **Missing values:** KNN Imputation (k=5) for numerical genomic features; `'Unknown'` fill for categorical (MSI, TARGET)
- **Scaling:** MinMaxScaler → all numerical features normalized to [0, 1]
- **Encoding:** LabelEncoder for high-cardinality categoricals (`TARGET_PATHWAY`, Cancer Type)
- **Skewness correction:** Log transformation on AUC distribution
- **Redundancy removal:** Dropped `LN_IC50` (collinear with AUC)
- **Final dataset:** 13,106 rows × 18 columns

### 3. Feature Selection
- Random Forest used for exploratory feature importance
- Dropped low-impact features: `GDSC Tissue descriptor 1`, `CNA`, `TCGA_DESC`
- Retained top contributors: `TARGET_PATHWAY`, `Z_SCORE`, `DRUG_NAME`, `DRUG_ID`, `TARGET`

### 4. Model Selection & Tuning
- **LazyPredict** benchmarked 42 regression models → XGBoost ranked #1
- **Grid Search** hyperparameter tuning:
  - `learning_rate`: 0.2
  - `max_depth`: 5
  - `n_estimators`: 300

### 5. Evaluation
- R² and RMSE on train/test splits
- Predicted vs Actual AUC scatter plot
- Residual distribution analysis (normally distributed, no systematic bias)

---

## Tech Stack

| Category | Tools |
|----------|-------|
| Language | Python |
| Data | Pandas, NumPy |
| ML | Scikit-Learn, XGBoost, LazyPredict |
| Preprocessing | KNNImputer, MinMaxScaler, LabelEncoder |
| Optimization | GridSearchCV |
| Visualization | Matplotlib, Seaborn, Plotly |
| Platform | Google Colab |

---

## Dataset

**GDSC (Genomics of Drug Sensitivity in Cancer)** — Yang et al., 2013  
~75,000 experiments across 138 drugs and ~700 cancer cell lines.  
Features include: AUC, Z_SCORE, gene expression, DNA methylation, CNA, MSI status, TARGET_PATHWAY.

---

## Resources

- 📓 [Colab Notebook](https://colab.research.google.com/drive/1y7UAyinGOr76unvVHTNowftvgls6dDIH?usp=sharing)
- 📄 Conference proposal: IEEE BIBM 2024 — *Deep Learning Approaches for Drug Sensitivity Prediction to Treat Breast Cancer*
