# 🍔 Food Delivery Time Prediction

![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-ML-orange?logo=scikit-learn)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

> A machine learning project that predicts food delivery time (regression) and classifies delivery performance as Fast or Delayed (classification) using real-world features like distance, traffic, weather, and delivery person experience.

---

## 📌 Project Highlights

- ✅ Linear Regression to predict continuous delivery time (ETA estimation)
- ✅ Random Forest Classifier to classify delivery as Fast or Delayed
- ✅ Feature engineering with Haversine distance, Rush Hour flag, and Order Priority encoding
- ✅ Full EDA with boxplots, correlation analysis, and outlier detection

---

## 📁 Project Structure

```
food-delivery-time-prediction/
├── Food_Delivery_Time_Prediction.ipynb   # Main notebook
├── Food_Delivery_Time_Prediction.csv     # Dataset (200 records)
├── requirements.txt
└── README.md
```

---

## 🚀 Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/food-delivery-time-prediction.git
cd food-delivery-time-prediction

# 2. Install dependencies
pip install -r requirements.txt

# 3. Open and run the notebook
jupyter notebook Food_Delivery_Time_Prediction.ipynb
```

---

## 📊 Dataset

| Column | Type | Description |
|--------|------|-------------|
| `Distance` | float | Delivery distance (standardized) |
| `Weather_Conditions` | int | Encoded weather (0=Clear, 1=Fog, 2=Rain, 3=Storm) |
| `Traffic_Conditions` | int | Encoded traffic (0=Low, 1=Medium, 2=High) |
| `Delivery_Person_Experience` | int | Years of experience (1–10) |
| `Order_Priority` | int | Encoded priority (0=High, 1=Low, 2=Medium) |
| `Vehicle_Type` | int | Encoded vehicle (0=Bike, 1=Scooter, 2=Car) |
| `Restaurant_Rating` | float | Rating (2.5–5.0) |
| `Customer_Rating` | float | Rating (2.6–5.0) |
| `Delivery_Time` | float | Target — actual delivery time (standardized) |
| `Order_Cost` | float | Order cost (standardized) |
| `Tip_Amount` | float | Tip in rupees |

**Dataset size:** 200 rows × 15 columns | **No missing values**

---

## 🔧 Feature Engineering

Three new features were created:

| Feature | How Created |
|---------|-------------|
| `Distance_km` | Haversine formula from Customer & Restaurant GPS coordinates |
| `Rush_Hour` | 1 if order placed in Morning / Evening / Night |
| `Non_Rush_Hour` | 1 if order placed in Afternoon |

---

## 🧠 Model Pipeline

```
Step 1 → Data Import & Preprocessing
         - Label encode: Weather, Traffic, Vehicle Type, Order Priority
         - StandardScaler on: Distance, Delivery_Time, Order_Cost

Step 2 → EDA
         - describe(), var(), corr() with Delivery_Time
         - Boxplot + IQR outlier check → 0 outliers found

Step 3 → Feature Engineering
         - Haversine distance, get_dummies for Order_Time, Rush_Hour flag

Step 4 → Linear Regression (Regression Task)
         - Features: Distance, Traffic_Conditions, Order_Priority
         - Predict: Delivery_Time (continuous)

Step 5 → Random Forest Classifier (Classification Task)
         - Features: Traffic, Weather, Experience, Distance
         - Predict: Delivery_Status (Fast / Delayed)

Step 6 → Model Evaluation & Comparison
```

---

## 📈 Results

### Regression — Linear Regression (Predict Delivery Time)

| Metric | Value |
|--------|-------|
| R² Score | 0.016 |
| MAE | 0.852 |
| MSE | 1.028 |

> **Note:** Low R² indicates that Distance, Traffic, and Order Priority alone are weak predictors of delivery time in this dataset. Adding more features (e.g., actual Distance_km, Vehicle_Type, Experience) would likely improve results — a good next step.

---

### Classification — Random Forest (Fast vs Delayed)

| Metric | Value |
|--------|-------|
| Accuracy | 1.00 |
| Precision | 1.00 |
| Recall | 1.00 |
| F1-Score | 1.00 |

> **⚠️ Important Note:** The 100% accuracy occurs because the `Delivery_status` threshold (`<= 30 minutes`) was applied to StandardScaled data, which placed all 200 records into the "Fast" class — making this a single-class problem. In a production setting, the threshold must be applied **before** scaling, or on the original delivery time values. This is a known preprocessing order issue.

---

## 📉 Correlation with Delivery Time

| Feature | Correlation |
|---------|-------------|
| Distance | −0.075 |
| Restaurant_Rating | −0.092 |
| Traffic_Conditions | +0.040 |
| Vehicle_Type | −0.056 |

> Low correlations across all features suggest delivery time in this dataset may depend on non-linear interactions — a tree-based model (Random Forest Regressor) would be a better fit than Linear Regression.

---

## 🛠️ Requirements

```
pandas
numpy
scikit-learn
matplotlib
seaborn
haversine
```

Install with:
```bash
pip install -r requirements.txt
```

---

## 🔮 Future Improvements

- Apply threshold for Fast/Delayed classification on **original (unscaled)** delivery time values
- Use **Random Forest Regressor** instead of Linear Regression for better R²
- Add `Distance_km` (Haversine) as a regression feature
- Collect more data (200 rows is small for ML)

---

## 👤 Author

**Hari Ganesh**
- Course: Machine Learning
- 📧 [your email here]
- 🔗 [LinkedIn profile here]

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first.
