# Air Quality Index (AQI) Prediction System

A machine learning system that predicts Air Quality Index (AQI) categories from pollutant measurements, enabling real-time air quality monitoring and public health advisories.

---

## **Project Overview**

Air pollution is a serious health concern in major cities across Pakistan and the world. Every winter, Lahore experiences severe smog, causing reduced visibility and respiratory illnesses. This project builds a machine learning pipeline that predicts AQI categories from pollutant measurements to enable proactive health advisories.

| **Aspect** | **Description** |
|------------|-----------------|
| Input | PM2.5, PM10, NOx, CO, SO2, O3, and other pollutant measurements |
| Output | 6 AQI categories — Good, Satisfactory, Moderate, Poor, Very Poor, Severe |

---

## **Dataset**

| **Attribute** | **Details** |
|---------------|--------------|
| Source | Central Pollution Control Board (CPCB), India |
| Time Period | 2015 – 2020 (5 years) |
| Cities | 26 Indian cities |
| Original Records | 29,531 rows × 16 columns |
| Final Records | 24,850 rows (after cleaning) |

---

## **Models Implemented**

| **Model** | **Accuracy** | **F1 Score** |
|-----------|--------------|---------------|
| Random Forest (Best) | 80.82% | 0.8092 |
| MLP Neural Network | 76.68% | 0.7692 |
| SVM | 74.65% | 0.7527 |
| Logistic Regression (Baseline) | 71.93% | 0.7264 |

---

## **Feature Engineering**

To improve model performance, we created 10 new features:

| **Feature Type** | **Description** |
|------------------|-----------------|
| **Temporal Features** | Month indicators with sine/cosine transformations (captures seasonal patterns) |
| **Ratio Features** | PM_Ratio = PM2.5/PM10 — indicates particulate composition; NOx_NO2_Ratio — nitrogen oxide composition |
| **Interaction Features** | PM_CO_Interaction = PM2.5 × CO; NOx_SO2_Interaction = NOx × SO2 |
| **Composite Indices** | Composite_PM = 0.6×PM2.5 + 0.4×PM10; Composite_NOx — weighted nitrogen oxide index |

---

## **Data Preprocessing**

| **Step** | **Description** |
|----------|-----------------|
| 1 | Dropped redundant columns — Removed 'Xylene' (61% missing values) |
| 2 | Handled missing values — Median imputation for all numeric columns |
| 3 | Class balancing — Applied SMOTE to address imbalance, resulting in 7,063 samples per class |
| 4 | Feature scaling — StandardScaler applied to normalize all features |

---

## **Key Findings**

### **Most Important Features (Random Forest)**

| **Rank** | **Feature** | **Importance** |
|----------|-------------|----------------|
| 1 | PM2.5 | 0.1463 |
| 2 | Composite_PM | 0.1398 |
| 3 | PM_CO_Interaction | 0.1320 |
| 4 | PM10 | 0.0977 |
| 5 | CO | 0.0834 |

### **Model Stability Experiments**

| **Experiment** | **Result** |
|----------------|------------|
| Random Seed Variation | All models showed consistent performance (std dev ≤ 0.0003) |
| Train-Test Split Variation | Random Forest maintained highest accuracy across 80-20, 70-30, and 60-40 splits |

---

## **Real-World Testing Scenarios**

| **Scenario** | **Predicted AQI** |
|--------------|-------------------|
| Clean Air (Mountain/Forest) | Good |
| Moderate Pollution (Small City) | Satisfactory |
| High Pollution (Industrial/Delhi Winter) | Very Poor |
| Severe Pollution (Smog/Diwali) | Severe |

---

## **How to Run**

| **Step** | **Action** |
|----------|-------------|
| 1 | Open Google Colab |
| 2 | Upload the notebook file |
| 3 | Run the first 2 cells (until `# Load Dataset`) |
| 4 | Upload `city_day.csv` when prompted |
| 5 | Run the remaining cells to see results |

> **Note:** All core ML libraries (pandas, scikit-learn, seaborn, etc.) are pre-installed in Google Colab — no manual installation required.

---

## **Technologies Used**

| **Category** | **Tools / Libraries** |
|--------------|------------------------|
| Language | Python 3.8+ |
| Data Manipulation | pandas, NumPy |
| Machine Learning | scikit-learn |
| Class Balancing | imbalanced-learn (SMOTE) |
| Visualization | Matplotlib, Seaborn |

---

## **Team Signal Seekers**

- Muhammad Abdullah Ismail
- Muhammad Sufian Zahid
- Mahira Ali
- Kinza Chaudhry

---

## **Future Work**

- Incorporate weather/meteorological data
- Hyperparameter optimization with GridSearchCV
- Deploy as web API for public access
- Test on Pakistani cities (Lahore, Karachi, Islamabad)
- Experiment with LSTM/GRU for time-series forecasting

---

## **License**

This project is for academic purposes. Please cite appropriately if using the code or findings.
