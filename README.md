# Improving NWM Runoff Forecasts with Deep Learning Error Correction

## 1. Project Objective

This project aims to improve a previous project, completed for CS-4440 at Appalachian State University, investigating the use of deep learning models to improve the accuracy of the National Water Model (NWM) for short-range runoff forecasting. The core approach is not to replace the NWM, but to build a data-driven post-processor that learns to predict and correct its systematic errors.

The primary goal was to compare the effectiveness of three distinct neural network architectures in this error-correction task:
* A **Simple Recurrent Neural Network (RNN)** as a baseline sequential model.
* A **Long Short-Term Memory (LSTM)** network, the industry standard for time-series forecasting.
* A **Transformer** network, a state-of-the-art architecture based on attention mechanisms.

## 2. Methodology

* **Error Prediction**: Instead of predicting streamflow directly, the models were trained to predict the residual error (`NWM_forecast - USGS_observation`). This predicted error is then subtracted from the original NWM forecast to produce a more accurate, corrected forecast.
* **Station-Specific Models**: Separate models were trained for two distinct USGS monitoring stations to capture unique local error characteristics.
* **Sequence Modeling**: The models used a 24-hour lookback window, using time-series data of NWM forecasts and engineered time-based features to predict the error at the next hour.
* **Evaluation**: Model performance was evaluated against the baseline NWM forecast using four standard hydrological metrics: Coefficient of Correlation (CC), Root Mean Square Error (RMSE), Percent Bias (PBIAS), and Nash-Sutcliffe Efficiency (NSE).

## 3. Key Results

The study successfully demonstrated that all three deep learning architectures could learn to correct the NWM's systematic underestimation of streamflow. As hypothesized, the more complex **LSTM and Transformer models significantly outperformed the baseline Simple RNN**, yielding substantial improvements across all evaluation metrics and lead times. The final corrected forecasts from the LSTM and Transformer models provided a much more reliable and accurate prediction of observed runoff.

## 4. How to Run

To replicate this project, follow these steps:

**Prerequisites:**
* Python 3.9+
* The raw data files placed in the `/data/raw/` directory.

**1. Set up the Environment:**
It is recommended to use a virtual environment.

```bash
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

Create/use a requirements.txt file with the necessary libraries (e.g., tensorflow, pandas, scikit-learn, pyarrow, matplotlib, seaborn) and install them.

```bash
pip install -r requirements.txt
```

Execute the Jupyter notebooks in numerical order to reproduce the entire workflow.

    01-data-exploration.ipynb: Loads and explores the raw data.

    02-preprocessing.ipynb: Cleans, aligns, scales, and sequences the data.

    03-training-and-tuning.ipynb: Trains the RNN, LSTM, and Transformer models for both stations.

    04-results-and-visualization.ipynb: Evaluates the trained models and generates all final results and figures.
