# Mental Health Prediction Model

This project is a mental health prediction web app that uses a trained machine learning model to estimate a student's mental health score based on profile, digital habits, lifestyle, and stress-related inputs.

## What this project contains

- `main.py`
  - FastAPI backend application.
  - Loads the trained model from `Mental_Health_Model.pkl`.
  - Defines a `/predict` endpoint that accepts student data and returns a predicted mental health score.

- `Mental_Health_Model.pkl`
  - Trained machine learning model persisted with `joblib`.
  - Used by the backend to predict the score from input features.

- `requirements.txt`
  - Python dependencies required to run the backend and frontend locally.
  - Includes `fastapi`, `uvicorn`, `pandas`, `scikit-learn`, `joblib`, and supporting packages.

- `index.html`
  - Static frontend for collecting input from users.
  - Includes the form and layout for the user interface.

- `style.css`
  - Styling for the frontend.
  - Uses a deep blue / black / white theme with glow and responsive layout.

- `script.js`
  - Client-side JavaScript for the frontend.
  - Validates form input, sends requests to the backend, and renders results.

- `Student Social Media And Mental Health Impact.csv`
  - Original dataset supporting the model.
  - Useful for model retraining or analysis.

- `requirements (1).txt`
  - Duplicate or backup dependency file.
  - Only `requirements.txt` is required for deployment.

## Backend details

The backend exposes a single POST endpoint:

- `POST /predict`
  - Request body: JSON matching the `StudentData` schema.
  - Response body: JSON containing `predicted_mental_health_score`.

### Expected input fields

- `age` (integer, 10–100)
- `gender` (`Male` or `Female`)
- `country` (string)
- `academic_level` (`Undergraduate`, `Graduate`, `High School`)
- `most_used_platform` (`Facebook`, `LinkedIn`, `Instagram`, `Snapchat`, `Twitter`, `YouTube`, `TikTok`, `LINE`, `KakaoTalk`, `VKontakte`, `WhatsApp`, `WeChat`)
- `purpose_of_use` (`Networking`, `Education`, `Entertainment`, `News`)
- `avg_daily_usage_hours` (float, 0–24)
- `daily_unlocks` (integer, 0+)
- `study_hours` (float, 0–24)
- `physical_activity_hours` (float, 0–24)
- `sleep_hours_per_night` (float, 0–24)
- `stress_level` (`Medium`, `Low`, `Very High`, `High`)

The backend also groups countries into a fixed list before prediction, mapping unknown countries to `Other`.

## Frontend details

The frontend is built with plain HTML, CSS, and JavaScript:

- `index.html` contains the UI and form structure.
- `style.css` provides the visual theme and responsive layout.
- `script.js` handles input validation, form submission, and result rendering.

The frontend sends requests to the backend API base configured in `script.js`.

## Local setup and running

### 1. Create a virtual environment

```powershell
py -3.11 -m venv .venv311
. .\.venv311\Scripts\Activate.ps1
```

### 2. Install dependencies

```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 3. Run the backend

```powershell
python -m uvicorn main:app --reload --host 127.0.0.1 --port 8000
```

### 4. Open the frontend

Open `index.html` in the browser or serve the folder locally:

```powershell
python -m http.server 5500
```

Then visit:

```
http://127.0.0.1:5500/index.html
```

## Deployment on Render

For Render deployment, ensure `requirements.txt` is present at the repository root and use one of these start commands in Render:

```text
uvicorn main:app --host 0.0.0.0 --port $PORT
```

If Render requires a `Procfile`, use:

```text
web: uvicorn main:app --host 0.0.0.0 --port $PORT
```

## Notes

- The model file `Mental_Health_Model.pkl` must remain in the root directory for the backend to load it.
- The frontend currently points to `https://menal-helth-prediction-1.onrender.com` in `script.js`. Update this URL if you deploy the backend to a different address or want to use local development instead.
- The app is informational and not a medical diagnosis tool.

## Recommended next improvements

- Add a backend health-check endpoint like `GET /health`.
- Add a `Procfile` for easier Render deployment.
- Add example request/response samples to the README.
- Add model versioning and retraining instructions.
