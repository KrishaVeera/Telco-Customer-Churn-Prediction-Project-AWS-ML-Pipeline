# Telco-Customer-Churn-Prediction-Project-AWS-ML-Pipeline

This project focuses on building a **customer churn prediction model** using **AWS services** for **data storage, processing, and machine learning**. The goal is to identify key factors influencing churn and develop a predictive model to assist businesses in **retaining customers**.

**Step 1: Create an IAM User**

To ensure **secure access** to AWS resources, an IAM user with the necessary permissions was created. Policies were assigned to allow interactions with **S3, Glue, and SageMaker**.

**Step 2: Set Up S3 Storage**

An **S3 bucket** was created to store the raw dataset (`WA_Fn-UseC_-Telco-Customer-Churn.csv`). This dataset contained **7,043 customer records** with **21 attributes** related to customer demographics, service subscriptions, and billing details.

**Step 3: Data Cleaning & Transformation Using AWS Glue ETL**

To preprocess the data, an **AWS Glue Crawler** was used to catalog the dataset. Then, an **AWS Glue ETL job** (Visual ETL) was created to:

- Remove null values.
- Ensure consistent data formatting.
- Convert categorical features into structured formats.
- Save the cleaned dataset back to **S3** in **CSV format**.

![image.png](attachment:91084a2b-fb65-47a3-a3b8-59e9a07f9551:image.png)

**Step 4: Use AWS Glue DataBrew**

AWS Glue DataBrew was used for **data exploration and validation**, allowing for:

- Data profiling to detect **missing values, outliers, and inconsistencies**.
- Validation of data transformations applied in **AWS Glue ETL**.
- Ensuring the dataset was ready for machine learning.

![image.png](attachment:1456e795-5852-43bf-97aa-0ee0d14a9526:image.png)

![image.png](attachment:170cb07c-1543-49c9-8d50-e8b2eb6cfb14:image.png)

**Step 5: Use AWS SageMaker for Machine Learning**

![image.png](attachment:df74c872-93de-4dc9-a473-3f7c6329fb22:image.png)

### **Model Training Process**

AWS SageMaker was used to **develop and train churn prediction models**:

1. **Data Loading** – The cleaned CSV file was imported from **S3** into a SageMaker Jupyter Notebook.
2. **Data Preprocessing** – Categorical features were encoded using **one-hot encoding**.
3. **Feature Scaling** – Numeric features were **normalized** to improve model performance.
4. **Handling Class Imbalance** – **SMOTE (Synthetic Minority Over-sampling Technique)** was applied to balance churn labels.
5. **Model Selection & Training** – Four models were trained:
    - **Logistic Regression**
    - **Random Forest**
    - **XGBoost**
    - **SMOTE Logistic Regression**

The jupyter notebook can be found here: 

**Step 6: Test Model & Performance Analysis**

Models were evaluated using **accuracy, precision, recall, and F1-score**.

![image.png](attachment:cc2915d3-1485-4f42-9375-d3c79a021eaf:image.png)

**SMOTE Logistic Regression performed best for detecting churners** with the highest **recall (0.78)**. This means it is best at identifying customers likely to churn.
**XGBoost provided a balance** between precision and recall, useful for reducing false alarms.
**Logistic Regression (without SMOTE) had the highest accuracy (0.82)** but missed many churners.

**Confusion Matrix Analysis**

The confusion matrix from the best model (SMOTE Logistic Regression) shows:

- **83 false negatives (missed churners)**
- **258 false positives (customers predicted to churn but stayed)**
- **290 true positives (correctly identified churners)**
- **778 true negatives (correctly identified non-churners)**

**Step 7:** **Understanding Insights & Business Recommendations**

![image.png](attachment:ae3eb1d1-d944-4a49-ab78-ce1569d4fec9:image.png)
