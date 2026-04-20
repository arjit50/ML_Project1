# ML_Project1

A renewable energy evaluation platform that analyzes location data and predicts the best energy source for a region using a hybrid pipeline of frontend visualization, a Node.js data API, and a Flask-based machine learning service.

## Project Structure

- `ML_Project-master/`
  - `FRONTEND/` - Static web UI for entering PIN code, income, population density, and visualizing renewable energy potential.
  - `API_NODE_SERVER/` - Node.js Express API server that gathers location, weather, elevation, solar irradiance, and biomass data.
  - `ML Server/` - Flask app that loads an XGBoost model to classify the recommended energy source (`Biomass`, `Solar`, or `Wind`).

## Key Features

- Location lookup based on Indian PIN code
- Weather data retrieval using Weatherstack
- Elevation lookup using Open Elevation API
- Solar irradiance from JRC PVcalc API
- Biomass potential estimation from state-level data
- Prediction of best renewable energy source via a trained XGBoost model
- Interactive map and radar chart visualization in the frontend

## How It Works

1. The frontend collects:
   - `pincode`
   - `avgIncome`
   - `populationDensity`
2. It sends the PIN code to the Node API at `http://localhost:3000/api/data`.
3. The Node API retrieves:
   - latitude and longitude
   - city and state
   - elevation
   - weather metrics
   - solar irradiance
   - biomass potential
4. The frontend forwards the combined data to the Flask ML server at `http://localhost:6565/predict`.
5. The ML server returns a predicted energy source.
6. The frontend updates the UI and recommendation dashboard.

## Setup Instructions

> The actual app files are inside `ML_Project-master/` after extracting `ML_Project-master.zip`.

### 1. Start the Node API server

```powershell
cd "c:\Users\LENOVO\Desktop\ML_Project1\ML_Project-master\API_NODE_SERVER"
npm install
node index.js
```

This starts the API at `http://localhost:3000`.

### 2. Start the Python ML server

```powershell
cd "c:\Users\LENOVO\Desktop\ML_Project1\ML_Project-master\ML Server"
pip install -r requirements.txt
python main.py
```

This starts the ML prediction API at `http://localhost:6565`.

### 3. Open the frontend

- Open `ML_Project-master/FRONTEND/index.html` in a browser.
- Or serve the frontend from a local server if preferred:

```powershell
cd "c:\Users\LENOVO\Desktop\ML_Project1\ML_Project-master\FRONTEND"
python -m http.server 8000
```

Then visit `http://localhost:8000`.

## Important Notes

- The Node API uses hardcoded third-party API keys in `API_NODE_SERVER/index.js`.
- The ML server expects `xgboost_energy_model.pkl` in the `ML Server/` directory.
- The frontend currently sends a fixed `electricity_demand` value of `450` to the prediction API.
- The UI contains some hardcoded presentation values based on the predicted class.

## Dependencies

### Node API

- `express`
- `cors`

### ML Server

- `flask`
- `flask-cors`
- `pandas`
- `scikit-learn`
- `xgboost`
- `numpy`

## Notes for Improvement

- Replace hardcoded external API keys with environment variables.
- Add error handling for failed external API responses.
- Add a proper frontend build or static server deployment.
- Update prediction inputs to use true dynamic electricity demand.

## Contact

For any updates or improvements, edit the appropriate folder:
- frontend: `ML_Project-master/FRONTEND`
- data API: `ML_Project-master/API_NODE_SERVER`
- ML service: `ML_Project-master/ML Server`

