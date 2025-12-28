# 🏠 California Housing Price Prediction

A Flask web application for predicting California housing prices using a trained Gradient Boosting model.

## 📊 Model Performance

| Metric | Train | Test |
|--------|-------|------|
| RMSE | $47,703 | $56,786 |
| R² Score | 0.830 | 0.754 |

## 🚀 Quick Start

### 1. Create Virtual Environment
```bash
python -m venv .venv
.\.venv\Scripts\Activate.ps1  # Windows
# source .venv/bin/activate   # Linux/Mac
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the Application
```bash
python app.py
```

### 4. Open in Browser
Navigate to **http://127.0.0.1:5000**

## 📁 Project Structure

```
Housing Price Prediction/
├── app.py                                    # Flask web application
├── requirements.txt                          # Python dependencies
├── best_model_gradient_boosting_(tuned).joblib  # Trained model
├── model_metrics.json                        # Performance metrics
├── california-housing-price-prediction.ipynb # Training notebook
└── README.md                                 # This file
```

## 🔧 Input Features

The model requires 9 input features:

| Feature | Description | Example |
|---------|-------------|---------|
| MedInc | Median income (in $10,000s) | 3.87 |
| HouseAge | Median house age (years) | 29 |
| AveRooms | Average rooms per household | 5.43 |
| AveBedrms | Average bedrooms per household | 1.10 |
| Population | Block group population | 1425 |
| AveOccup | Average household members | 3.07 |
| Latitude | Block group latitude | 35.63 |
| Longitude | Block group longitude | -119.57 |
| Households | Number of households | 500 |

## 🔬 Feature Engineering Pipeline

The model automatically engineers additional features:

1. **IncomePerRoom** = MedInc / AveRooms
2. **LatLongInteraction** = Latitude × Longitude
3. **MedInc_Squared** = MedInc²
4. **MedInc_Cubed** = MedInc³
5. **AgeGroup_Young** = 1 if HouseAge < 20
6. **AgeGroup_Medium** = 1 if 20 ≤ HouseAge < 40
7. **AgeGroup_Old** = 1 if HouseAge ≥ 40

**Pipeline Order:** Input → Engineer 16 Features → RobustScaler → SelectKBest (12 features) → GradientBoostingRegressor

## 🌐 API Endpoints

### Web Interface
```
GET /
```
Returns the prediction form UI.

### Prediction API
```
POST /predict
Content-Type: application/json

{
  "MedInc": 3.87,
  "HouseAge": 29,
  "AveRooms": 5.43,
  "AveBedrms": 1.10,
  "Population": 1425,
  "AveOccup": 3.07,
  "Latitude": 35.63,
  "Longitude": -119.57,
  "Households": 500
}
```

**Response:**
```json
{
  "success": true,
  "prediction": 206855.82
}
```

### Model Info
```
GET /api/model-info
```
Returns model performance metrics.

### Health Check
```
GET /health
```
Returns application status.

## ⚙️ Requirements

- Python 3.8+
- Flask 2.3+
- scikit-learn 1.0+
- pandas 1.3+
- numpy 1.21+
- joblib 1.1+

## 📝 Notes

- The model was trained on the California Housing dataset (20,640 samples)
- Predictions are in USD (actual house values, not scaled)
- The model uses RobustScaler for handling outliers
- SelectKBest selects the 12 most informative features

## 👤 Author

Mohammed Ali

---
*Built with Flask & scikit-learn*
