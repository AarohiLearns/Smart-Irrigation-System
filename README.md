# 🌱 Smart-Irrigation-System

A real-time crop water requirement prediction system built using FAO-56 Penman-Monteith physics equations and machine learning, desgined for deployment 
 on Raspberry Pi 5.

---

## 📌 Problem Statement

Farmers in India waste 30-40% of irrigation water due to guesswork. This system predicts the **exact amount of water** a crop needs daily using real-time sensor data — helping farmers irrigate precisely and save water.

---

## 🎯 What This System Predicts

| Task | Output |
|------|--------|
| Crop Water Requirement | 2.33 mm/day |
| Soil Fertility Score | 68 / 100 |
| Fertility Class | High / Medium / Low |
| Irrigation Decision | YES / NO |

---

---

## 📊 Dataset

- **Rows:** 8000
- **Columns:** 32
- **Source:** Physics-based generation using FAO-56, ICAR and USDA SCS standards
- **Coverage:** All seasons + all crop growth stages

---

## ⚙️ Tech Stack

```
Language:   Python
Libraries:  NumPy, Pandas, Matplotlib, Seaborn, Scikit-learn, Joblib
Platform:   Google Colab 


```

---

## 🧠 Machine Learning Pipeline

```
Raw Data
    ↓
EDA + Visualization
    ↓
Feature Engineering (32 → 38 features)
    ↓
Train / Test Split (80/20)
    ↓
StandardScaler (fit on train only)
    ↓
Model Training (23 models across 4 tasks)
    ↓
Evaluation (R², RMSE, MAE, MAPE, CV)
    ↓
Save .joblib files

```

---

## 📈 Results

### Task A — Crop Water Requirement (Regression)

| Model | R² | RMSE |
|-------|----|------|
| **Extra Trees** ✅ | **0.9980** | **0.079 mm/day** |
| Gradient Boosting | 0.9978 | 0.083 mm/day |
| Random Forest | 0.9956 | 0.091 mm/day |
| Ridge | 0.9579 | 0.142 mm/day |

**5-Fold CV R² = 0.9975 ± 0.0003**

### Task B — Fertility Score (Regression)
- Best model selected by Adjusted R²

### Task C — Fertility Classification
- Classes: High / Medium / Low
- Accuracy: 88%+

### Task D — Irrigation Decision
- Binary: YES / NO
- Accuracy: 88%+

---

## 🌾 Feature Engineering

Started with **32 raw features** → engineered to **38 model features**

New features added:
- `temp_range_C` — daily temperature variation
- `heat_stress` — penalty above 35°C
- `VPD_stress` — atmospheric dryness above 1 kPa
- `NPK_composite` — ICAR normalized soil health
- `pH_deviation` — distance from optimal 6.5
- `aridity_index` — rainfall / ETo ratio
- Cyclic encoding: `doy_sin`, `doy_cos`, `month_sin`, `month_cos`

---

## 🔬 FAO-56 Physics Pipeline (Computed on Pi)

```
Ra  → Extraterrestrial Radiation    (astronomy)
Rs  → Solar Radiation at Surface    (Angstrom formula)
Rn  → Net Radiation                 (energy balance)
es  → Saturation Vapor Pressure     (thermodynamics)
ea  → Actual Vapor Pressure         (humidity based)
VPD → Vapor Pressure Deficit        (atmospheric dryness)
ETo → Reference Evapotranspiration  (Penman-Monteith)
ETc → Crop Evapotranspiration       (ETo × Kc)
Ks  → Water Stress Coefficient      (soil moisture)
Pe  → Effective Rainfall            (USDA SCS)
CWR → Crop Water Requirement        (Ks × ETc - Pe)
```

---

## 📱 Farmer Output

```
💧 Irrigate: 2.33mm today
🌿 Fertility: 68/100 Medium
✅ IRRIGATE TODAY
⚠️ Add Nitrogen Fertilizer
Updated: 6:02 AM
```

Farmer receives daily push notification on **Blynk app** at 6AM automatically.

---

## 💰 Cost Analysis

| Item | Cost |
|------|------|
| Raspberry Pi 5 | ₹7,000 |
| NPK Sensor | ₹4,500 |
| All other sensors | ₹6,900 |
| **Total (one time)** | **₹18,400** |

vs Fasal (competitor): ₹15,000/season recurring
**Payback period: 1.2 seasons**

---

## 📁 Project Structure

```
Smart-Irrigation-ML/
│
├── Smart_Irrigation_ML_Code.ipynb   ← Main Colab notebook
├── Smart_Irrigation_FAO56_8000.csv  ← Dataset
└── README.md
```

---

## 📚 References

1. Allen et al. (1998) — FAO-56 Irrigation and Drainage Paper No. 56
2. ICAR Soil Health Card Methodology
3. USDA SCS Technical Release 21
4. Agricultural Census of India 2015-16

---

## 👨‍💻 Author

Made with ❤️ for Indian farmers
