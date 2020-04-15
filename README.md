Insurance-Fraud-Claims-Detection

Problem Statement: -
Need a model to predict the fraudlent vehicle insurance claims

Kaggle data set https://www.kaggle.com/buntyshah/insurance-fraud-claims-detection

insurance_claims.csv - Dataset
insurance_claims.ipynb - Python code(Jupyter Nitebook)

Data Analysis: -
The data contains 1000 observations and 40 dimensions. The data is imbalanced as the target variable 'fraud_reported' has more ‘No’ category than ‘Yes’. (Binary classification)
The following are the columns
       'months_as_customer', 'age', 'policy_number', 'policy_bind_date',
       'policy_state', 'policy_csl', 'policy_deductable',
       'policy_annual_premium', 'umbrella_limit', 'insured_zip', 'insured_sex',
       'insured_education_level', 'insured_occupation', 'insured_hobbies',
       'insured_relationship', 'capital-gains', 'capital-loss',
       'incident_date', 'incident_type', 'collision_type', 'incident_severity',
       'authorities_contacted', 'incident_state', 'incident_city',
       'incident_location', 'incident_hour_of_the_day',
       'number_of_vehicles_involved', 'property_damage', 'bodily_injuries',
       'witnesses', 'police_report_available', 'total_claim_amount',
       'injury_claim', 'property_claim', 'vehicle_claim', 'auto_make',
       'auto_model', 'auto_year', 'fraud_reported', '_c39'

1.	Missing Value Analysis
The data has missing values in “?” format. The “?” was replaced with NaN and the count was recognised.
collision_type                       178
property_damage                360
police_report_available     343
_c39                                        1000

The variables _c39, property_damage, police_report_available were dropped as the missing values were greater than 30% of the data.

The variables were converted into appropriate data types i.e. float and object. Then the categorical variables were converted into appropriate cat type codes.

For collision_type variable the missing value was 162 for fraud_reported=No and 16 for 'fraud_reported=Yes. The 162 missing collison_type with fraud_reported =Yes category was dropped as already the Yes category was large.(A form of balancing the data).

The remaining 16 observations was imputed using KNN Imputation method. Few values came up with decimal points which was rounded off as it is a categorical variable.

2.	Feature Engineering

policy_bind_date, incident_date were converted into datetime format using dattime library.

policy_Month  Month derived out of policy_bind_date
policy_Year  Year derived out of policy_bind_date
Inc_Month Month derived out of incident_date.

The incident_date and policy_bind_date were dropped. The policy_month, policy_Year and inc_Month were converted into categorical variables.

Capital_Loss_or_Gain  Variable derived by simple mathematical calculation. (df_ins['capital-gains']-abs(df_ins['capital-loss']).

capital-gains' and 'capital-loss was dropped.

Dropped incident_location as it is unique and doesn't add much value to fraud_reported.

Saving the policy_number variable to a list and droping the variabe from data frame as it is a unique id for the policy and it doesn’t add much value to the target variable.

injury_claim+property_claim+vehicle_claim =total_claim. These variables contains amount information. Hence kept the total_claim and converted the three variables (injury_claim, property_claim, vehicle_claim) into categorical type codes i.e. if injury_claim >0 assign 1 else 0.


3.	Feature Selection

Applying correlation analysis (Heatmap) for numerical var we get to see that age and months_as_customer are highly correlated. (0.92).

Hence dropped the months_as_customer variable and converted the age variable into categorical type codes with following conditions below<20, 20-30, 30-40, 40-50, 50-60, 60-70.

Applied Chi-Sq-Test to eliminate insignificant categorical variables. The following categorical variables were taken and others were left out.

['insured_hobbies', 'incident_type', 'incident_severity', 'authorities_contacted', 'incident_state', 'fraud_reported']


4.	Down-sampling the imbalanced data to make it a balanced data set
Down sampled the data set using resample from sklearn.
0   - 400
1   - 247

5.	Model Building
Random Forest
Accuracy: 0.8307692307692308
Confusion matrix: [[110  22]
                                   [ 11  52]]

Decision Tree
Accuracy: 0.7487179487179487
Confusion matrix: [[108  24]
                                   [ 25  38]]

Logistic Regression
Accuracy: 0.6564102564102564
Confusion matrix: [[119  13]
                                    [ 54   9]]

Among the models, Randomn forest came with good accuracy, TP and TN rates


