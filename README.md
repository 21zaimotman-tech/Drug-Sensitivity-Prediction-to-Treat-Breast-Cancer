# 🔬 Breast Cancer Drug Sensitivity Prediction

## 📌 Problem Statement
The effectiveness of cancer treatment varies significantly between patients due to the genetic diversity of tumors. 
In clinical research, **AUC (Area Under the Curve)** is a key metric used to measure drug sensitivity—a lower AUC indicates that the cancer cells are more sensitive to the treatment. 
The challenge is to accurately predict this sensitivity using a complex mix of features like gene expression, DNA methylation, and target pathways, allowing for more personalized and effective treatment strategies.

## 💡 Solution
This project develops a predictive machine learning pipeline that processes large-scale pharmacogenomic data (GDSC dataset) specifically for Breast Cancer (BRCA). 
By cleaning genomic features and applying advanced gradient boosting algorithms, the system can estimate the AUC score for a specific drug-cell line pair, helping identify which drugs are likely to be most effective against specific cancer profiles.

## 🛠️ Technologies Used
* **Language:** Python
* **Data Manipulation:** Pandas, NumPy
* **Visualization:** Seaborn, Matplotlib, Plotly
* **Machine Learning:** * Scikit-Learn (Preprocessing, KNNImputer, MinMaxScaler)
    * LazyPredict (Model Benchmarking)
    * **XGBoost** (Primary Regressor)
* **Optimization:** GridSearchCV for hyperparameter tuning

## 🧠 Key Challenges
* **Data Sparsity:** Managed missing genomic data using `KNNImputer` to maintain dataset integrity.
* **Feature Complexity:** Encoded high-cardinality categorical variables like `TARGET_PATHWAY`.
* **Feature Selection:** Analyzed feature importance to refine the model and focus on the most impactful biomarkers.

## 📈 Outcomes & Results
* **High Performance:** The optimized XGBoost model achieved a strong R^2 score (91%) and low RMSE on test data.
* **Biological Insights:** Identified key molecular pathways that serve as strong predictors for drug response.
* **Visual Validation:** Confirmed model reliability through residual analysis and "Predicted vs. Actual" sensitivity plots.
