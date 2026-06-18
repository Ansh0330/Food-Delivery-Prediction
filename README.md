# Food Delivery Time Prediction

A machine learning project that predicts delivery times for food orders using Random Forest regression with hyperparameter tuning. This project includes both a Jupyter notebook for model development and a Streamlit web application for real-time predictions.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Model Performance](#model-performance)
- [Key Findings](#key-findings)
- [Technologies Used](#technologies-used)
- [Results](#results)
- [Contributing](#contributing)
- [License](#license)

## 📊 Overview

This project builds a predictive model to estimate food delivery times based on various factors such as distance, weather conditions, traffic levels, time of day, vehicle type, preparation time, and courier experience. The model is trained using a Random Forest Regressor with optimized hyperparameters via RandomizedSearchCV.

**Problem Statement:** Predict accurate delivery times to improve customer satisfaction and operational efficiency in food delivery services.

## ✨ Features

- **Data Preprocessing:** Handle missing values, clean data, and encode categorical variables
- **Exploratory Data Analysis:** Statistical analysis and visualization of delivery factors
- **Feature Engineering:** Correlation analysis and ANOVA testing for feature importance
- **Model Development:** Compare Decision Tree and Random Forest models
- **Hyperparameter Tuning:** RandomizedSearchCV to find optimal parameters
- **Model Evaluation:** Comprehensive metrics (MAE, MSE, RMSE, R²)
- **Web Application:** Interactive Streamlit app for real-time predictions
- **Model Persistence:** Serialized models for easy deployment

## 📁 Dataset

**Source:** Food_Delivery_Times.csv

**Features:**

- `Order_ID`: Unique order identifier (removed during preprocessing)
- `Distance_km`: Distance from restaurant to delivery location (km)
- `Weather`: Weather conditions (Clear, Rainy, Foggy, Windy)
- `Traffic_Level`: Traffic intensity (Low, Medium, High)
- `Time_of_Day`: Time period (Morning, Afternoon, Evening, Night)
- `Vehicle_Type`: Type of delivery vehicle (Bike, Scooter, Car)
- `Preparation_Time_min`: Time to prepare the order (minutes)
- `Courier_Experience_yrs`: Years of delivery experience
- `Delivery_Time_min`: **Target Variable** - Actual delivery time (minutes)

**Data Characteristics:**

- Missing values in categorical and numerical columns (handled via mode and median imputation)
- 8 features (after dropping Order_ID)
- Regression problem with continuous target variable

## 🏗️ Project Structure

```
Food-Delivery-Prediction/
├── README.md                      # This file
├── requirements.txt               # Python dependencies
├── model.ipynb                    # Jupyter notebook with model development
├── main.py                        # Streamlit web application
├── Food_Delivery_Times.csv        # Dataset
├── optimized_rf_model.pkl         # Trained Random Forest model
└── label_encoders.pkl             # Encoded categorical variables
```

## 🚀 Installation

### Prerequisites

- Python 3.7 or higher
- pip or conda package manager

### Setup

1. **Clone the repository:**

```bash
git clone https://github.com/Ansh0330/Food-Delivery-Prediction.git
cd Food-Delivery-Prediction
```

2. **Create a virtual environment (optional but recommended):**

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies:**

```bash
pip install -r requirements.txt
```

## 💻 Usage

### Option 1: Run the Streamlit Web App

```bash
streamlit run main.py
```

The app will open in your browser at `http://localhost:8501`

**Features:**

- Input delivery parameters through an interactive form
- Get real-time delivery time predictions
- User-friendly interface for non-technical users

### Option 2: Explore the Jupyter Notebook

```bash
jupyter notebook model.ipynb
```

This notebook includes:

- Data loading and preprocessing
- Exploratory data analysis with visualizations
- Statistical testing (Correlation analysis, ANOVA)
- Model comparison (Decision Tree vs Random Forest)
- Hyperparameter tuning with RandomizedSearchCV
- Model evaluation and performance metrics
- Model serialization for deployment

## 📈 Model Performance

### Decision Tree Regressor (Baseline)

- **Training R² Score:** 1.00 (Perfect fit - **OVERFITTING**)
- **Test R² Score:** 0.49
- **Test MAE:** 10.56 minutes
- **Test RMSE:** 15.06 minutes

**Analysis:** The decision tree overfits the training data due to its nature of creating complex decision boundaries. While it perfectly memorizes training data, it generalizes poorly to unseen data.

### Random Forest Regressor (Default)

- **Test MAE:** 7.06 minutes
- **Test MSE:** 100.12
- **Test RMSE:** 10.01 minutes
- **Test R² Score:** 0.78

### Optimized Random Forest Regressor

- **Best Hyperparameters Found:**
  - `n_estimators`: 781
  - `max_depth`: 11
  - `max_features`: 3
  - `min_samples_split`: 3
  - `min_samples_leaf`: 3

- **Performance:**
  - **Test MAE:** 6.88 minutes
  - **Test MSE:** 92.53
  - **Test RMSE:** 9.62 minutes
  - **Test R² Score:** 0.79

**Improvement:** The optimized model achieved a 1.4% improvement in R² (from 0.78 to 0.79) and reduced MAE by 0.18 minutes through hyperparameter tuning, demonstrating consistent performance gains.

## 🔍 Key Findings

### Statistical Analysis Results

1. **Feature Importance (Correlation with Delivery Time):**
   - Distance is the strongest predictor of delivery time
   - Preparation time significantly impacts total delivery time
   - Courier experience inversely correlates with delivery time

2. **ANOVA Test Results:**
   - Weather, Traffic Level, Time of Day, and Vehicle Type are statistically significant predictors (p < 0.05)
   - All categorical features have meaningful impact on delivery times

3. **Model Diagnostics:**
   - Decision Tree: Overfitting identified by comparing training (R²=1.00) vs test (R²=0.49) performance
   - Random Forest: Excellent generalization with balanced train/test metrics
   - Hyperparameter tuning: Achieved marginal but consistent improvements

## 🛠️ Technologies Used

- **Python 3.x**
- **scikit-learn:** Machine learning algorithms and metrics
- **pandas:** Data manipulation and analysis
- **numpy:** Numerical computing
- **matplotlib & seaborn:** Data visualization
- **scipy:** Statistical testing
- **streamlit:** Web application framework
- **pickle:** Model serialization

## 📊 Results

### Model Performance Comparison

| Model                   | MAE   | MSE    | RMSE  | R² Score |
| ----------------------- | ----- | ------ | ----- | -------- |
| Decision Tree           | 10.56 | 243.24 | 15.06 | 0.49     |
| Random Forest (Default) | 7.06  | 100.12 | 10.01 | 0.78     |
| Optimized Random Forest | 6.88  | 92.53  | 9.62  | 0.79     |

**Analysis:** The Optimized Random Forest model outperforms the default Random Forest with lower error metrics. Despite the Decision Tree achieving perfect training fit (R²=1.00), it severely overfits and fails on test data (R²=0.49). The Random Forest ensemble provides superior generalization with a 0.79 R² score on unseen data.

### Model Selection

✅ **Chosen Model:** Optimized Random Forest Regressor

- Excellent generalization ability
- Interpretable feature importance
- Robust to outliers and noise
- Fast prediction time
- Suitable for production deployment

## 🚀 Deployment

The trained model (`optimized_rf_model.pkl`) and label encoders (`label_encoders.pkl`) are ready for deployment:

1. **Streamlit App:** Run locally or deploy to Streamlit Cloud
2. **API Server:** Integrate model with REST API framework (Flask, FastAPI)
3. **Batch Predictions:** Use for processing multiple orders
4. **Mobile App:** Backend integration with mobile applications

## 📝 Model Usage Example

```python
import pickle
import pandas as pd

# Load model and encoders
with open('optimized_rf_model.pkl', 'rb') as f:
    model = pickle.load(f)

with open('label_encoders.pkl', 'rb') as f:
    encoders = pickle.load(f)

# Prepare input data
input_data = pd.DataFrame({
    'Distance_km': [10.5],
    'Weather': ['Clear'],
    'Traffic_Level': ['Low'],
    'Time_of_Day': ['Afternoon'],
    'Vehicle_Type': ['Bike'],
    'Preparation_Time_min': [15],
    'Courier_Experience_yrs': [3.0]
})

# Encode categorical features
for col in ['Weather', 'Traffic_Level', 'Time_of_Day', 'Vehicle_Type']:
    input_data[col] = encoders[col].transform(input_data[col])

# Make prediction
predicted_time = model.predict(input_data)[0]
print(f"Predicted delivery time: {predicted_time:.2f} minutes")
```

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👤 Author

**Ansh Kotnala**

## 🙏 Acknowledgments

- Dataset provided for machine learning education
- scikit-learn documentation and community
- Streamlit framework for easy web app development

## 📧 Contact

For questions or inquiries, please reach out through:

- GitHub Issues
- Email: meanshbhardwaj@gmail.com

---

**Last Updated:** 2026-06-18

**Status:** ✅ Production Ready
