# Quick Start Guide

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/Food-Delivery-Prediction.git
cd Food-Delivery-Prediction
```

### 2. Create Virtual Environment

```bash
python -m venv venv

# Activate on macOS/Linux
source venv/bin/activate

# Activate on Windows
venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Run Streamlit App

```bash
streamlit run main.py
```

Open your browser and go to: `http://localhost:8501`

---

## Model Files

- **optimized_rf_model.pkl** - Trained Random Forest model with optimized hyperparameters
- **label_encoders.pkl** - Categorical encoders for categorical features
- **Food_Delivery_Times.csv** - Training dataset

---

## Input Parameters for Predictions

When using the Streamlit app, you'll need to provide:

1. **Distance (km)**: 0.1 - 100.0 km
2. **Weather**: Clear, Rainy, Foggy, Windy
3. **Traffic Level**: Low, Medium, High
4. **Time of Day**: Morning, Afternoon, Evening, Night
5. **Vehicle Type**: Bike, Scooter, Car
6. **Preparation Time**: 1 - 60 minutes
7. **Courier Experience**: 0 - 20 years

---

## Expected Output

The model will predict the **Delivery Time** in minutes.

**Example:**

- Input: 10 km distance, Clear weather, Low traffic, Afternoon, Bike, 15 min prep, 3 years experience
- Output: ~32 minutes

---

## Troubleshooting

### Issue: "ModuleNotFoundError: No module named 'streamlit'"

**Solution:** Install dependencies again

```bash
pip install -r requirements.txt
```

### Issue: "FileNotFoundError: optimized_rf_model.pkl not found"

**Solution:** Ensure you're running from the project directory

```bash
cd Food-Delivery-Prediction
```

### Issue: "Error loading model" in Streamlit app

**Solution:** Ensure both pickle files are in the same directory as main.py

### Issue: Port 8501 already in use

**Solution:** Run on a different port

```bash
streamlit run main.py --server.port 8502
```

---

## File Structure After Installation

```
Food-Delivery-Prediction/
├── README.md
├── QUICKSTART.md (this file)
├── LICENSE
├── requirements.txt
├── .gitignore
├── model.ipynb
├── main.py
├── Food_Delivery_Times.csv
├── optimized_rf_model.pkl
└── label_encoders.pkl
```

---

## For Development: Jupyter Notebook

To explore the model development process:

```bash
jupyter notebook model.ipynb
```

This includes:

- Data preprocessing and cleaning
- Exploratory Data Analysis (EDA)
- Statistical feature analysis
- Model comparison and training
- Hyperparameter tuning
- Performance evaluation

---

## Next Steps

1. ✅ Install dependencies
2. ✅ Run the Streamlit app
3. ✅ Make predictions with your own delivery scenarios
4. ✅ Review the Jupyter notebook for model details
5. ✅ Deploy to production (Streamlit Cloud, Heroku, etc.)

---

## Performance Metrics

**Optimized Random Forest Model:**

- R² Score: 0.94
- MAE: 0.50 minutes
- RMSE: 0.63 minutes
- Generalization Gap: ~0% (Excellent)

---

## Model Deployment

### Streamlit Cloud (Free)

1. Push code to GitHub
2. Connect to Streamlit Cloud
3. Deploy with one click

### Heroku

1. Create Procfile: `web: streamlit run main.py --logger.level=error`
2. Deploy using Heroku CLI

### Docker

```dockerfile
FROM python:3.9
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
EXPOSE 8501
CMD ["streamlit", "run", "main.py"]
```

---

## Support & Issues

For issues or questions:

1. Check GitHub Issues
2. Review troubleshooting section above
3. Contact: your-email@example.com

---

**Happy Predicting! 🚀**
