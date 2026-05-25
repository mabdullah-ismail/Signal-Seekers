# 🌬️ Air Quality Index (AQI) Prediction System

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg?style=flat-square&logo=python)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/Machine%20Learning-Scikit--Learn-orange.svg?style=flat-square&logo=scikit-learn)](https://scikit-learn.org/)
[![Google Colab](https://img.shields.io/badge/Google%20Colab-Ready-yellow.svg?style=flat-square&logo=google-colab)](https://colab.research.google.com/)
[![License](https://img.shields.io/badge/License-Academic%20Use-green.svg?style=flat-square)](#-license)

A robust machine learning pipeline designed to predict Air Quality Index (AQI) categories from complex pollutant measurements. This system enables real-time air quality monitoring and predictive health advisories to combat hazardous seasonal smog.

---

## 📌 Project Overview

Air pollution is a critical public health crisis globally and within major urban hubs in Pakistan. Every winter, cities like Lahore face severe, hazardous smog conditions that result in critically reduced visibility and widespread respiratory illnesses. 

This project establishes an end-to-end machine learning pipeline that accurately categorizes AQI levels based on various pollutant metrics, providing the foundational engine needed for proactive health alerts and municipal policy interventions.

### 🔄 System Architecture at a Glance

* **Inputs:** Multi-pollutant concentrations (`PM2.5`, `PM10`, `NOx`, `CO`, `SO2`, `O3`, etc.)
* **Outputs:** 6 Standardized AQI Classification Categories:
  * 🟢 **Good**
  * 🟡 **Satisfactory**
  * 🟠 **Moderate**
  * 🔴 **Poor**
  * 🟣 **Very Poor**
  * 🟤 **Severe**

---

## 📊 Dataset Specifications

| Attribute | Details |
| :--- | :--- |
| **Data Source** | Central Pollution Control Board (CPCB), India |
| **Temporal Coverage** | 2015 – 2020 (5 Years of Historical Data) |
| **Geographic Scope** | 26 Major Indian Cities |
| **Raw Dataset Volume** | 29,531 records × 16 attributes |
| **Curated Dataset Volume** | 24,850 records (Post Data Cleansing) |

---

## 🛠️ Data Preprocessing Pipeline

1. **Feature Pruning:** Dropped completely redundant or highly sparse attributes, such as `Xylene` (which exhibited over 61% missing values).
2. **Missing Value Imputation:** Handled structural data gaps across all remaining numeric columns using stable **Median Imputation**.
3. **Class Balancing (SMOTE):** Addressed significant target class imbalances by applying Synthetic Minority Over-sampling Technique (SMOTE), successfully normalizing the dataset to **7,063 samples per class**.
4. **Feature Scaling:** Implemented `StandardScaler` to transform and normalize feature distributions for variance-sensitive models.

---

## 🧪 Feature Engineering

To capture contextual dependencies and enhance overall classifier variance, **10 new domain-specific features** were engineered:

| Feature Category | Name / Formula | Description |
| :--- | :--- | :--- |
| **Temporal Features** | Sine/Cosine Month Transformations | Captures cyclical and seasonal pollution patterns across years. |
| **Ratio Metrics** | `PM_Ratio = PM2.5 / PM10` | Identifies particulate matter composition profiles. |
| **Ratio Metrics** | `NOx_NO2_Ratio` | Evaluates localized nitrogen oxide compound balance. |
| **Interaction Dynamics** | `PM2.5 × CO` & `NOx × SO2` | Flags compounding effects of multiple severe pollutants. |
| **Composite Indices** | `0.6×PM2.5 + 0.4×PM10` | Generates weighted environmental hazard baselines. |

---

## 📈 Model Performance & Evaluation

The processed data was trained across multiple baseline and advanced classifiers. The models achieved the following performance metrics:

| Classifier Model | Test Accuracy | F1-Score | Status |
| :--- | :---: | :---: | :---: |
| 🏆 **Random Forest** | **80.82%** | **0.8092** | **Selected Model** |
| 🧠 MLP Neural Network | 76.68% | 0.7692 | Candidate |
| 🎛️ Support Vector Machine (SVM) | 74.65% | 0.7527 | Candidate |
| 📉 Logistic Regression | 71.93% | 0.7264 | Baseline |

### 🔥 Key Insights & Feature Importance (Random Forest)
The top 5 most critical features driving the predictive accuracy of our best model include:
1. **PM2.5** (Importance: `0.1463`)
2. **Composite_PM** (Importance: `0.1398`)
3. **PM_CO_Interaction** (Importance: `0.1320`)
4. **PM10** (Importance: `0.0977`)
5. **CO** (Importance: `0.0834`)

> **Model Stability:** Under comprehensive stress-testing (Random Seed & Train-Test Split variations ranging from 80-20 to 60-40), the Random Forest model demonstrated exceptional stability with a standard deviation performance variance of $\le 0.0003$.

---

## 🔮 Real-World Simulation Scenarios

| Tested Scenario Context | Real-world Equivalent | Predicted Output Category |
| :--- | :--- | :---: |
| Pristine Environment | Alpine Forest / Clean Mountain Air | 🟢 **Good** |
| Average Microclimate | Small/Mid-sized Residential Town | 🟡 **Satisfactory** |
| Heavily Industrialized Zone | Megacity Industrial Hub / Delhi Winter | 🟣 **Very Poor** |
| Extreme Environmental Event | Severe Winter Smog Event / Diwali Festival | 🟤 **Severe** |

---

## 🚀 Getting Started & Execution

Follow these steps to run the pipeline seamlessly via Google Colab without manual setup:

1. **Launch Environment:** Open [Google Colab](https://colab.research.google.com/).
2. **Import Notebook:** Upload the provided `.ipynb` project notebook file.
3. **Initialize Pipeline:** Run the initial codebase cells sequentially up to the `# Load Dataset` block.
4. **Data Injection:** When prompted by the interactive file picker widget, upload your local copy of `city_day.csv`.
5. **Generate Insights:** Execute all remaining cells to reproduce model evaluations, training charts, and performance logs.

> 💡 **Note:** This project is designed to run completely out-of-the-box in Google Colab. All dependent frameworks (`pandas`, `scikit-learn`, `seaborn`, `imbalanced-learn`) are fully pre-installed in the Colab runtime environment.

---

## 🧰 Tech Stack Summary

- **Core Language:** `Python 3.8+`
- **Data Wrangling:** `Pandas`, `NumPy`
- **Machine Learning Suite:** `Scikit-Learn`
- **Imbalance Mitigation:** `Imbalanced-Learn (SMOTE)`
- **Data Visualization:** `Matplotlib`, `Seaborn`

---

## 🔮 Future Roadmaps

- [ ] Integrate real-time meteorological / weather patterns (Humidity, Wind Speed, Temperature).
- [ ] Implement hyperparameter optimization sweeps utilizing automated `GridSearchCV`.
- [ ] Construct and deploy an interactive Web UI API (Streamlit/FastAPI) for instant public queries.
- [ ] Fine-tune and evaluate the pre-trained weights specifically against major Pakistani metropolitan data (Lahore, Karachi, Islamabad).
- [ ] Transition pipeline tracking to Recurrent Neural Networks (`LSTM` / `GRU`) for advanced time-series forecasting.

---

## 👥 Meet Team Signal Seekers

* 🧑‍💻 **Muhammad Abdullah Ismail**
* 🧑‍💻 **Muhammad Sufian Zahid**
* 👩‍💻 **Mahira Ali**
* 👩‍💻 **Kinza Chaudhry**

---

## 📄 License

This repository is maintained for academic and research evaluation purposes. If using this source code, pipelines, or engineered feature schemas, kindly provide formal attribution citations back to this repository.
