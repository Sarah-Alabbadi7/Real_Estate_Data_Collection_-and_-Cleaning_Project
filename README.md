# Real_Estate_Data_Collection_-and_-Cleaning_Project

# Property Listings Data Analysis

## Objectives
This project aims to:
- Combine and clean property listings data from two different real estate websites.
- Perform exploratory data analysis (EDA) to understand trends and patterns.
- Prepare the data for potential machine learning models (e.g., price prediction, classification by property type).

## Websites Used
1. **Hilal Sale Data**: A dataset of property listings from an unspecified source (likely a local real estate platform).
2. **Dubizzle Properties for Sale**: A popular Middle Eastern classifieds website for real estate listings.

---

## Data Collection and Cleaning

### Steps Taken:
1. **Data Loading**:
   - Loaded datasets from `hilal_sale_data.csv` and `dubizzle_properties_for_sale.csv`.
   - Standardized column names (e.g., `Title` → `title`) for consistency.

2. **Missing Value Handling**:
   - Numeric columns (`bedrooms`, `bathrooms`, `garage`, `size`): Filled with median values.
   - Text columns (`location`): Filled with `"Unknown"`.

3. **Outlier Treatment**:
   - Used the IQR (Interquartile Range) method to cap outliers in numeric columns (`price`, `size`, `bedrooms`, `bathrooms`).
   - Added outlier indicator columns (e.g., `price_outlier`) for tracking.

4. **Property Type Extraction**:
   - Derived `property_type` from the `title` column using keywords:
     - `apartment`: Matched terms like "apartment," "flat," "condo."
     - `house`: Matched terms like "villa," "townhouse," "bungalow."
     - Default: `other`.

5. **Combining Data**:
   - Merged both datasets into a single DataFrame (`df`) using `pd.concat()`.

---

## Feature Engineering Strategy
1. **New Features**:
   - `property_type`: Categorical feature extracted from `title`.
   - Outlier flags (e.g., `price_outlier`) to mark capped values.

2. **Transformations**:
   - Numeric columns scaled to minimize skewness (e.g., log-transform for `price` if needed).
   - Categorical columns (`location`, `property_type`) encoded for modeling (e.g., one-hot encoding).

3. **Derived Metrics** (Potential):
   - Price per square meter (`price` / `size`).
   - Room ratio (`bedrooms` / `bathrooms`).

---

## Modeling Approach (If Applicable)
### Potential Use Cases:
1. **Price Prediction**:
   - **Target**: `price` (regression problem).
   - **Features**: `bedrooms`, `bathrooms`, `size`, `location`, `property_type`.
   - **Models**: Linear Regression, Random Forest, XGBoost.

2. **Property Type Classification**:
   - **Target**: `property_type` (classification problem).
   - **Models**: Logistic Regression, Decision Trees.

### Steps:
1. **Train-Test Split**: 80/20 split for evaluation.
2. **Feature Scaling**: Standardize numeric features.
3. **Model Training**: Optimize hyperparameters using cross-validation.
4. **Evaluation**:
   - Regression: RMSE, R².
   - Classification: Accuracy, F1-score.


## Output
- Final cleaned dataset: `combined_properties_data.csv`.
- Columns: `title`, `location`, `bedrooms`, `bathrooms`, `price`, `size`, `property_type`, etc.

