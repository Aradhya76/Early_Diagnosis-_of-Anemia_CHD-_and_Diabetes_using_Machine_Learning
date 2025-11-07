# Blood Disease Prediction - README

This repository contains a Flask web application that predicts three blood-related conditions:
**Diabetes**, **Anemia**, and **Coronary Heart Disease (CHD)** using pre-trained scikit-learn models saved as `.pkl` files.

## Files required (place these in the project root / folders)
Expected project structure (minimal):

```
blood-disease-app/
├─ app.py
├─ requirements.txt
├─ models/
│  ├─ diabetes_model.pkl
│  ├─ diabetes_scaler.pkl   (optional)
│  ├─ anemia_model.pkl
│  ├─ anemia_scaler.pkl     (optional)
│  ├─ chd_model.pkl
│  └─ chd_scaler.pkl        (optional)
├─ templates/
│  ├─ base.html
│  ├─ diabetes.html
│  ├─ diabetesParameters.html
│  ├─ anemia.html
│  ├─ anemiaParameters.html
│  ├─ chd.html
│  └─ chdParameters.html
└─ static/
   ├─ style.css
   └─ validate.js
```

> Make sure the `.pkl` filenames match exactly what `app.py` loads:
> `diabetes_model.pkl`, `diabetes_scaler.pkl`, `anemia_model.pkl`, `anemia_scaler.pkl`, `chd_model.pkl`, `chd_scaler.pkl`

---

## Quick start — Run locally (recommended for development)

1. Create and activate a Python virtual environment:

Linux / macOS:
```bash
python3 -m venv venv
source venv/bin/activate
```

Windows (PowerShell):
```powershell
python -m venv venv
venv\Scripts\Activate.ps1
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Verify your models are present:
```bash
ls models
# should show the .pkl files like diabetes_model.pkl
```

4. Run the Flask app:
```bash
python app.py
```
Open http://127.0.0.1:5000 in your browser.

---

## Run in Google Colab (quick demo with public URL via ngrok)

1. Zip your project folder locally (or upload files individually to Colab).
2. In Colab, install dependencies:
```python
!pip install -q flask flask-ngrok scikit-learn numpy pandas requests
```
3. Upload and unzip your project zip, then `cd` into it:
```python
from google.colab import files
uploaded = files.upload()   # upload blood-disease-app.zip
!unzip -q blood-disease-app.zip -d blood-disease-app
%cd blood-disease-app
```
4. Start the app with flask-ngrok:
```python
from flask_ngrok import run_with_ngrok
import app as myapp

run_with_ngrok(myapp.app)
myapp.app.run()
```
Colab will print a public `https://xxxx.ngrok.io` URL — click it to open the GUI.

---

## Credits & License
This project is provided under the MIT License (see LICENSE file).
