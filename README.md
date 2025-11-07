# Early Diagnosis of Anemia, CHD and Diabetes using Machine Learning



## Table of Contents
- Project Overview  
- Repository Structure  
- Requirements  
- Installation  
- Usage  
- Data & Models  
- How it works (short)    
- License  


## Project Overview
This repository contains a small end‑to‑end project for early diagnosis prediction of three conditions using machine learning: Anemia, Coronary Heart Disease (CHD), and Diabetes. It includes the CSV datasets used, trained models and scalers (pickle files), and simple Python scripts to run predictions.

## Repository structure (high‑level)
- `anemia.csv`, `diabetes.csv`, `framingham.csv` (datasets)  
- `anemia_model.pkl`, `diabetes_model.pkl`, `chd_model.pkl` (trained models)  
- `anemia_scaler.pkl`, `diabetes_scaler.pkl`, `chd_scaler.pkl` (scalers)  
- `anemia_prediction.py`, `diabetes_prediction.py`, `chd_disease_prediction.py` (prediction scripts)  
- `30 algos Anemia.csv`, `30 algos Diabetes.csv`, `30 algos CHD.csv` (benchmark/result CSVs)  
- `LICENSE` (MIT)  

## Requirements
- Python 3.8+  
- numpy, pandas, scikit‑learn, joblib (if used)  

Install dependencies:
```bash
pip install numpy pandas scikit-learn joblib
```

## Installation
```bash
git clone https://github.com/Aradhya76/Early_Diagnosis-_of-Anemia_CHD-_and_Diabetes_using_Machine_Learning.git
cd Early_Diagnosis-_of-Anemia_CHD-_and_Diabetes_using_Machine_Learning
python -m venv venv
# Activate your virtual environment:
# Windows: venv\Scripts\activate
# macOS/Linux: source venv/bin/activate
pip install -r requirements.txt
```

## Usage
Run a prediction script (example):
```bash
python diabetes_prediction.py
```

Programmatic example to load model & scaler:
```python
import pickle
import numpy as np

with open("diabetes_model.pkl","rb") as f:
    model = pickle.load(f)

with open("diabetes_scaler.pkl","rb") as f:
    scaler = pickle.load(f)

# Example sample input (replace with your actual features):
X = np.array([1, 85, 66, 29, 0, 26.6, 0.351, 31]).reshape(1, -1)
X_scaled = scaler.transform(X)
prediction = model.predict(X_scaled)
print("Prediction:", prediction[0])
```

## Data & Models
- CSV datasets: `anemia.csv`, `diabetes.csv`, `framingham.csv`  
- Model files: `*_model.pkl`  
- Scaler files: `*_scaler.pkl`  

## How it works 
1. Pre‑processing & scaling of dataset features  
2. Model training & benchmarking (CSV files like `30 algos …` show algorithm comparisons)  
3. Saving of best model and scaler  
4. Prediction scripts load artifacts and produce output  

## License
MIT License. See `LICENSE` file for full text.

