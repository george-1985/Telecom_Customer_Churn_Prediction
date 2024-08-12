# **Telecom Customer Churn Prediction**

## **Overview**

### **Business Problem**

In the highly competitive telecom industry, customer churn (the process of customers leaving one service provider for another) significantly impacts profitability. Given that acquiring a new customer costs 5-10 times more than retaining an existing one, reducing churn, especially among high-value customers, is crucial. This project aims to predict which customers are at high risk of churn and identify the main indicators of churn using customer-level data from a leading telecom firm.

### **Project Objective**

1. **Predict Churn:** Develop models to predict whether a high-value customer will churn in the near future.  
2. **Identify Indicators:** Identify key variables that are strong predictors of churn, helping the business understand why customers might leave.

## **Understanding and Defining Churn**

### **Types of Churn**

* **Revenue-Based Churn:** Customers not generating revenue through calls, SMS, or data usage.  
* **Usage-Based Churn:** Customers not using services (calls, internet, etc.) over a period of time.

### **Focused Definition for this Project**

* **Usage-Based Churn:** Defined as customers who have neither made calls nor used mobile internet during the churn phase.

### **High-Value Churn**

In this project, high-value customers are defined as those whose average recharge amount in the first two months is above the 70th percentile. Predicting churn for these customers is critical as they contribute the most to the company’s revenue.

## **Data Overview**

### **Dataset**

The dataset contains customer-level data spanning four consecutive months (June-September), encoded as months 6, 7, 8, and 9\.

### **Key Phases of Customer Lifecycle**

1. **Good Phase (Months 6 and 7):** The customer behaves as usual.  
2. **Action Phase (Month 8):** The customer starts exhibiting signs of churn.  
3. **Churn Phase (Month 9):** The customer churns (stops using services).

### **Data Dictionary**

The dataset includes various metrics such as total incoming and outgoing minutes of use (MOU), recharge amounts, and data usage. The data dictionary provides explanations for abbreviations like `loc` (local), `IC` (incoming), `OG` (outgoing), and `RECH` (recharge).

## **Data Preparation**

### **Key Steps**

1. **Feature Engineering:** Derived new features using business understanding to capture important indicators of churn.  
2. **Filtering High-Value Customers:** Selected customers with an average recharge amount in the first two months (6 and 7\) above the 70th percentile.  
3. **Tagging Churners:** Tagged customers as churners (1) or non-churners (0) based on their activity in month 9\.  
4. **Removing Churn Phase Data:** Discarded all data corresponding to the churn phase after tagging.

### **Handling Missing Data**

* Dropped columns with more than 50% missing values.  
* Imputed missing values based on logical assumptions (e.g., setting missing dates to the last date of the month).

### **Outlier Treatment**

* Capped the upper outliers at the 99th percentile.

### **Data Transformation**

* Converted categorical variables to dummy variables.  
* Standardized predictor columns (mean \= 0, standard deviation \= 1).

## **Exploratory Data Analysis (EDA)**

### **Key Insights**

* High churn likelihood for customers with declining revenue and usage patterns.  
* Churners typically exhibit a decrease in call and data usage in the action phase (month 8).  
* Significant predictors include the number of recharges, local incoming and outgoing calls, and data usage patterns.

## **Modelling**

### **Model 1: Logistic Regression with RFE & Manual Elimination**

* **Purpose:** Identify key predictors of churn.  
* **Important Predictors:**  
  * `loc_ic_t2f_mou_8`: Local incoming calls from fixed lines.  
  * `total_rech_num_8`: Total number of recharges in month 8\.  
  * `monthly_2g_8_0` and `monthly_3g_8_0`: Usage of 2G and 3G monthly packages.

### **Model 2: PCA \+ Logistic Regression**

* **Train Performance:**  
  * Accuracy: 0.627  
  * Recall: 0.918  
* **Test Performance:**  
  * Accuracy: 0.086  
  * Recall: 1.0  
* **Comments:** High sensitivity but poor precision on test data.

### **Model 3: PCA \+ Random Forest Classifier**

* **Train Performance:**  
  * Accuracy: 0.882  
  * Recall: 0.816  
* **Test Performance:**  
  * Accuracy: 0.86  
  * Recall: 0.80  
* **Comments:** Balanced performance, better generalization.

### **Model 4: PCA \+ XGBoost**

* **Train Performance:**  
  * Accuracy: 0.873  
  * Recall: 0.887  
* **Test Performance:**  
  * Accuracy: 0.086  
  * Recall: 1.0  
* **Comments:** Similar to Model 2, with high sensitivity but poor precision.

## **Evaluation Metrics**

### **Key Metrics**

* **Accuracy:** Overall correctness of the model.  
* **Sensitivity (Recall):** Ability to correctly identify churners.  
* **Specificity:** Ability to correctly identify non-churners.  
* **Precision:** Proportion of true positives among predicted positives.  
* **F1-Score:** Harmonic mean of precision and recall.

## **Recommendations**

### **Key Findings**

* **Strongest Churn Indicators:**  
  * Lower local incoming calls from fixed lines.  
  * Fewer recharges in month 8\.  
  * Usage of monthly 2G/3G packages in month 8\.

### **Business Recommendations**

1. **Target Customers with Declining Usage:** Focus on customers showing a drop in local incoming calls and fewer recharges in month 8\.  
2. **Use Models with High Sensitivity:** Implement the PCA \+ Logistic Regression model for predicting churn due to its high sensitivity.

## **Conclusion**

This project demonstrates the importance of predictive modelling in identifying high-risk customers and suggests actionable strategies for reducing churn. By focusing on key indicators and using appropriate models, telecom companies can proactively retain their high-value customers, thereby reducing revenue leakage.

## **Future Work**

### **Potential Improvements**

* **Further Model Tuning:** Experiment with other machine learning algorithms and hyperparameter tuning to improve performance.  
* **Real-Time Churn Prediction:** Implement a real-time system to predict churn and take immediate corrective actions.

