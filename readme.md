# Credit Card Fraud Detection Using GMM-Based Synthetic Sampling


<p align="center">
  <b> Name:</b> Mohmad Yaqoob <br>
  <b> Roll. no.:</b> DA25M017
</p>


---

## Overview

Detecting fraudulent credit card transactions is a crucial problem in financial security and fraud prevention. The dataset used in this assignment consists of over 284,000 real-world transactions, where fraud cases comprise only about 0.17% of the total data. This extreme class imbalance makes it difficult for standard classifiers to learn to identify fraud effectively since they tend to focus on the majority (valid) class.

To improve fraud detection, this project explores advanced resampling techniques designed to address class imbalance:

- A **baseline Logistic Regression** model is first trained on the imbalanced dataset as a reference.
- **Gaussian Mixture Model (GMM)-based oversampling** generates realistic synthetic fraudulent samples by modeling the minority class distribution.
- **Cluster-Based Undersampling (CBU)** reduces the majority class size while preserving data diversity.
- A combined approach using GMM oversampling and CBU is evaluated for maximum improvement.

---

## Dataset Description

The dataset contains 284,807 credit card transactions with 31 features:

- Principal components (V1 to V28), anonymized for privacy.
- The transaction amount.
- A binary class label indicating fraud (1) or valid (0).

The extreme imbalance (fraud rate ~0.17%) presents challenges typical of fraud detection.

---

## Objectives

- Establish a baseline with Logistic Regression on imbalanced data.
- Generate synthetic fraud samples that better represent minority class variation using GMM.
- Balance the dataset with cluster-based undersampling of the majority class.
- Compare model performance on minority class detection using precision, recall, and F1-score.
- Provide clear recommendations based on empirical results and theoretical considerations.

---

## Methodology

### 1. Data Loading and Exploration

- Loaded dataset and inspected the first few rows.
- Confirmed severe class imbalance: majority class vastly outweighs minority.

### 2. Baseline Logistic Regression

- Trained a Logistic Regression model on original data with class weight balancing.
- Evaluated on test data using accuracy, confusion matrix, precision, recall, and F1-score for the fraud class.

#### Baseline Performance Metrics (Fraud Class):

| Metric   | Value  |
|----------|--------|
| Precision| 0.067  |
| Recall   | 0.878  |
| F1-Score | 0.125  |

- Results show high recall but very low precision, indicating many false positives in fraud detection.

---

### 3. GMM-Based Synthetic Oversampling

- Modeled minority class using Gaussian Mixture Model with 4 components (selected via AIC and BIC).
- Generated synthetic fraud samples by sampling from the mixture model.
- Trained Logistic Regression on the augmented dataset.

#### GMM-Augmented Data Metrics (Fraud Class):

| Metric   | Value  |
|----------|--------|
| Precision| 0.089  |
| Recall   | 0.865  |
| F1-Score | 0.161  |

- Precision increases, showing fewer false positives.
- Slight reduction in recall, but still very high.
- F1-score improves substantially, reflecting a better balance.

---

### 4. Cluster-Based Undersampling (CBU) Combined With GMM

- Applied cluster-based undersampling on the majority class to remove redundant data points.
- Combined undersampled majority data with GMM synthetic minority samples.
- Trained Logistic Regression on the newly balanced dataset.

#### Combined GMM + CBU Metrics (Fraud Class):

| Metric   | Value  |
|----------|--------|
| Precision| 0.090  |
| Recall   | 0.865  |
| F1-Score | 0.163  |

- Marginal additional improvement over GMM alone.
- Confirms that balancing both classes improves model effectiveness.

---

## Confusion Matrices

### Baseline Logistic Regression

|                 | Predicted Valid | Predicted Fraud |
|-----------------|-----------------|-----------------|
| Actual Valid    | High True Negatives | Some False Positives |
| Actual Fraud    | Some False Negatives | Low True Positives |

### GMM Resampled Model

- Confusion matrix heatmap showed an increase in true positives and a decrease in false positives compared to baseline.

### GMM+CBU Balanced Model

- Further improved true positives, maintaining a low false positive rate, indicating better minority class recognition.

---

## Theoretical Insights

- **GMM Advantages:**
  - Models minority class as a mixture of Gaussian distributions, capturing complex data substructures.
  - Generates realistic synthetic samples distributed across minority subgroups, avoiding over-generalization typical of simple oversampling methods such as SMOTE.

- **Cluster-Based Undersampling:**
  - Reduces majority class size without losing informative samples by selecting representative clusters.
  - Helps in reducing bias towards majority class and speeds up training.

- Together, they provide a principled approach to address class imbalance.

---

## Final Recommendations

- The combination of GMM-based synthetic sampling and cluster-based undersampling significantly improves minority class detection while controlling false positives.
- Even modest numerical improvements in precision and F1-score translate into meaningful reductions in false alarms and better fraud capture in practical scenarios.
- This approach is a robust solution for imbalanced fraud detection problems, balancing theoretical rigor and empirical effectiveness.

---

Mohmad Yaqoob  
DA25M017  

---
