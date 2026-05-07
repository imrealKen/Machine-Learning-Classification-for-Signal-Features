# Machine Learning Classification for Signal Features

## Project Overview
This repository provides a rigorous machine learning workflow for the identification and classification of specific substances (Rn and Xe) based on their physical signal features. By strictly analyzing raw signals and calibrating key physical characteristics (e.g., FWHM, Peak Position), we have eliminated systematic feature-engineering errors to ensure absolute data reliability.

The core notebook (`classfication.ipynb`) demonstrates the complete pipeline, spanning data cleaning, feature standardization, leakage-safe model training, and strict cross-validation. It is designed to provide highly reproducible and academically rigorous analytical evidence.

## Repository Structure & Data
- **`classfication.ipynb`**: The core Jupyter Notebook containing data preprocessing, hyperparameter optimization via `GridSearchCV`, and independent test set evaluation.
- **`副本用于机器学习(2).csv`**: The raw feature dataset. (Note: Depending on the manuscript's Data Availability statement, proprietary raw data may require reasonable requests to the corresponding author, or you can replace this with a public download link).

## Feature Space
To maintain physical relevance, the models are trained on the following seven continuous numerical features:

1. **Concentration**
2. **Max Intensity**
3. **Peak Pos**
4. **FWHM (Full Width at Half Maximum)**
5. **The width at the base of the peak**
6. **Peak Area**
7. **Skewness**

**Target Variable**:

- **Category**: Binary target label (`Rn` and `Xe`).

## Methodology & Rigor
To meet the stringent data analysis standards of high-impact peer review, this project employs a strictly leakage-safe strategy in its model design:

- **Isolated Test Set**: The dataset was divided into an 80% training set and a 20% independent test set using Stratified Random Splitting. The test set was strictly "frozen" and excluded from any feature fitting or hyperparameter tuning.

- **Pipeline Integration**: During the 5-Fold Stratified Cross-Validation, `sklearn.pipeline.Pipeline` was utilized to strictly bind feature standardization (`StandardScaler`) with the classification algorithms. This ensures that scaling parameters (mean and variance) are computed only on the training folds of each split, systematically preventing any implicit data leakage from the validation sets.

- **Robust Model Selection**: While tree-based models (e.g., Random Forest) can easily achieve perfect separation (Accuracy = 1.0) on experimental data—posing a risk of overfitting or capturing trivial boundaries—this study evaluates and emphasizes regularized models, specifically Logistic Regression (L1/L2) and Support Vector Machines (SVM, Linear/RBF). These models provide a more objective, realistic, and robust generalization baseline for physical feature differentiation.

## Dependencies
This code requires Python 3.8+ and the following core libraries:

- `pandas`
- `numpy`
- `scikit-learn`
- `matplotlib`
- `seaborn`

## Usage
1. Ensure the raw data file is named `副本用于机器学习(2).csv` and is placed in the same directory as the notebook.
2. Execute the cells in `classfication.ipynb` sequentially.

The pipeline will automatically:

- Strip invalid empty columns (e.g., Unnamed structural artifacts from CSV export)
- Print the feature dimensions
- Perform 5-fold cross-validation with grid search
- Output detailed evaluation metrics (Accuracy, Precision, Recall, and F1-score) on the independent test set

## Citation
This code constitutes the core machine learning analysis of our study. If you reference or utilize this workflow in your research, please refer to the "Data and Code Availability" section of our published manuscript and provide appropriate citation.
