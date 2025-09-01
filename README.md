# Financial Fraud Analysis with KNIME

A comprehensive data mining and machine learning project built in **KNIME Analytics Platform** aimed at identifying and analyzing fraudulent transactions within the synthetic PaySim mobile money dataset.

[![KNIME](https://img.shields.io/badge/Built%20with-KNIME-%230278C0?style=flat&logo=knime)](https://www.knime.com/)

## 📖 Project Overview

This project implements an end-to-end data analysis workflow in KNIME to detect suspicious and fraudulent financial activities. The workflow encompasses data loading, exploratory data analysis (EDA), data preprocessing, feature engineering, and training multiple machine learning models. The goal is to evaluate the effectiveness of different models within the KNIME ecosystem for the task of financial anomaly detection.

---

## 📊 Dataset

**Name:** Synthetic Financial Datasets For Fraud Detection
**Source:** Available on [Kaggle](https://www.kaggle.com/datasets/ealaxi/paysim1).

**Description:** A realistic synthetic dataset simulating mobile money transactions, designed for fraud detection research.

**Size:** 6,362,620 transactions

**Key Features:** `step`, `type`, `amount`, `nameOrig`, `oldbalanceOrg`, `newbalanceOrig`, `nameDest`, `oldbalanceDest`, `newbalanceDest`, `isFraud`, `isFlaggedFraud`.

## 🧩 KNIME Workflow Overview

The main workflow (`project.knwf`) is structured into several key sections:

1.  **Data Input & Exploration:** Using a **File Reader** node to load the data, followed by **Rule Engine**, **Statistics**, and **Bar Chart** nodes to understand data distribution, missing values, and the concentration of fraud.
2.  **Data Preprocessing:** Filtering data (using a **Row Filter**) to focus only on `TRANSFER` and `CASH_OUT` transactions. Creating a new feature `hour_of_day` from the `step` column using a **Math Formula** node.
3.  **Model Training & Validation:** The workflow splits into parallel branches for different models:
    *   **K-Means Clustering:** Using the **k-Means** node for unsupervised learning.
    *   **Supervised Models:** Using the **Partitioning** node to split data and various learner/predictor nodes:
        *   **Decision Tree**
        *   **Naïve Bayes**
        *   **Random Forest**
    *   Model evaluation is performed using **Cross-Validation** meta-nodes and scored using **Scorer** and **Numeric Scorer** nodes to calculate accuracy, precision, recall, and F1-score.
4.  **Results Visualization:** Using **ROC Curve**, **Scatter Plot**, and **View** nodes to visualize model performance and analysis results.

## 🎯 Key Insights from EDA

*   Fraud is **exclusively** present in **TRANSFER** and **CASH_OUT** transaction types.
*   Extreme **class imbalance**: Only 8,213 fraudulent transactions out of 6+ million.
*   No direct correlation was found between `amount`, time of day (`step`), or specific users and fraudulent activity.

---

## 📈 Results & Performance

The performance of all implemented models is summarized in the table below. The key metrics are **Error Count** and **Accuracy**, with a detailed breakdown of prediction types (True/False Positives/Negatives).

| Model | Error Count | True Positive | True Negative | False Positive | False Negative | Accuracy |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| k-Means Clustering | 1,364,345 | 5,469 | 1,400,595 | 1,361,601 | 2,744 | 50.75% |
| Naïve Bayes | 1,642 | 0 | 2,762,196 | 0 | 8,213 | 99.70% |
| Decision Tree (Outliers Removed) | **865** | 232 | 2,521,287 | 168 | 4,160 | **99.82%** |
| Decision Tree (Outliers Not Removed) | 1,345 | 1,899 | 2,761,784 | 412 | 6,314 | 99.75% |
| Random Forest (Outliers Removed) | 876 | 10 | 2,521,454 | 1 | 4,382 | 99.82% |
| Random Forest (Outliers Not Removed) | 1,411 | 1,226 | 2,762,125 | 71 | 6,987 | 99.74% |

---

## ⚠️ Challenges & Limitations

1.  **Class Imbalance:** The extreme rarity of fraud cases leads to models biased towards the majority class.
2.  **Pattern Repetition:** Artificial patterns in the data can cause overfitting.
3.  **Limited Feature Set:** Lack of user historical data limits behavioral analysis.

---

## 🧑‍🎓 Author

**Fatemeh Mousavi**  
Student at IUT  
Course: Data Mining  
Semester: Spring 2024-2025
