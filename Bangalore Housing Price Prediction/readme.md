# 🏠 Bangalore House Price Prediction  
### *Machine Learning Regression Project using XGBoost & Scikit-Learn Pipeline*

---

## 📌 Project Overview
This project predicts **house prices in Bangalore** using machine learning.  
The workflow includes:

- Data cleaning & preprocessing  
- Exploratory Data Analysis (EDA)  
- Feature engineering  
- Building an XGBoost regression model  
- Hyperparameter tuning  
- Model evaluation (R², RMSE, MAE, MAPE)  
- Saving the model with Joblib  

The final model is wrapped inside a **Scikit-Learn Pipeline**, making it ready for deployment.

---

## 📂 Dataset Description
The dataset (`Bangalore house data.csv`) contains real-estate features such as:

| Column | Description |
|--------|-------------|
| `area_type` | Carpet area / Built-up area / Super built-up |
| `availability` | Ready to move / Immediate / etc. |
| `location` | Property location |
| `size` | Number of bedrooms (e.g., 2 BHK) |
| `society` | Society / building name |
| `total_sqft` | Total area in square feet |
| `bath` | Number of bathrooms |
| `balcony` | Number of balconies |
| `price` | Price in Lakhs |

---

## 🧹 Data Preprocessing

### ✔ Cleaning `total_sqft`
Some entries were ranges like `"1000-1500"`.  
These were converted to numeric values using the average of the range.

### ✔ Handling Missing Values
| Feature | Strategy |
|---------|----------|
| location | Mode |
| size | Mode |
| society | Mode |
| bath | Mean |
| balcony | Mean |

### ✔ Outlier Removal
Removed entries where **bath ≥ 5** to avoid unrealistic outliers.

### ✔ Feature Engineering
- Extracted numeric BHK from the `size` column → created `bhk`
- Cleaned and standardized `location` & `society` names  
- Created `price_per_sqft = price * 100000 / total_sqft`  

### ✔ Dropped Columns
- `size` column dropped after extracting BHK

---

## 📊 Exploratory Data Analysis
Visualizations included:

- Correlation heatmap  
- Scatterplot (Sqft vs Price)  
- Boxplot (BHK vs Price)  
- Regression plot  
- Pie charts for categorical features  
- Actual vs Predicted scatterplot  
- Residual plot  

These helped understand the relationships and distribution patterns.

---

## 🤖 Model Building

### **Model Used:**  
⭐ **XGBoost Regressor** (`objective="reg:squarederror"`)

### **Pipeline Structure**
Pipeline(
    preprocessor = ColumnTransformer(
    cat → OneHotEncoder
    num → passthrough),
    model = XGBRegressor
)


### **Hyperparameters Used**
```python
{
    'subsample': 0.8,
    'n_estimators': 300,
    'max_depth': 10,
    'learning_rate': 0.1,
    'colsample_bytree': 1,
    'objective': 'reg:squarederror',
    'random_state': 42
}

Hyperparameter search was originally done using RandomizedSearchCV, and then the best parameters were manually applied.

| Metric       | Value           |
| ------------ | --------------- |
| **R² Score** | 0.9396         |
| **RMSE**     | Low error       |
| **MAE**      | Low deviation   |
| **MAPE**     | Good % accuracy |
