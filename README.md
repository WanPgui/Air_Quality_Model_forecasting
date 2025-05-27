# 🌫️ Air Quality Forecasting with LSTM

This project tackles a real-world problem: forecasting PM2.5 air pollution levels in Beijing using historical air quality and weather data. Accurate predictions of PM2.5 can support better public health responses and urban planning strategies.

## 📌 Problem Statement

Air pollution—especially PM2.5—poses significant health risks. This project applies machine learning, specifically **Recurrent Neural Networks (RNNs)** and **Long Short-Term Memory (LSTM)** models, to forecast hourly PM2.5 levels based on weather and pollutant data.

---

## 📊 Dataset

The data comes from a Kaggle challenge and includes three main files:

- `train.csv` – Historical data for training
- `test.csv` – Data used to generate predictions
- `sample_submission.csv` – Format for final submission

Each row represents an hour, with columns such as:

- `PM2.5` (target)
- `TEMP`, `DEWP`, `PRES`, `Iws`, `Is`, `Ir`
- `cbwd` (categorical wind direction)
- Date components: year, month, day, hour

---

## 🧪 Preprocessing Steps

- Combined date features into a timestamp.
- Handled missing PM2.5 values via forward fill + interpolation.
- Scaled features using MinMaxScaler.
- Converted dataset into sequences of 24-hour windows to predict the next PM2.5 value.
- One-hot encoded `cbwd` (wind direction) for categorical data inclusion.

---

## 🧠 Model Overview

The best-performing model was a **stacked LSTM** network:

- 3 LSTM layers: 256, 128, 64 units
- Dropout (0.3) to reduce overfitting
- LayerNormalization between layers
- Final Dense layer with linear activation

**Optimizer**: Adam  
**Loss Function**: MSE  
**Learning Rate**: 1e-5  
**Best RMSE (Validation)**: **4713**

---

## 📈 Results

| Experiment | Parameters | Epochs | RMSE (val) | Notes |
|-----------:|------------|--------|------------|-------|
| #1 | LSTM(128), LR=1e-3, dropout=0.2 | 30 |5680| Baseline model |
| #2 | LSTM(256), 2 layers, LR=1e-4 | 35 | 4944 | Improved depth |
| #3 | LSTM(256+128), dropout 0.3 | 40 | 4829 | Better generalization |
| #4 | LSTM(512+256+128), dropout 0.3, norm | 25 | **4713** | ✅ Best performance |
| #5 | GRU-based | 30 | 5021 | Slightly worse |

---

## 🚀 How to Run Locally

1. Clone the repository:
   ```bash
   git clone https://github.com/WanPgui/Air_Quality_Model_Frorecasting.git
   cd air-quality-lstm



🔍 Repository Structure

📁 Air_Quality_Model_Forecasting/
├── 📄 air_quality_forecasting_starter_code.ipynb
├── 📄 submission.csv
├── 📄 train.csv
├── 📄 test.csv
├── 📄 sample_submission.csv
├── 📄 README.md
