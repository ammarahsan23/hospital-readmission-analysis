# 🏥 Hospital Patient Readmission Analysis

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python) ![Tableau](https://img.shields.io/badge/Tableau-Dashboard-orange?logo=tableau) ![sklearn](https://img.shields.io/badge/scikit--learn-ML-green?logo=scikit-learn) ![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

An end-to-end data analytics project analyzing 30-day hospital readmission risk factors using 101,766 patient records from the UCI Diabetes 130-US Hospitals dataset. The project covers data cleaning, exploratory data analysis, logistic regression modeling, and an interactive Tableau dashboard.

---

## 📊 Dashboard Preview

> Built in Tableau — 4 interactive charts showing readmission patterns across age groups, hospital stay duration, prior inpatient visits, and top risk factors.

---

## 🎯 Project Objectives

- Identify key risk factors driving 30-day hospital readmission in diabetic patients
- Build a logistic regression model to predict high-risk patients
- Visualize findings in an interactive Tableau dashboard for stakeholder reporting
- Deliver actionable recommendations to reduce readmission rates

---

## 📁 Project Structure

```
hospital-readmission-analysis/
│
├── data/
│   ├── raw/                        # Original diabetic_data.csv
│   └── processed/                  # cleaned_diabetes_data.csv
│
├── notebooks/
│   └── 01_EDA_and_Modeling.ipynb   # Full analysis notebook
│
├── visuals/
│   ├── readmission_eda_charts.png  # EDA visualizations
│   ├── correlation_heatmap.png     # Feature correlation heatmap
│   ├── confusion_matrix.png        # Model evaluation
│   └── feature_importance.png      # Top risk factors chart
│
├── dashboard/
│   └── Hospital_Readmission_Dashboard.twb   # Tableau workbook
│
└── README.md
```

---

## 🗃️ Dataset

| Property | Details |
|---|---|
| Source | [UCI ML Repository — Diabetes 130-US Hospitals](https://www.kaggle.com/datasets/brandao/diabetes) |
| Records | 101,766 patient encounters |
| Features | 50 columns (demographics, diagnoses, medications, visit history) |
| Target | `readmitted` — whether patient was readmitted within 30 days |
| Time Period | 1999–2008, 130 US hospitals |

---

## 🔧 Tools & Technologies

| Category | Tools |
|---|---|
| Language | Python 3.11 |
| Data Manipulation | pandas, numpy |
| Visualization | matplotlib, seaborn |
| Machine Learning | scikit-learn (LogisticRegression, StandardScaler) |
| NLP/Encoding | LabelEncoder |
| BI Dashboard | Tableau Desktop / Tableau Public |
| Environment | Google Colab / VS Code |

---

## 🧹 Data Cleaning

- Replaced `?` placeholders with `NaN` across all columns
- Dropped high-missing columns: `weight` (96.9%), `max_glu_serum` (94.8%), `A1Cresult` (83.3%), `medical_specialty` (49.1%), `payer_code` (39.6%)
- Filled remaining missing values in `race` (mode) and `diag_1/2/3` ('Unknown')
- Converted `age` bracket strings (e.g. `[30-40)`) to numeric midpoints
- Removed non-feature ID columns: `encounter_id`, `patient_nbr`
- Created binary target: `readmitted_binary` — 1 if readmitted `<30` days, else 0

**Final cleaned dataset: 101,766 rows × 44 columns, 0 missing values**

---

## 📈 Key Findings

### Readmission Distribution
- **54%** of patients were not readmitted
- **35%** were readmitted after 30 days
- **11%** were readmitted within 30 days (high-risk group)

### Top Risk Factors (Logistic Regression Coefficients)
| Rank | Feature | Coefficient | Insight |
|---|---|---|---|
| 1 | `number_inpatient` | 0.366 | Prior hospital stays are the strongest predictor |
| 2 | `discharge_disposition_id` | 0.136 | Discharge destination significantly affects risk |
| 3 | `diabetesMed` | 0.097 | Patients on diabetes medication show higher risk |
| 4 | `number_diagnoses` | 0.084 | More diagnoses = more complex cases |
| 5 | `number_emergency` | 0.063 | Prior emergency visits indicate instability |

### Readmission by Age
- Patients aged **25 had the highest readmission rate (14.2%)** — suggesting poor chronic disease management in young adults
- Risk rises again for patients **75–85 years (11.8–12.1%)** — expected in elderly populations

### Readmission by Prior Inpatient Visits
- **0 prior visits → 8.4% readmission rate**
- **5 prior visits → 31.4% readmission rate**
- **8+ prior visits → 44%+ readmission rate**
- Clear linear relationship: each additional prior visit significantly increases risk

---

## 🤖 Model Performance

| Metric | Value |
|---|---|
| Algorithm | Logistic Regression |
| Train/Test Split | 80% / 20% |
| Class Imbalance Handling | `class_weight='balanced'` |
| ROC-AUC Score | **0.6464** |
| Recall (Readmitted <30) | **51%** |
| Precision (Readmitted <30) | 17% |

> **Note:** In healthcare settings, recall is prioritized over precision — it is better to flag more patients for follow-up than to miss high-risk cases. The model successfully identifies 51% of patients who will be readmitted within 30 days.

---

## 📊 Tableau Dashboard

The interactive dashboard contains 4 views:

1. **Readmission Rate by Age Group** — Bar chart showing readmission % across 10 age brackets
2. **Readmission Rate by Time in Hospital** — Line chart showing how stay duration correlates with readmission
3. **Top 10 Risk Factors** — Horizontal bar chart of logistic regression coefficients
4. **Readmission Rate by Prior Inpatient Visits** — Bar chart showing steep risk increase with visit history

---

## 🚀 How to Run

**1. Clone the repository**
```bash
git clone https://github.com/YOUR_USERNAME/hospital-readmission-analysis.git
cd hospital-readmission-analysis
```

**2. Install dependencies**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

**3. Download the dataset**
- Download `diabetic_data.csv` from [Kaggle](https://www.kaggle.com/datasets/brandao/diabetes)
- Place it in `data/raw/`

**4. Run the notebook**
```bash
jupyter notebook notebooks/01_EDA_and_Modeling.ipynb
```

**5. View the dashboard**
- Open `dashboard/Hospital_Readmission_Dashboard.twb` in Tableau Desktop
- Or view the published version on Tableau Public *(link here)*

---

## 💡 Business Recommendations

Based on the analysis, the following actions are recommended to reduce 30-day readmission rates:

1. **Flag high-risk patients before discharge** — patients with 3+ prior inpatient visits should receive mandatory follow-up scheduling
2. **Improve discharge planning** — discharge destination (`discharge_disposition_id`) is the 2nd strongest predictor; better post-discharge support programs are needed
3. **Target young adults aged 20–30** — this age group showed surprisingly high readmission rates (14.2%), suggesting gaps in chronic disease management education
4. **Prioritize patients on diabetes medication** — `diabetesMed` patients carry elevated readmission risk and may need more intensive outpatient monitoring

---

## 👤 Author

**Mohammad Ammar Ahsan**  
B.E. in Artificial Intelligence & Data Science  
Muffakham Jah College of Engineering and Technology, Hyderabad  

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://linkedin.com/in/ammar-ahsan-850205201)  
📧 ammarahsanmaa786@gmail.com | 📞 +91 94902 11907

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
