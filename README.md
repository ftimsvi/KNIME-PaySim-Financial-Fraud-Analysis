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
