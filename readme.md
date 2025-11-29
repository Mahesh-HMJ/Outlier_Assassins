## 🛠️ Machine Learning Pipeline

The solution involves the following key steps:

### 1. Data Cleaning & Feature Engineering

* **Price Normalization:** The target variable (`price`) was unified by converting values from "Lakhs (L)" to "Crores (Cr)" to ensure consistency.
* **Outlier Handling:** Custom, context-driven filters were applied using **Area per BHK** to remove physically impossible or highly erroneous data points (e.g., extremely small areas for high BHK counts).
* **Feature Creation:** A critical feature, `area_per_bhk` (Area / BHK), was created to better capture density and value.

### 2. Feature Encoding

* **Target Encoding (Locality):** The high-cardinality `locality` feature was encoded using **Target Encoding** (mean price per locality). This technique significantly improves model performance over standard Label Encoding for this type of data.
* **Label Encoding:** Remaining categorical features (`type`, `region`, `status`, `age`) were encoded using **Label Encoding**.
* **Scaling:** Numerical features were scaled using `StandardScaler`.

### 3. Model Training & Evaluation

The **Random Forest Regressor** was chosen for its robustness and ability to handle non-linear relationships.

| Metric | Value | Interpretation |
| :--- | :--- | :--- |
| **R-squared ($\mathbf{R^2}$)** | **0.868** | The model explains **86.8%** of the variance in house prices. |
| **Mean Absolute Error (MAE)** | **$\approx 0.220$ Cr** | On average, the model's price prediction is off by **22 Lakhs** (0.22 Crores). |
| **Mean Squared Error (MSE)** | **$\approx 0.611$** | Measures the average squared difference (used to heavily penalize large errors). |

---

## ⚙️ Dependencies

To run the notebook and reproduce the analysis, you will need the following Python libraries:

* `pandas`
* `numpy`
* `matplotlib`
* `seaborn`
* `scikit-learn` (for modeling, preprocessing, and evaluation)
* `joblib` (for saving/loading the model)

You can install all dependencies using pip:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn joblib