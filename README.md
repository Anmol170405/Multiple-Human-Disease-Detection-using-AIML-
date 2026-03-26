# Eye-Opener SSRP · MFIL-Net + VRN

**Multi-Vital IoMT Diagnostic Framework for Early Disease Detection**

R&D Internship · Centre for Advanced Research Studies (CARS), Gujarat, India · Jun 2025 to Aug 2025

---

## Overview

Eye-Opener SSRP implements **MFIL-Net** (Multi-Feature IoMT Learning Network) combined with a **Vital Rule Network (VRN)**, a hybrid neuro-symbolic architecture that fuses WHO/AHA/ADA clinical rule logic with supervised ML to detect health anomalies from continuous IoMT sensor streams across 12 patients and 1,762 records.

The system covers the full ML lifecycle: raw sensor data ingestion, clinically-grounded threshold labelling, group-aware model training with no patient leakage, six-algorithm benchmarking, SHAP explainability, and per-patient evaluation.

---

## Results at a Glance

| | Metric | Value |
|--|--------|-------|
| 🎯 | ROC-AUC (Random Forest) | **95.3%** |
| ✅ | Precision (combined system) | **100%** (zero false positives) |
| 📊 | F1-Score (combined system) | **82.7%** |
| 🗃️ | Total records evaluated | **1,762** across 12 patients |
| 🏥 | Patients processed | **12** |
| 🤖 | Algorithms benchmarked | **6** |

---

## Model Benchmarking

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|-------|----------|-----------|--------|----|---------|
| 🏆 **Random Forest** | 85.0% | 99.6% | 77.3% | 87.1% | **95.3%** |
| Decision Tree | 99.7% | 99.7% | 100.0% | 99.8% | 98.6% |
| SVM | 90.4% | 90.3% | 100.0% | 94.9% | 96.2% |
| Neural Network (MLP) | 89.0% | 90.1% | 98.0% | 93.0% | 94.5% |
| Logistic Regression | 89.8% | 90.3% | 99.4% | 94.6% | 91.7% |
| XGBoost | 91.2% | 100.0% | 83.1% | 90.7% | 93.8% |

> Random Forest selected as the final model. Best ROC-AUC with the most clinically meaningful precision/recall trade-off under group-aware evaluation (unseen patients only).

---

## Per-Patient Results

| Patient | Samples | F1 | ROC-AUC | Condition Detected |
|---------|---------|----|---------|-------------------|
| Patient 12 | 418 | 99.6% | 99.6% | 🫁 Severe Hypoxia |
| Patient 10 | 209 | 97.0% | 97.1% | 🫁 Severe Hypoxia |
| Patient 8 | 72 | 87.6% | 89.0% | 💉 Hypotension + Tachycardia |
| Patient 9 | 177 | 85.8% | 87.6% | 🌡️ Fever / Infection |
| Patient 4 | 52 | 80.6% | 83.7% | 🫀 Bradycardia |
| Patient 7 | 247 | 76.0% | 80.7% | 🫀 Tachycardia |
| Patient 5 | 49 | 68.8% | 76.2% | 💉 Hypotension |
| Patient 11 | 130 | 57.4% | 70.1% | 💉 Hypotension |
| Patient 3 | 196 | 52.3% | 67.7% | 💉 Hypotension |
| Patient 6 | 83 | 51.5% | 67.4% | 💉 Hypotension |
| Patient 2 | 71 | 49.4% | 66.4% | 💉 Hypotension |
| Patient 1 | 58 | 37.0% | 61.4% | 💉 Hypotension |

---

## Architecture

```
🗂️  Raw IoMT Sensor Data (Excel per patient)
          |
          v
🧠  VRN · Vital Rule Network
    WHO / AHA / ADA clinical thresholds
    Severity scoring 1-5 per reading
          |
          v
⚙️  Feature Engineering + Labelling
    Respiratory flag derivation, NaN handling
          |
          v
✂️  GroupShuffleSplit  (no patient leakage)
          |
          v
🤖  6-Algorithm Benchmark + SHAP Explainability
          |
          v
📈  Per-Patient Evaluation + Condition Tagging
```

---

## Clinical Thresholds (VRN)

| Vital | Normal Range | Conditions Flagged |
|-------|-------------|-------------------|
| ❤️ Heart Rate | 65 to 95 bpm | Tachycardia >95 · Bradycardia <65 |
| 🩺 Blood Pressure | 95 to 115 mmHg | Hypotension <95 · Hypertension >115 |
| 🌡️ Body Temperature | 36.3 to 37.1 °C | Hypothermia <36.3 · Fever >37.1 |
| 💨 SpO2 | 96% or above | Hypoxemia <96% · Severe Hypoxia <92% |

---

## Quick Start

```bash
# 1. Clone
git clone https://github.com/Anmol170405/eye-opener-ssrp
cd eye-opener-ssrp

# 2. Install
pip install pandas numpy scikit-learn xgboost tensorflow shap openpyxl matplotlib seaborn

# 3. Run
jupyter notebook Eye_Opener_SSRP.ipynb
```

Update the data path in Cell 0:

```python
file_path = r"./data/patient 1.xlsx"
```

---

## Project Structure

```
eye-opener-ssrp/
├── Eye_Opener_SSRP.ipynb               # Main research notebook
├── data/
│   ├── patient_1.xlsx                  # Raw IoMT sensor exports
│   └── labeled_outputs/                # VRN-annotated datasets
└── results/
    └── diagnostic_metrics_summary.xlsx # Full per-patient evaluation
```

---

## Stack

`Python` `Scikit-learn` `TensorFlow` `XGBoost` `SHAP` `Pandas` `NumPy` `Matplotlib` `Seaborn`

**Evaluation methods:** GroupShuffleSplit · LeaveOneGroupOut CV · SHAP TreeExplainer · ROC/AUC · Confusion Matrix · Severity Scoring (1 to 5)

---

## About

Built during the **Summer Student Research Programme (SSRP)** at the Centre for Advanced Research Studies (CARS), Gujarat, India. Clinical thresholds are grounded in WHO, AHA, ADA, and international medical guidelines.

**Anmol Rai** · CSE undergrad at Chandigarh University · [LinkedIn](https://linkedin.com/in/anmolrai05) · rai679531@gmail.com
