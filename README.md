
# GNSS Error Prediction

## Overview

This project focuses on predicting **GNSS (Global Navigation Satellite System) orbit errors** using a deep learning approach based on **Long Short-Term Memory (LSTM)** networks. The model learns temporal patterns from historical satellite error measurements and forecasts future error values in three dimensions:

- **R_Error** – Radial Error
- **A_Error** – Along-Track Error
- **C_Error** – Cross-Track Error

The objective is to improve GNSS positioning accuracy by modeling and predicting satellite orbit errors from historical observations.

---

## Dataset

The dataset contains GNSS satellite error observations with the following features:

| Feature | Description |
|----------|------------|
| R_Error | Radial orbit error |
| A_Error | Along-track orbit error |
| C_Error | Cross-track orbit error |

### Dataset Statistics

- Total Records: **73,507**
- Data Type: **Multivariate Time Series**
- Timestamp Column: `target_time`

---

## Data Preprocessing

1. Loaded the dataset using Pandas.
2. Converted `target_time` to datetime format.
3. Selected the three error components:
   - R_Error
   - A_Error
   - C_Error
4. Applied **StandardScaler** normalization.
5. Split data into:
   - Training Set: 60%
   - Validation Set: 20%
   - Test Set: 20%

---

## Sequence Generation

A sliding-window approach was used to convert the time-series data into supervised learning sequences.

### Parameters

- Sequence Length: **20**
- Input Shape: **(20, 3)**
- Output Shape: **(3)**

Each training sample contains the previous 20 observations of the three error components and predicts the next error values.

---

## Model Architecture

```text
Input (20 × 3)
        │
        ▼
LSTM (64 units, return_sequences=True)
Dropout = 0.1
        │
        ▼
LSTM (32 units)
Dropout = 0.1
        │
        ▼
Dense (64, ReLU)
        │
        ▼
Dense (3)
        │
        ▼
[R_Error, A_Error, C_Error]
```

### Training Configuration

| Parameter | Value |
|------------|--------|
| Optimizer | Adam |
| Learning Rate | 0.0005 |
| Loss Function | MAE |
| Metric | RMSE |
| Epochs | 50 |
| Batch Size | 64 |
| Early Stopping | Patience = 10 |

---

## Results

### Test Performance

| Metric | Value |
|----------|----------|
| Test RMSE | 0.00455 |

The model achieved a very low prediction error, demonstrating its ability to capture temporal dependencies in GNSS orbit error signals.

---

## Visualization

The notebook generates comparison plots between:

- Actual vs Predicted R_Error
- Actual vs Predicted A_Error
- Actual vs Predicted C_Error

These visualizations help evaluate forecasting performance and model accuracy.

---

## Technologies Used

- Python
- Pandas
- NumPy
- TensorFlow / Keras
- Scikit-learn
- Matplotlib
- Google Colab

---

## Installation

Clone the repository:

```bash
git clone https://github.com/amaynagar/GNSSerrorprediction.git
cd GNSSerrorprediction
```

Install dependencies:

```bash
pip install pandas numpy matplotlib scikit-learn tensorflow
```

---

## Usage

Launch the notebook:

```bash
jupyter notebook g01errorpred.ipynb
```

or open it directly in **Google Colab**.

The notebook performs:

1. Data loading and preprocessing
2. Feature normalization
3. Sequence generation
4. LSTM model training
5. Model evaluation
6. Prediction visualization

---

## Project Structure

```text
GNSSerrorprediction/
│
├── g01errorpred.ipynb
├── G01_data.csv
├── README.md
│
└── outputs/
    └── prediction_plots/
```

---

## Future Improvements

- Bidirectional LSTM networks
- GRU-based forecasting models
- Transformer-based time-series prediction
- Multi-step forecasting
- Real-time GNSS error correction
- Model deployment using FastAPI or Streamlit

---


