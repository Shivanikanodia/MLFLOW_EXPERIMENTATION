## Workforce Attrition Prediction with Explainable and Reproducible ML

Predicting Employee churn and identifying key drivers of attrition using scalable machine learning practices. 
Built with classification and booster algorithms. Used Unity Catalog to store models and features, and MLflow for experiment tracking, model reproducibility and transparency.

---

### Problem Statement:

This project focuses on predicting which employees are most likely to leave, store the important predictors from feature selection in Unity Catalog for Business to use it later for comparison and decisions.  By leveraging machine learning models, MLflow and  SHAP  the goal is to empower HR teams with proactive insights—helping them improve retention through monitoring model metrics. 

## ML pipeline covering:

**Data Management with Unity Catalog (secure and versioned Delta tables)**

**Data Cleaning and Collection** 

**Exploratory Data Analysis**

**Data Preprocessing (Data Transformation and Feature Selection using Chi-Square and T-test)**
  
**Model training, testing with Logistic Regression, Random Forest XGBoost and Evaluation**

**Model monitoring and tracking using MLflow (parameters, metrics, artifacts, comparison).**

---

### Dataset Overview:

-  Attributes :Demographics, Job Role, Job Satisfaction levels and Performance metrics. 
-  Checked Unique values in each category to see frequency of different categories and its distribution.
-  Identified missing values and empty strings using insull.sum().
-  Features such as Distance from Home, Monthly Income, Years at Company, Years Since Last Promotion, and Total Working Years show right-skewed distributions, with most values concentrated on the lower end. Used log1p for transformation. 
  
---

### Unity Catalog & Access Control:

Created a Catalog (`ml_catalog`) and schema (`ml_schema`) under a managed volume to store both the complete dataset and the training subset in Delta format. This structure enables governed, scalable, and versioned access to data for the ML workflow.

---

## FEATURE SELECTION:

Capture attrition trends (Based on Demographics, Career Trajectory, Growth Opportunites and Organisation Culture). 
The t-test and chi-square analyses were conducted to examine relationships between various features and employee attrition.

___

## MODEL SELECTION:

- Logistic regression with L1 and L2 Penality, and class weight balanced to account for coefficents and features.
- Random forest classiffier with hyperparamters like max_depth, n_estimators which will help us to generalize well, and deal with variance and overfitting. 
- Xgboost Classifier to deal with complex data points. 

---

## 🚀 Model Experimentation using MLFLOW

Setting the Experimentation inside Databricks Notebook. 

<img width="1039" alt="Experimentation" src="https://github.com/user-attachments/assets/a927d8d0-5ea7-4e53-8365-fdb842b5bd62" />

This centralized tracking ensured experiment reproducibility and logging Hyperparameter from models, metrics, artifacts and model versioning. 
Logged key hyperparameters, evaluation metrics, trained model and visual artifacts like confusion matrix for every run — making it easy to reproduce or explain later.

---

### MLFLOW METRICS AND DASHBOARD:  

As we can see screenshot below from Databricks MLFlow UI with Run Name, Duration of each Run and metrics logged.  Used the MLflow UI in Databricks to compare multiple runs of Logistic Regression, Random Forest, and XGBoost. 

<img width="1264" height="440" alt="Screenshot 2025-10-07 at 11 25 24" src="https://github.com/user-attachments/assets/1ef7910e-319a-4d11-9ffd-5691308bcfb8" />

Each dashboard recorded: adjusted_f1, adjusted_precision, adjusted_recall, precision, recall and f1 score. 

<img width="908" height="363" alt="Screenshot 2025-10-07 at 07 30 50" src="https://github.com/user-attachments/assets/fcd14556-35a6-40a7-a289-db8e17fb9729" />

<img width="928" height="362" alt="Screenshot 2025-10-07 at 07 31 20" src="https://github.com/user-attachments/assets/f5446022-0a39-4c09-98ee-10de40d85eda" />

---

### MODEL SERVING AND REGISTRY: 

Registered model using Model Registry in databricks to serve it later for deployment for making real time predictions. Provided signatures examples to be used by registered and served model for making predictions at endpoint in JSON format. 

<img width="632" height="227" alt="Screenshot 2025-10-18 at 20 46 12" src="https://github.com/user-attachments/assets/30af9741-4000-4161-b440-9446459431aa" />

---

### Conclusion:

- After evaluating multiple models—including Logistic Regression, Xgboost and Random Forest (with maximum depth of 6 and n_estimators of 200) emerged as the best-performing model for our attrition prediction task. With a tuned threshold of 0.33, it struck an effective balance between interpretability, performance, and generalization. 
- The model achieved a recall of 82% and precision of 70% on detecting attrition, which is crucial for early risk detection while minimizing false positives that may harm employee trust.
- Unity Catalog ensures secure, governed, and scalable data access.
- SHAP explainability provides transparency into model decisions.
- MLflow ensures experiment reproducibility, loggging and tracking for deployment.
  
---

### HIGH RISK FACTORS FROM MODEL AND RECOMMENDATIONS TO HR TEAMS: 

- Overtime, Low job satisfaction and Poor work-life balance - Monitor satisfaction & workload monthly.
- Employees with long commutes or frequent travel - Enable flexible work or hybrid policies.
- Employees with limited growth, low income or recognition  - Design retention bonuses or stock options.
   
--- 

### Future Scope:

- Automating retraining via Databricks Jobs and retraining with 50,000 row making inference on Production level data. 
- AI Agent for Attrition Predictions, giving alerts on employee sentiments and recommending strategies. 

---

### Tech Stack:

- **Languages**: Python  
- **Libraries**: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`, `mlflow`, `shap`  
- **Platform**: Databricks  
- **Version Control & Tracking**: MLflow. 
  
---

### 📁 Clone the repository
git clone https://github.com/<ShivaniKanodia>/employee-attrition-mlpipeline.git
cd employee-attrition-mlpipeline

### 📦 Install Python dependencies
pip install -r requirements.txt
