
# Enhanced Synthetic NFHS + Framingham Dataset

## Overview
This dataset is a **synthetic health dataset** designed to simulate real-world Indian population health profiles, combining insights from:

- **NFHS-5 (National Family Health Survey - India)**: to reflect Indian-specific demographic and lifestyle diversity.
- **Framingham Heart Study**: to align with global cardiovascular disease (CVD) prediction standards.

The dataset contains:
- **10,000 synthetic individuals per state** across all 36 Indian states/UTs (360,000 rows total).
- Key health metrics relevant to cardiovascular and metabolic disease risk classification.
- A binary **`CVD_Risk` label**: `1` for likely CVD risk, `0` for likely metabolic or low-risk profile.
- A numeric **`FraminghamRisk`** score for 10-year CVD risk estimation (simplified proxy version).

---

## Features & Calculation Logic

| Column Name         | Description                                                                 | Generation Logic                                                                 |
|---------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| `State`             | Name of Indian state/UT                                                     | Randomly assigned among 36 states/UTs (excluding 'India')                        |
| `Age`               | Age in years (18-79)                                                        | Random integer: 18–79                                                            |
| `Gender`            | Biological sex                                                              | Random: Male ('M') or Female ('F')                                               |
| `BMI`               | Body Mass Index                                                             | Normally distributed: mean=24, std=4                                             |
| `SBP`               | Systolic Blood Pressure (mmHg)                                              | Normal(mean = 120 + 0.5*(age−40), std=10)                                        |
| `DBP`               | Diastolic Blood Pressure (mmHg)                                             | Normal(mean = 80 + 0.3*(age−40), std=8)                                          |
| `TotalCholesterol`  | Total serum cholesterol (mg/dL)                                             | Normal(mean=200, std=30)                                                         |
| `HDL`               | HDL cholesterol (mg/dL)                                                     | Normal(mean=50 (F) or 45 (M), std=10)                                            |
| `Glucose`           | Fasting glucose (mg/dL)                                                     | Normal(mean=90, std=15)                                                          |
| `Smoker`            | 1 = current smoker, 0 = non-smoker                                          | Binomial (p=0.3 M / 0.1 F)                                                       |
| `Diabetic`          | 1 = diabetic, 0 = non-diabetic                                              | Based on glucose >125 or BMI >27 + chance                                        |
| `AlcoholUse`        | 1 = drinks alcohol, 0 = non-drinker                                         | Binomial (p=0.25 M / 0.05 F)                                                     |
| `PhysicalActivity`  | Self-reported activity level                                                | Random choice: 'Low', 'Medium', 'High'                                          |
| `Diet`              | Vegetarian or Non-vegetarian                                                | Random choice: 'Veg' (60%), 'NonVeg' (40%)                                       |
| `Education`         | Highest education level                                                     | Random choice: 'Primary', 'Secondary', 'Tertiary'                                |
| `BMICategory`       | Category based on BMI                                                       | Based on WHO cutoffs                                                             |
| `PulsePressure`     | Difference between SBP and DBP                                              | `SBP - DBP`                                                                      |
| `FraminghamRisk`    | Simplified CVD risk score (proxy)                                           | `0.1*Age + 0.2*(SBP/120) + 0.1*(TotalChol/200) - 0.1*(HDL/50) + 5*Smoker + 5*Diabetic + 0.2*BMI` |
| `CVD_Risk`          | Target label: 1 = CVD likely, 0 = metabolic or low-risk                     | `1 if (SBP ≥ 140 or DBP ≥ 90 or Chol ≥ 240 or Smoker)`                          |

---

## Usage

This dataset is suitable for:
- ML modeling for binary classification (CVD risk)
- Risk scoring pipeline prototyping
- Feature selection experiments
- Healthcare-focused data science training

---

## Disclaimer
This dataset is **fully synthetic** and should **not** be used for clinical or diagnostic purposes. It is only for **research, prototyping, and modeling experiments**.

