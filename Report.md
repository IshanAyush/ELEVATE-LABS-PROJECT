#  Medical Appointment No-Show Prediction

This project analyzes over 110,000 medical appointment records in Brazil to predict whether a patient will show up for their scheduled appointment. The goal is to identify patterns in patient behavior and reduce the no-show rate, which causes inefficiencies in public health systems.

---

##  Dataset Overview

- **Source**: [Kaggle: No-show appointments](https://www.kaggle.com/datasets/joniarroba/noshowappointments)
- **Records**: 110,527 appointments
- **Target**: `No-show` (Yes → 1, No → 0)

---

##  Objectives

- Analyze patient behavior regarding appointment attendance.
- Identify key features contributing to no-shows.
- Build a machine learning model to predict appointment no-shows.
- Recommend improvements for patient notification and scheduling systems.

---

##  Data Preprocessing

- Removed duplicates and negative ages.
- Converted `ScheduledDay` and `AppointmentDay` to datetime.
- Engineered new features:
  - `WaitingDays` (time between scheduling and appointment)
  - `Total_Prior_Appointments`, `Total_Missed_Appointments` (patient history)
  - Age category bins (`AgeCategory`)
  - Day of the week (`DayOfWeek`)
- Categorical encoding and handling class imbalance using **SMOTE**.

---

##  Exploratory Data Analysis (EDA)

###  Gender
- Females had more appointments and more no-shows, but the **no-show rate was similar (~20%)** for both genders.

### ♻ Returning Patients
- Over **48,000 patients** had more than one appointment, enabling history-based features.

###  Age
- No-shows were highest in patients **aged 10–35** (Age Categories 1–4).

###  SMS Reminders
- Patients who received SMS reminders had a **higher no-show rate (38%)** than those who didn't (20%). SMS reminders may need reevaluation.

###  Neighbourhood
- No significant impact; most neighbourhoods have ~20% no-show rates.

###  Appointment Days
- Appointments mostly occurred early in the week.
- **Saturdays had the lowest no-show rate**, but sample size was too small to be conclusive.

###  Waiting Time
- Most appointments booked ~30 days in advance.
- **Longer waiting times → higher no-show rates**. Important predictive feature.

###  Chronic Conditions
- Patients with **Hypertension** attended more reliably.
- **Diabetes** did not show a strong effect.
- Patients with **multiple disabilities** (especially 4) had the **highest no-show rate**.

###  Scholarship
- Patients with **government subsidies** were **slightly more likely to miss** their appointments.

---

##  Feature Engineering

Key model features include:
- `Age`, `Gender`, `Scholarship`, `Hipertension`, `Diabetes`, `Alcoholism`, `Handcap`
- `WaitingDays`, `DayOfWeek`, `SMS_received`
- `Total_Prior_Appointments`, `Total_Missed_Appointments`

---

##  Handling Class Imbalance

- **SMOTE** (Synthetic Minority Over-sampling) was applied to balance the dataset, as only ~20% of records were no-shows.

---

##  Model Training

- **Model**: Random Forest Classifier
- **Parameters**: `n_estimators=100`, `class_weight='balanced'`
- **Train-Test Split**: 80/20 after balancing

---

##  Evaluation Metrics

| Metric                  | Value   |
|-------------------------|---------|
| **Accuracy**            | ~82%    |
| **ROC AUC Score**       | ~0.89   |
| **Precision-Recall AUC**| ~0.84   |

The model performs well in distinguishing between show and no-show cases.

---

##  Feature Importance (Top)

1. `Total_Prior_Appointments`
2. `WaitingDays`
3. `Age`
4. `Total_Missed_Appointments`
5. `DayOfWeek`
6. `Scholarship`
7. `Hypertension`
8. `SMS_received`
9. `Gender`
10. `Alcoholism`

---

##  Conclusions

- **Younger patients (10–35)** are more likely to miss appointments.
- **Longer waiting times** increase the chance of no-shows.
- **SMS reminders may not be working effectively**.
- **Chronic illnesses, scholarships, and disabilities** have moderate impact.
- Hospitals should **optimize reminders**, enable **flexible rescheduling**, and consider **overbooking** for high-risk slots.

---

##  Tools & Libraries

- **Python**
- **Pandas**, **NumPy**
- **Matplotlib**, **Seaborn**
- **Scikit-learn**, **Imbalanced-learn**
- **Random Forest Classifier**, **SMOTE**

---

## 📎 Future Work

- Try other classification models (e.g., XGBoost, LightGBM)
- Build a real-time no-show risk dashboard
- Integrate hospital policy simulation for testing interventions

---


