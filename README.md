# Insurance Fraud Claims Detection

This project focuses on building a model to predict fraudulent vehicle insurance claims.

## Files

- **Dataset:**
  - `insurance_claims.csv`

- **Python Code:**
  - Jupyter notebook: `insurance_claims.ipynb`

## Problem Statement

The objective is to develop a model capable of predicting fraudulent vehicle insurance claims. The dataset is obtained from Kaggle: [Insurance Fraud Claims Detection](https://www.kaggle.com/buntyshah/insurance-fraud-claims-detection).

## Data Analysis

- **Dataset Overview:**
  - Contains 1000 observations and 40 dimensions.
  - Binary classification problem - 'fraud_reported' (Yes/No).

- **Column Descriptions:**
  - Columns include various features such as `months_as_customer`, `age`, `policy_number`, etc.

- **Missing Value Analysis:**
  - Identified missing values represented as "?" and replaced with NaN.
  - Dropped variables with missing values exceeding 30%: `_c39`, `property_damage`, `police_report_available`.

- **Feature Engineering:**
  - Converted date columns (`policy_bind_date`, `incident_date`) to datetime format.
  - Derived new features like `policy_Month`, `policy_Year`, `Inc_Month`.
  - Created `Capital_Loss_or_Gain` based on `capital-gains` and `capital-loss`.
  - Imputed missing values for `collision_type` using KNN Imputation.
  - Created a new variable `total_claim` and converted related variables to categorical type codes.
  
- **Feature Selection:**
  - Applied correlation analysis (Heatmap) to identify and address multicollinearity.
  - Dropped `months_as_customer` due to high correlation with `age`.
  - Applied Chi-Sq-Test to select significant categorical variables.

- **Down-sampling:**
  - Balanced the imbalanced dataset using resampling techniques (0 - 400, 1 - 247).

- **Model Building:**
  - **Random Forest:**
    - Accuracy: 0.8307692307692308
    - Confusion Matrix: 
      ```
      [[110  22]
      [11  52]]
      ```

  - **Decision Tree:**
    - Accuracy: 0.7487179487179487
    - Confusion Matrix: 
      ```
      [[108  24]
      [25  38]]
      ```

  - **Logistic Regression:**
    - Accuracy: 0.6564102564102564
    - Confusion Matrix: 
      ```
      [[119  13]
      [54  9]]
      ```

  - Random Forest performed the best among the models.

## Usage

1. Clone the repository:
   ```bash
   git clone <repository_url>
   ```

2. Navigate to the project directory:
   ```bash
   cd Insurance-Fraud-Claims-Detection
   ```

3. Explore the dataset and Jupyter notebook for detailed analysis and code.

Feel free to refer to `insurance_claims.ipynb` for an in-depth explanation of the project.


**Note:** Adjust file paths and comments as needed for your project structure.
