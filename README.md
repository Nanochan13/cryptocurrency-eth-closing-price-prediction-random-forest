# cryptocurrency-eth-closing-price-prediction-random-forest
A machine learning project for predicting daily cryptocurrency closing prices using the Random Forest algorithm with robustness and data leakage validation.

# ETH/IDR Closing Price Prediction using Random Forest

## 📌 Project Overview
This project aims to predict the next-day closing price of ETH/IDR using the Random Forest regression algorithm.  
Instead of directly predicting price, the model predicts the next-day return (t+1), which is then converted back into IDR closing price for evaluation and interpretation.

This approach is designed to improve model robustness in financial time-series forecasting.

---

## 🎯 Objective
To develop a machine learning model capable of forecasting ETH/IDR next-day movement while ensuring:

- No data leakage
- Proper time-based validation
- Fair comparison with baseline model
- Robust multi-metric performance evaluation

---

## 📊 Dataset
The dataset consists of historical ETH/IDR price data including:

- Open price  
- High price  
- Low price  
- Close price  

Target variable:
- Return (t+1)

Return is calculated from closing prices and aligned properly to avoid future information leakage.

---

## 📐 Why Predict Return Instead of Price?

Financial time-series data such as cryptocurrency prices are typically non-stationary, meaning their scale changes over time. Directly predicting raw price can cause the model to focus on absolute value magnitude rather than relative movement.

By predicting return (t+1) instead of raw price:

- The data becomes more scale-invariant  
- The model learns relative percentage movement  
- It reduces bias caused by long-term price growth  
- It improves generalization across different price ranges  

After prediction, the return is converted back into actual price (IDR) to make evaluation and interpretation more practical and meaningful.

This approach aligns with common practices in financial machine learning research.

---

## ⚙️ Methodology

### 1️⃣ Target Engineering
- Compute return (t+1) from closing prices
- Align features and target carefully
- Remove NaN values after shifting
- Convert predicted return back to IDR price using:

Predicted_Close(t+1) = Close(t) × (1 + Predicted_Return)

---

### 2️⃣ Train-Test Split
- 90% training data
- 10% testing data
- Time-series split (no shuffling)

This preserves chronological order and prevents look-ahead bias.

---

### 3️⃣ Model
- Random Forest Regressor (Scikit-learn)

Random Forest is chosen due to its ability to:
- Capture non-linear relationships
- Handle structured tabular data effectively
- Reduce overfitting via ensemble learning

---

## 📈 Evaluation Metrics

Model performance is evaluated using:

- Mean Absolute Error (MAE)
- Mean Absolute Percentage Error (MAPE)
- Root Mean Squared Error (RMSE)
- R² Score

All metrics are calculated on reconstructed closing prices (IDR), not on raw returns.

---

## 🛡 Data Leakage Validation

To ensure model reliability and integrity, multiple leakage detection tests were implemented:

1. Feature shifting test  
   (All features shifted backward to ensure no implicit future usage)

2. Baseline comparison  
   (Close_t → Close_t+1 naive prediction comparison)

3. Randomized target test  
   (Target shuffled to verify model does not learn noise)

4. Future feature (peek) test  
   (Artificial future information injected to confirm abnormal score inflation)

These validation steps confirm that model performance is not driven by unintended future information.

---

## 🚀 Tools & Libraries

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib

---

## 📂 Repository Structure

- `notebook.ipynb` → Main modeling and evaluation notebook  
- `dataset.csv` → ETH/IDR historical dataset  

---

## 📌 Research Context

This project is developed as part of undergraduate final project research in machine learning for financial time-series forecasting, with emphasis on:

- Proper validation methodology  
- Leakage prevention  
- Financially meaningful target engineering  

---

Developed for academic research and educational purposes.
