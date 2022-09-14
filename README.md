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

<img src="https://github.com/felipefvasconcelos/insurance_cross_sell/blob/main/assets/acumulative_gain.png" width="1200" height="500"><br>

The lift curve plot show us the percentage of the sample (customers) on the x-axis and the lift (propensity score / percentage of customers) in the y-axis. In other words, it shows us how better the model is compared to the state of art (random sortment) (i.e. in the XGBoost Classifier model, using the propensity score achived with the model, if we reach 20% of the customer we will find almost 3x more customer that answered yes to th survey than using random sortment.

<img src="https://github.com/felipefvasconcelos/insurance_cross_sell/blob/main/assets/lift_curve.png" width="1200" height="500"><br>

Also, we use K-top metrics to avaluate the performance and compare the results after doing the cross-validation.

Before cross-validation:

<img src="https://github.com/felipefvasconcelos/insurance_cross_sell/blob/main/assets/k_top_metrics.png" width="370" height="200"><br>

After cross-validation

<img src="https://github.com/felipefvasconcelos/insurance_cross_sell/blob/main/assets/k_top_metrics_cv.png" width="400" height="200"><br>

Based on the performance and overall memory usage, it was chosen the Gradient Boosting Classifier model for production

## 7. Business Results

### 7.1. Top Insights
* Focus on customers older than 36 years. 18% of customers older than 36 are interested in buying insurance, and only 7% of customers younger than 36 are interested.

* Focus on customers that had vehicle damaged. 24% of customers with damaged vehicle are interested vs 0.5% of customers whitout damage vehicle.

* Fucus on customers with vehicle older than 1 year. 29% of customers with vechicles older than 2 years and 17% of customers with vehicle age between 1 and 2 year are interested in buying insurance, while only 4% of customer with vehicle newer than 1 year are interested. PS: number of customers with vehicles within 1 to 2 years old is much greater.

### 7.2. Inferred Sales Results
* Considering a base of 68,600 customers, if you make 20,000 calls (29.15% of your base) you will reach 76.30% of customers interested. 

* Supposing each auto insurance is a 2,000 sale, if using random model (choose customer randomly) for 20,000 calls we would reach 29.65% of interested cusmoter, corresponding to 4,968,000 in sales.

* By using the Gradient Boosting model, with the same 20,000 calls we would reach 76.30% of interested customers, corresponding to 12,826,962 in sales.

* In other words, we would sell 7,858,962 more than calling customers randomly. This is an improved performance in a factor of 2.57.

## 8. Conclusion

The objective of this project was to simulate a real life business problem and address the solution using Machine Learning models. By using CRISP-DS methodoly, it was possible to build an organized structure in order to understand the business problem, analyse the data, test models and finally provide an accurate ranked list to maximize reaching customers with greater probability of buying the new product. 

## 9. Next Steps
Next step would be run a second cycle for CRISP-DM proccess with focus on following points:
* Create new and more relevant parameter at feature engineering.
* Create more hypotesis in order to find more relevant variables.
* Test more Machine Learning models.
* Test different methods to deal with imbalanced data.
<br>

---
## References:

* Datasets from [Kaggle](https://www.kaggle.com/datasets/anmolkumar/health-insurance-cross-sell-prediction)
* Blog [Seja um Data Scientist](https://sejaumdatascientist.com/os-5-projetos-de-data-science-que-fara-o-recrutador-olhar-para-voce/)
