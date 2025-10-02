## Introduction
The objective is to develope machine learning models that accurately predict customer churn for a telecommunications company. The company wants to identify which customers are likely to
leave (churn) and target them with retention offers. 
## Exploratory Data Analysis (EDA)
The training and testing datasets were provided separately, with the training set containing 5,634 records and the test set containing 1,409 records, each consisting of 21 features. Initial exploratory data analysis was conducted to understand the distribution of the features, including statistical measures such as mean and standard deviation.
The TotalCharges column, which should be a numeric feature, was incorrectly stored as an object datatype. This issue was corrected by converting it to a float in both datasets.
In the training dataset, several missing values were identified: approximately 170 in gender and OnlineSecurity, 400 in MonthlyCharges, and 280 in TotalCharges. The test dataset had only 2 missing values in TotalCharges.

The distribution of the numerical features in the training dataset is illustrated in the figure below.

<img width="452" height="451" alt="download" src="https://github.com/user-attachments/assets/5f51b269-21e3-473d-95c5-83a22be236e4" />

and the correlation heat map is given below 

<img width="1056" height="830" alt="download" src="https://github.com/user-attachments/assets/64f4d43b-d419-4b54-8ad3-fe65fb0d3396" />

## Data Preprocessing
### Missing Values
* The missing values in Gender was filled using mode.
* For the missing values in OnlineService, the missing values which correspond to the No in Internet Service was given the value 'No Internet service'. the rest of the was filled using mode
* For MonthlyCharges and TotalCharges since their distributions where skewed the missing values where filled using median

### Outlier Treatment

<img width="839" height="836" alt="download" src="https://github.com/user-attachments/assets/15fb352b-0507-4f0e-b19b-3252c769d259" />

Since TotalCharges had outliers they were treated using winsorize technique

### Encoding 
* All the categorical features except Contract were encoded using LabelEncoder
* Contract was encoded using OrdinalEncoder as it represents ordered categories

### Scaling
Since all the numerical features exhibited a skewed distribution, Min-Max Scaling was initially applied. However, during model evaluation, Standard Scaling resulted in higher accuracy compared to Min-Max Scaling. Therefore, Standard Scaling was ultimately chosen for the final model.

## Feature Engineering
To capture the long-term revenue potential of each customer, a new feature called CustomerLifetimeValue was created.
This feature estimates the total amount a customer has contributed (or is expected to contribute) based on their tenure and average monthly charges.

## Model Building
Three machine learning models were implemented for churn prediction: Logistic Regression, Decision Tree, and Random Forest.
For the Decision Tree model, hyperparameter tuning was performed using Grid Search to identify the optimal configuration.
For the Random Forest model, manual tuning was conducted, and the best performance was achieved with the following parameters: n_estimators = 2500, max_depth = 15, min_samples_split = 10, min_samples_leaf = 10, max_features = 'log2', and random_state = 42

## Model Evaluation
* The Logistic Regression model demonstrated strong predictive performance, achieving an accuracy of 80.95% on the test dataset. with a weighted precision of 0.801, recall of 0.809, and an F1 score of 0.803, demonstrating reliable performance in predicting customer churn.
* The Decision Tree model achieved an accuracy of 79.10%, with a weighted precision of 0.781, recall of 0.791, and an F1 score of 0.784, indicating good performance in predicting customer churn.
* The Random Forest model achieved an accuracy of 81.09%, with a weighted precision of 0.801, recall of 0.811, and an F1 score of 0.803, demonstrating the best performance among the evaluated models for predicting customer churn.

## Conclusion
Among the three models evaluated for customer churn prediction, Random Forest achieved the highest accuracy (81.09%) and slightly better precision, recall, and F1 scores compared to Logistic Regression and Decision Tree.
