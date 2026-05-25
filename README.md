#  Air Quality Index (AQI) Prediction System

> An advanced, end-to-end machine learning pipeline built to ingest complex multi-pollutant datasets and accurately categorize Air Quality Index (AQI) thresholds for real-time public safety advisories.

**Explore the Project:** [ Dataset Specs](#-dataset-specifications) • [ Preprocessing Pipeline](#-data-preprocessing-pipeline) • [ Feature Engineering](#-feature-engineering) • [ Model Performance](#-model-performance--evaluation) • [ Quick Start](#-getting-started--execution)

---

###  Tech Stack & Project Metrics
![](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![](https://img.shields.io/badge/Scikit--Learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![](https://img.shields.io/badge/Google_Colab-Ready-F9AB00?style=for-the-badge&logo=google-colab&logoColor=white)
![](https://img.shields.io/badge/Best_Accuracy-80.82%25-2ea44f?style=for-the-badge)
![](https://img.shields.io/badge/Data_Source-CPCB_India-blue?style=for-the-badge)
![](https://img.shields.io/badge/License-Academic_Use-red?style=for-the-badge)

---

##  Why This Project?

Air pollution is a critical public health crisis globally and within major urban hubs in Pakistan. Every winter, cities like Lahore face severe, hazardous smog conditions that result in critically reduced visibility and widespread respiratory illnesses. 

* **Proactive Interventions:** Traditional monitoring flags pollution *after* it happens. This system builds the predictive engine needed for preemptive public alerts.
* **Granular Multi-Pollutant Processing:** Analyzes complex interactions between `PM2.5`, `PM10`, `NOx`, `CO`, `SO2`, and `O3`.
* **Standardized Health Categorization:** Maps continuous sensor outputs into 6 globally recognized health risk categories: *Good, Satisfactory, Moderate, Poor, Very Poor, and Severe*.

---

##  Table of Contents
1. [Dataset Specifications](#-dataset-specifications)
2. [Data Preprocessing Pipeline](#-data-preprocessing-pipeline)
3. [Feature Engineering](#-feature-engineering)
4. [Model Performance & Evaluation](#-model-performance--evaluation)
5. [Real-World Simulation Scenarios](#-real-world-simulation-scenarios)
6. [Getting Started & Execution](#-getting-started--execution)
7. [Future Roadmap](#-future-roadmap)
8. [Team Signal Seekers](#-team-signal-seekers)

---

##  Dataset Specifications

| Attribute | Details |
| :--- | :--- |
| **Data Source** | Central Pollution Control Board (CPCB), India |
| **Temporal Coverage** | 2015 – 2020 (5 Years of Historical Tracking) |
| **Geographic Scope** | 26 Major Industrial/Urban Cities |
| **Raw Volume** | 29,531 records × 16 attributes |
| **Curated Volume** | 24,850 records (Post Data Cleansing) |

---

##  Data Preprocessing Pipeline

* **`STEP 1` Data Pruning:** Dropped completely redundant or highly sparse columns, such as `Xylene` which exhibited over **61% missing values**.
* **`STEP 2` Missing Value Imputation:** Handled structural data gaps across all remaining numeric pollutant metrics using robust **Median Imputation**.
* **`STEP 3` Class Balancing (SMOTE):** Addressed significant target class imbalances by applying Synthetic Minority Over-sampling Technique (SMOTE), normalizing the dataset to exactly **7,063 samples per class**.
* **`STEP 4` Feature Scaling:** Implemented `StandardScaler` to normalize variations, ensuring distance-sensitive baseline models converge optimally.

---

##  Feature Engineering

To capture contextual dependencies and enhance classifier variance, **10 new domain-specific features** were engineered:

| Feature Category | Formulation Strategy | Description |
| :--- | :--- | :--- |
| **Temporal Features** | Sine/Cosine Month Transformations | Captures cyclical and seasonal pollution patterns across years. |
| **Ratio Metrics** | `PM_Ratio = PM2.5 / PM10` | Isolates fine vs. coarse particulate matter distribution profiles. |
| **Interaction Dynamics** | `PM2.5 × CO` & `NOx × SO2` | Flags compounding hazards of concurrent pollutant spikes. |
| **Composite Indices** | `0.6×PM2.5 + 0.4×PM10` | Generates a single weighted environmental hazard baseline. |

---

##  Model Performance & Evaluation

The processed dataset was evaluated across multiple distinct architectural approaches:

| Classifier Model | Test Accuracy | F1-Score | Status |
| :--- | :---: | :---: | :---: |
|  **Random Forest** | **80.82%** | **0.8092** | 🔥 **Production Selected** |
|  **MLP Neural Network** | **76.68%** | **0.7692** | Candidate |
|  **Support Vector Machine (SVM)** | **74.65%** | **0.7527** | Candidate |
|  **Logistic Regression** | **71.93%** | **0.7264** | Baseline |

###  Feature Importance Ranking (Top 5 Drivers)
Our production-selected Random Forest model identified the following features as the strongest predictors for dangerous shifts in the AQI:
1. **PM2.5** (Importance Weight: `0.1463`)
2. **Composite_PM** (Importance Weight: `0.1398`)
3. **PM_CO_Interaction** (Importance Weight: `0.1320`)
4. **PM10** (Importance Weight: `0.0977`)
5. **CO** (Importance Weight: `0.0834`)

> ** Model Stability Verification:** Under comprehensive stress-testing (shuffling Random Seeds & altering Train-Test Split variations from 80/20 to 60/40), the Random Forest model demonstrated flawless consistency with a variance standard deviation of $\le 0.0003$.

---

##  Real-World Simulation Scenarios

| Environmental Context | Simulation Reference | Predicted System Output |
| :--- | :--- | :---: |
| **Pristine Environment** | Alpine Forest / Clean Mountain Air | 🟢 **Good** |
| **Average Microclimate** | Small / Mid-sized Residential Town | 🟡 **Satisfactory** |
| **Heavily Industrialized** | Megacity Industrial Hub / Delhi Winter | 🟣 **Very Poor** |
| **Extreme Climate Event** | Severe Seasonal Smog / Festival Fireworks | 🟤 **Severe** |

---

##  Getting Started & Execution

Follow these steps to run the training and inference pipeline seamlessly inside Google Colab:

1. **Launch Environment:** Open [Google Colab](https://colab.research.google.com/).
2. **Import Assets:** Upload the `Signal_Seekers_Dileverable_2.ipynb` notebook.
3. **Initialize Cells:** Execute cells sequentially up to the `# Load Dataset` block.
4. **Upload Data:** When prompted by Colab's interactive file-picker widget, upload your local copy of `city_day.csv`.
5. **Run Inference:** Execute the remaining cells to generate visualization reports and metrics.

> **Note:** This pipeline is structured to run entirely out-of-the-box. Core environment frameworks (`pandas`, `scikit-learn`, `imbalanced-learn`, `seaborn`) are fully natively pre-loaded into the Google Colab runtime ecosystem.

---

##  Future Roadmap

- [ ] **Meteorological Ingestion:** Integrate live weather variables (Humidity, Wind Velocity, Temperature).
- [ ] **Automated Optimization:** Implement `GridSearchCV` hyperparameter tuning sweeps.
- [ ] **API & UI Deployment:** Package the backend into a FastAPI interface with a Streamlit dashboard.
- [ ] **Regional Adaptation:** Fine-tune pre-trained weights against native data from Pakistani hubs (Lahore, Karachi, Islamabad).
- [ ] **Sequential Forecasting:** Transition architectures toward recurrent neural models (`LSTM` / `GRU`).

---

##  Team Signal Seekers

* **Muhammad Abdullah Ismail**
* **Muhammad Sufian Zahid**
* **Mahira Ali**
* **Kinza Chaudhry**

---

##  License

This repository is maintained for academic and research evaluation purposes. If utilizing this source code, pipeline configurations, or engineered feature schemas, kindly provide formal attribution citations.
