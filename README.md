# insurance_cross_sell

This repository contains all steps based on CRISP-DS process model methodology to create a classification model to help a large insurance company to maximize sales of a new product. The data used in this repos is available ar the [Health Insurance Cross Sell Prediction](https://www.kaggle.com/datasets/anmolkumar/health-insurance-cross-sell-prediction) at Kaggle.

All information below is fictional.

## 1. Business Problem

The insurance company currently offers only health insurance to its customers, and, in order to increase the incomes, it wants to offer a new product: a vehicle insurance.

To understand the interest of the customers in buying this new product, the company performed a survey with its customer base and recorded the answer for each customer. However, even though more than 350k customers have answered the survey, there are still more than 120k customers the company doesn't know if they are interested or not.

Since the company has limited resources to reach the customer base (by call, by message, by email, etc.), the challenge is to use the available resources to reach the maximum number of customers that will buy the new product.

Therefore, this project aims to create a classification model that will rank the customers according to their propensity to buy the new product, based on previously made survey.

## 2. Data

The data used in this project can be found at:<br>
https://www.kaggle.com/datasets/anmolkumar/health-insurance-cross-sell-prediction
<br>

<details><summary>Click here to see the original attibutes table</summary><br>
  
Attribute | Definition
------------ | -------------
|id|Unique ID for the customer|
|Gender | Gender of the customer|
|Age|Age of the customer)|
|Driving_License|0 : Customer does not have DL, 1 : Customer already has DL|
|Region_Code|Unique code for the region of the customer|
|Previously_Insured|1 : Customer already has Vehicle Insurance, 0 : Customer doesn't have Vehicle Insurance|
|Vehicle_Age|Age of the Vehicle|
|Vehicle_Damage|1 : Customer got his/her vehicle damaged in the past. 0 : Customer didn't get his/her vehicle damaged in the past|
|Annual_Premium|The amount customer needs to pay as premium in the year|
|PolicySalesChannel|Anonymized Code for the channel of outreaching to the customer ie. Different Agents, Over Mail, Over Phone, In Person, etc.|
|Vintage|Number of Days, Customer has been associated with the company|
|Response|1 : Customer is interested, 0 : Customer is not interested|
</details>

## 3. Business Assumptions

* Customers that aswered yes (1) in the columns<i>"Response"</i> are highly likely to buy the vehicle insurance.
* Customers that aswered no (0) in the columns<i>"Response"</i> are definitely not a buy.
* The company has resources to make from 20,000 to 40,000 calls.
* Each sell will correspond to a monetary value of 2,000 of the currency in the data (there is no information on the currency)

## 4. Solution Strategy

1. Data Description Analysis
2. Feature Engineering
3. Data Filtering
4. Exploratory Data Analysis
5. Data Preparation
6. Feature Selection
7. Machine Learning Modeling 
8. Hyperparameter Fine Tuning
9. Understand Model Performance
10. Deploy

## 5. Tools and Machine Learning Models

* Python 3.9.12
* Extra Trees Classifier as feature selector
* Logistic Regression
* KNeighbors Classifier (KNN)
* Gradiant Boosting Classifier
* Random Forest Classifier
* XGBoost Classifier

## 6. Models Performance

In order to understing the learn to rank performance, it was plotted the cumulative gain and the lift curve.

The cumulative gain plot shows us the percentage of the sample (customers) on the x-axis and the percentage cumulative gain (response) in the y-axis. In other words, it shows us the cumulative gain percentage of custormers that answered yes to the survey when ordered by propensity score achived with the model from highest to lowest propensity (i.e. in the XGBoost Classifier model, the first 20% of customers listed by propensity score corresponds to almost 60% of customers that answered yes in the survey).




The image below shows values of MAE (Mean Absolute Error), MAPE (Mean Absolute Percentage Error) and RMSE (Root-Mean_Square Deviation) for each model after performing Cross-Validation.

<img src="https://github.com/felipefvasconcelos/Rossman_Sales_Prediction/blob/main/assets/cross_val.png" width="500" height="150"><br>

Even though Random Forest Regressor model presented a slightly better performance, it was decided to proceed with XGBoost Regressor model because of the signicant lower memory and time consuming.

After running hyperparameter fine tuning for XGBoost Regressor model, the final performance was found as showed below.

<img src="https://github.com/felipefvasconcelos/Rossman_Sales_Prediction/blob/main/assets/final_performance.png" width="300" height="50"><br>

Error (real sales - prediction) scatter plot:

<img src="https://github.com/felipefvasconcelos/Rossman_Sales_Prediction/blob/main/assets/error.png" width="600" height="275"><br>

## 7. Business Results

According to the model, in the next six weeks all stores together will sell R$ 285,047,136.00. Assuming the error found after running fine tuning, we can assume that the stores will sell R$ 284,322,899.11 in the worst case scenario and R$ 285,771,403.20 in the best case scenario.

<img src="https://github.com/felipefvasconcelos/Rossman_Sales_Prediction/blob/main/assets/Scenarios.png" width="300" height="150"><br>

## 8. Telegram Bot

It was created a Telegram Bot in order to easily accesss predictions for individual stores by texting the store number you want the see the sales prediction. Bot can be accessed at https://t.me/rossmann_ffv_bot.

## 9. Conclusion

The objective of this project was to simulate a real life business problem and address the solution using Machine Learning models. By using CRISP-DS methodoly, it was possible to build an organized structure in order to understand the business problem, analyse the data, test models and finally provide an accurate sales predictions for the stores. 

## 10. Next Steps
Next step would be run a second cycle for CRISP-DM proccess with focus on following points:
* Create new and more relevant parameter at feature engineering.
* Create more hypotesis in order to find more relevant variables.
* Test more Machine Learning models.
* Improve messages in the Telegram Bot.
<br>

---
## References:

* Datasets Rossmann Store Sales from [Kaggle](https://www.kaggle.com/competitions/rossmann-store-sales/data)
* Variables meaning on [Kaggle discussion](https://www.kaggle.com/competitions/rossmann-store-sales/overview)
* Blog [Seja um Data Scientist](https://sejaumdatascientist.com/os-5-projetos-de-data-science-que-fara-o-recrutador-olhar-para-voce/)
