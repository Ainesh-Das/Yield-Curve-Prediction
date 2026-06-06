# Stochastic Interest Rate Modelling and Prediction

This project implements the Cox-Ingersoll-Ross (CIR) short-rate model to reconstruct a full yield curve from only the 3-month rate, with a deterministic-shift CIR++ extension for comparison.

## Model Framework

The short rate follows the CIR process:

$$dr_t = \kappa(\theta - r_t)\,dt + \sigma\sqrt{r_t}\,dW_t$$

The closed-form affine term structure gives zero-coupon bond prices at any maturity, which are then converted to continuously compounded yields. On each test date, only the observed 3M yield is used as input — no other maturities are seen by the model.

## Repository Structure

```
├── CIR_Ainesh_24114008.ipynb   # Main notebook
├── train_data.csv              # Training yield panel
├── test_data.csv               # Labeled test dataset
└── test_data_3M.csv            # 3M-only input for test period
```

## Methodology

1. Clean and standardize raw yield data (missing values, outliers, scale normalization)
2. Calibrate $(κ, θ, σ)$ via penalized MLE on the exact CIR transition density
3. Reconstruct yields at 6M, 9M, 1Y, 2Y, 5Y, 10Y, 20Y, 30Y from the 3M input
4. Evaluate out-of-sample R², RMSE, MAE, and bias per maturity
5. Compare base CIR against the CIR++ deterministic-shift extension

## Results

Metrics are reported per tenor and in aggregate. The model exceeds the project threshold of R² > 0.85 on the held-out test set.

## Requirements

```
numpy  pandas  scipy  matplotlib
```

## How to Run

```bash
git clone https://github.com/Ainesh-Das/Yield-Curve-Prediction.git
cd Yield-Curve-Prediction
jupyter notebook CIR_Ainesh_24114008.ipynb
```
