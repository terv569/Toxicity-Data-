Here's a comprehensive README file for your toxicity classification notebook:

# 🧪 Molecular Toxicity Prediction Using Machine Learning

## 📋 Project Overview

This project implements a comprehensive machine learning pipeline to predict the toxicity of chemical compounds based on molecular descriptors. The dataset contains 171 chemical compounds characterized by 1204 molecular descriptors, with the goal of classifying compounds as **Toxic** or **NonToxic**.

The notebook demonstrates a complete data science workflow including:
- Exploratory Data Analysis (EDA)
- Feature analysis and selection
- Handling class imbalance
- Multiple ML model implementations
- Model comparison and evaluation

## 📊 Dataset Description

- **Samples**: 171 chemical compounds
- **Features**: 1204 molecular descriptors (numerical)
- **Target Variable**: Class (Toxic/NonToxic)
- **Class Distribution**: 
  - NonToxic: 115 samples (67%)
  - Toxic: 56 samples (33%)

The dataset exhibits significant class imbalance, requiring specialized techniques for reliable model performance.

## 🔍 Key Findings from Exploratory Data Analysis

### Top Features Correlated with Toxicity:
| Feature | Correlation | Description |
|---------|------------|-------------|
| EE_Dt | 0.215 | Estrada-like index |
| C2SP2 | 0.189 | Centered 2D autocorrelation |
| AATSC7p | 0.165 | Average centered autocorrelation |
| SpDiam_Dt | 0.165 | Spectral diameter |
| MLogP | 0.164 | Moriguchi octanol-water partition coefficient |

### Data Characteristics:
- High-dimensional data (1204 features vs 171 samples)
- Some features show significant outliers
- Complex correlation structure between descriptors
- Imbalanced target variable (67% NonToxic, 33% Toxic)

## 🛠️ Methodology

### 1. Data Preprocessing
- Target encoding (NonToxic→0, Toxic→1)
- Removal of constant features using VarianceThreshold
- Feature scaling for SVM models
- Stratified train-test split (80-20)

### 2. Class Imbalance Handling Techniques
The notebook implements multiple approaches:
- **SMOTE** (Synthetic Minority Over-sampling)
- **Random Undersampling**
- **SMOTE + Tomek Links** (hybrid approach)
- **Class weights** for cost-sensitive learning

### 3. Machine Learning Models Tested

#### Model 1: Random Forest with SMOTE
- **Pipeline**: SMOTE → Random Forest
- **Hyperparameter tuning**: n_estimators, max_depth, min_samples_split
- **Strengths**: Handles high-dimensional data well, provides feature importance

#### Model 2: XGBoost with Undersampling
- **Pipeline**: RandomUnderSampler → XGBoost
- **Hyperparameter tuning**: n_estimators, max_depth, learning_rate
- **Strengths**: Gradient boosting, handles non-linear relationships

#### Model 3: SVM with SMOTE + Tomek Links
- **Pipeline**: SMOTETomek → StandardScaler → SVM
- **Hyperparameter tuning**: C, gamma
- **Strengths**: Effective in high-dimensional spaces

## 📈 Results Comparison

| Model | Technique | Accuracy | Precision | Recall | F1 Score | Toxic Predictions |
|-------|-----------|----------|-----------|--------|----------|-------------------|
| Random Forest | SMOTE | 0.6571 | 0.3333 | 0.0909 | **0.1429** | 3 |
| **XGBoost** | **Undersampling** | **0.7143** | **0.5385** | **0.6364** | **0.5833** | **13** |
| SVM | SMOTE+Tomek | 0.3429 | 0.3235 | 1.0000 | 0.4889 | 34 |

### Best Model: XGBoost with Undersampling
- **F1 Score**: 0.5833 (best balance)
- **Recall**: 0.6364 (detects 64% of toxic compounds)
- **Precision**: 0.5385 (54% of toxic predictions are correct)
- **Accuracy**: 71.43%

## 🔬 Key Insights

1. **Class Imbalance Challenge**: The dataset's imbalance significantly impacts model performance, with many models struggling to detect toxic compounds.

2. **Feature Importance**: Molecular descriptors related to autocorrelation (C2SP2, AATSC7p) and lipophilicity (MLogP) show strong correlation with toxicity.

3. **Model Trade-offs**:
   - **High Recall** (SVM): Detects all toxic compounds but with many false positives
   - **Balanced Performance** (XGBoost): Best trade-off between precision and recall
   - **Conservative Predictions** (Random Forest): Few toxic predictions, low recall

## 🚀 Recommendations for Improvement

### Immediate Actions
1. **Feature Selection**: Reduce dimensionality from 1204 to top 20-50 features using:
   - Correlation-based filtering
   - Mutual information
   - Feature importance from tree-based models

2. **Advanced Ensemble Methods**:
   - Balanced Random Forest
   - EasyEnsemble classifier
   - XGBoost with optimized scale_pos_weight

3. **Data Collection**: Gather more toxic compound samples to improve minority class representation

### Advanced Approaches to Consider
1. **Molecular Fingerprints**: Replace descriptors with structural fingerprints
2. **Deep Learning**: Implement graph neural networks for molecular structure
3. **Anomaly Detection**: Treat toxic compounds as anomalies
4. **Transfer Learning**: Leverage pre-trained chemical property predictors

## 💻 Requirements

```
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
imbalanced-learn
tqdm
```

## 📁 Repository Structure

```
├── Toxicity report.ipynb    # Main notebook with complete analysis
├── README.md                # This file
└── data.csv                 # Input dataset (molecular descriptors)
```

## 📊 Visualizations Included

1. **Class Distribution**: Bar plot showing Toxic vs NonToxic counts
2. **Feature Distributions**: Histograms of top molecular descriptors
3. **Boxplots**: Outlier analysis and feature comparisons
4. **Correlation Heatmaps**: Feature-feature correlations
5. **PCA Visualization**: 2D projection of the data
6. **Confusion Matrices**: Model performance visualization
7. **Model Comparison Charts**: Side-by-side metric comparisons

## 📝 Usage

1. Clone the repository
2. Install required dependencies
3. Run the Jupyter notebook sequentially
4. Modify model parameters as needed
5. Use the best model for predictions on new compounds

## 🎯 Conclusion

The XGBoost model with undersampling provides the most balanced performance for toxic compound detection, achieving an F1 score of 0.5833. While there's room for improvement, this analysis establishes a solid foundation for toxicity prediction using molecular descriptors and provides clear direction for future enhancements.

The notebook serves as both a practical implementation and a template for similar cheminformatics classification problems, with comprehensive handling of common challenges like high dimensionality and class imbalance.

---

**Note**: This project is for research and educational purposes. Always validate predictions with experimental data for regulatory or safety-critical applications.
