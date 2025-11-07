# Early Diagnosis of Anemia, CHD and Diabetes using Machine Learning

**This README is an extended version that includes instructions for the GUI (Flask) and how to run it in Google Colab.**

## Table of Contents
- Project Overview
- Repository Structure
- Requirements
- Installation
- Usage
- GUI (Flask) — Web Interface & Colab
- Data & Models
- How it works (short)
- Notes & Next steps
- License

## Project Overview
This repository contains a small end‑to‑end project for early diagnosis prediction of three conditions using machine learning: **Anemia**, **Coronary Heart Disease (CHD)**, and **Diabetes**. It includes the CSV datasets used, trained models and scalers (pickle files), and simple Python scripts to run predictions.

## Repository structure (high‑level)
- `anemia.csv`, `diabetes.csv`, `framingham.csv` (datasets)  
- `anemia_model.pkl`, `diabetes_model.pkl`, `chd_model.pkl` (trained models)  
- `anemia_scaler.pkl`, `diabetes_scaler.pkl`, `chd_scaler.pkl` (scalers)  
- `anemia_prediction.py`, `diabetes_prediction.py`, `chd_disease_prediction.py` (prediction scripts)  
- `templates/`, `app.py` (Flask GUI files if present)  
- `30 algos Anemia.csv`, `30 algos Diabetes.csv`, `30 algos CHD.csv` (benchmark/result CSVs)  
- `LICENSE` (MIT)  

## Requirements
- Python 3.8+  
- numpy, pandas, scikit‑learn, joblib, flask, pyngrok (for Colab tunneling)  

Install dependencies (minimal):
```bash
pip install numpy pandas scikit-learn joblib flask pyngrok
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

## Usage (CLI)
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

## GUI (Flask) — Web Interface & Colab

A simple Flask-based GUI has been included (or can be generated) that provides a web form to input patient features and returns model predictions. The provided Colab-ready package (`flask_diabetes_ui_colab.zip`) contains a working example for **Diabetes** that:

- Automatically generates an input form based on the columns in `diabetes.csv` (except the target column).  
- Loads `models/diabetes_model.pkl` and `models/diabetes_scaler.pkl` from the `models/` folder (place them there).  
- Shows prediction and probability (if the model supports `predict_proba`).  
- Prints a public ngrok URL when run in Colab (requires ngrok authtoken) so you can open the UI in your browser.


### How to run the Flask GUI locally
1. Ensure `app.py` and `templates/` are in the project root.  
2. Place model and scaler files in `models/` (create if missing). Example filenames:
   - `models/diabetes_model.pkl`  
   - `models/diabetes_scaler.pkl`  
3. Install Flask:
```bash
pip install flask
```
4. Run the app:
```bash
python app.py
```
5. By default the app listens on `http://127.0.0.1:8501`. Open it in a browser.

### How to run the Flask GUI in Google Colab (auto ngrok)
1. Upload `flask_diabetes_ui_colab.zip` to Colab (or the app folder).  
2. Unzip and `cd` into the folder.  
```python
from google.colab import files
uploaded = files.upload()  # upload flask_diabetes_ui_colab.zip
!unzip flask_diabetes_ui_colab.zip -d flask_diabetes_ui_colab
%cd flask_diabetes_ui_colab
```
3. Install requirements:
```bash
!pip install flask pyngrok
```
4. (Optional) Upload `diabetes_model.pkl` and `diabetes_scaler.pkl` and move into `models/`:
```python
from google.colab import files
uploaded = files.upload()
!mv diabetes_model.pkl models/
!mv diabetes_scaler.pkl models/
```
5. Run the app (it will print the public ngrok URL):
```bash
!python app.py
```

**Note about ngrok:** As of late 2025, ngrok requires a verified account and authtoken to create tunnels. If you see an authentication error, either add your ngrok authtoken inside Colab (via `pyngrok.set_auth_token(<token>)`) or use an alternative tunnel service (localtunnel or cloudflared).

### Important: Same GUI process for Anemia and CHD
The GUI created for **Diabetes** uses a generic pattern that can be re-used for **Anemia** and **CHD** with minimal changes:

1. Add `anemia.csv` and `framingham.csv` (or the CHD dataset you have) to the repository.  
2. Add the trained model and scaler files:
   - `models/anemia_model.pkl` and `models/anemia_scaler.pkl`  
   - `models/chd_model.pkl` and `models/chd_scaler.pkl`  
3. Duplicate or extend the Flask app to add routes/forms for Anemia and CHD (the provided Colab-ready package generator already supports automatic form creation based on CSV columns).  
4. The inference workflow and front-end layout are identical — only the feature list and model files change.


## Data & Models
- CSV datasets: `anemia.csv`, `diabetes.csv`, `framingham.csv`  
- Model files: `*_model.pkl`  
- Scaler files: `*_scaler.pkl`  

## How it works (short)
1. Pre‑processing & scaling of dataset features  
2. Model training & benchmarking (CSV files like `30 algos …` show algorithm comparisons)  
3. Saving of best model and scaler  
4. Prediction scripts load artifacts and produce output

## Notes & Next steps
- Add `requirements.txt` with pinned versions for reproducibility.  
- Add UI pages for Anemia and CHD (I can generate these automatically if you upload `anemia.csv` and CHD dataset).  
- Improve error handling and add unit tests for inference code.  

## License
MIT License. See `LICENSE` file for full text.
