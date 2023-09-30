![Multivariate Visualization for Numeric Features](https://github.com/SamarKri/Project-2/assets/136517111/b1039963-e6ed-4640-816c-90ec24440ad2)
![Multivariate Visualization for Categorical Features](https://github.com/SamarKri/Project-2/assets/136517111/6f743408-6f1b-4671-913a-499512381ea2)
# Healthcare Prediction

## Author : 
Samar Krimi

## Business Problem :
A healthcare prediction to predict whether a patient is likely to get stroke. Stroke can be very hard to predict and therefore try to hinder, because it is the result of many different pathophysiologies.

## Source of data : 
healthcare-dataset-stroke-data.csv
Here is the link for where the data is found from kaggle: https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset
  
## Attribute Information :
1) id: unique identifier
2) gender: "Male", "Female" or "Other"
3) age: age of the patient
4) hypertension: 0 if the patient doesn't have hypertension, 1 if the patient has hypertension
5) heart_disease: 0 if the patient doesn't have any heart diseases, 1 if the patient has a heart disease
6) ever_married: "No" or "Yes"
7) work_type: "children", "Govt_jov", "Never_worked", "Private" or "Self-employed"
8) Residence_type: "Rural" or "Urban"
9) avg_glucose_level: average glucose level in blood
10) bmi: body mass index
11) smoking_status: "formerly smoked", "never smoked", "smokes" or "Unknown"*
*Note: "Unknown" in smoking_status means that the information is unavailable for this patient
12) stroke: 1 if the patient had a stroke or 0 if not
  
## Data Description : 
This is a healthcare dataset used to predict whether a patient is likely to get stroke based on the input parameters like gender, age, various diseases, and smoking status. Each row in the data provides relavant information about the patient. This is a binary classification problem.
There are 2 possible classes : predict stroke (target): 1 if the patient had a stroke or 0 if not. These classes are highly unbalanced.
The data contains 12 attributes (columns or features) and 5110 observations (rows), each row represents a specific patient. 

## Exploratory Data Analysis :

### Numeric Feature Inspection :

![Sans titre](https://github.com/SamarKri/Project-2/assets/136517111/c37d16c0-6170-4577-9ed2-1ccfa4d10fc2)

#### Observations :

- For bmi Feature vs. Target :

I would expect this feature to be a classificator of the target: I think it's important to know about its body mass index to avoid certain diseases due to obesity.

This feature doesn't appear to be a classificator of the target because it has a very low correlation with it, diagnosis based on body mass index is not very relevant to determine if the patient will have a stroke.

- For age Feature vs. Target :

I would expect this feature to be a classificator of the target: I think stroke increases with age, patients who are more than 45 are most likely to develop a stroke.

This feature doesn't appear to be a classificator of the target because it has a low correlation with it.

- For avg_glucose_level vs. Target Observations:

I would expect this feature to be a classificator of the target: I think it's important to know about its average glucose level in blood to avoid diabetes which is a serious chronic disease, the most important Average glucose level in blood is between 60 and 100.

This feature doesn't appear to be a classificator of the target because it has a very low correlation with it.


### Categorical Feature Inspection :

![Sans titre-1](https://github.com/SamarKri/Project-2/assets/136517111/48b9e494-08ae-4f76-943b-f9e932c32463)

#### Observations : 

- gender {Male, Female} : Stroke targets male patients more than females.
  
hypertension {0 if the patient doesn't have hypertension, 1 if the patient has hypertension} : If the patient does not have hypertension, he has a great chance to avoid stroke.

- heart_disease {0 if the patient doesn't have any heart diseases, 1 if the patient has a heart disease} : If the patient doesn't have cardiovascular disease, he's more likely to avoid stroke.
  
- ever_married {No or Yes} : Patients who haven't been married in their lives will be spared by the stroke.
  
- work_type {children, Govt_jov, Never_worked, Private or Self-employed} : patients that Never_worked are undiagnosed, children don't have a stroke, Patients who have - private jobs are more likely to develop stroke than self_employed or patient with govermental jobs, may be they are more stressed by their work schedules.
  
- Residence_type {Rural, Urban} : Urban life induce stroke more than rural life.
  
- smoking_status {formerly smoked, never smoked, smokes or occasional smoker}: patients how have never smoked are more likely to be spared from stroke although in some cases related to life quality they may develop stroke.

## Model Developpement
We will evaluate 4 types of Models on train & test data with Classification Report, Normalized Confusion Matrix & ROC curves :
2 Sequential Models :
        LGBMClassifier
        XGBClassifier

2 Ensemble Sequential Models :
        ensemble.AdaBoostClassifier
        ensemble.GradientBoostingClassifier

2 Linear Models :
        linear_model.LogisticRegression
        linear_model.SGDClassifier

2 Ensemble Parallel Models :
        ensemble.BaggingClassifier
        ensemble.RandomForestClassifier

--> for LGBMClassifier & XGBClassifier, I will evaluate the default models without any regularization.
--> for AdaBoostClassifier & GradientBoostingClassifier, I will tunned some hyperparameters with RandomizedSearchCV.
--> for LogisticRegression & SGDClassifier, I will use Class Weights to tell the relative importance of each class, using class_weight='balanced'.

## Best Model 
LGBMClassifier & XGBClassifier are the best predictive models for stroke target we choose LGBMClassifier because it detects highly FN=0.94 (the most problemetic) with AUC=0.82 on test set and perfect AUC=1 on train set.
![image](https://github.com/SamarKri/Project-2/assets/136517111/da462f05-9b08-4832-ad64-190204ec3369)

![Sans titre](https://github.com/SamarKri/Project-2/assets/136517111/18d21984-f2b0-4b55-9bbf-e69262c89261)

![Sans titre-1](https://github.com/SamarKri/Project-2/assets/136517111/7da09430-44cd-4544-b4fc-414f4a022b1f)

## Recommendations :
My "production" model is LGBMClassifier that will be tunned with RandomizedSearchCV & Regularized by Ridge/Lasso/ElasticNet in order to improve the model classification performance.

- Stroke targets male patients more than females. They must check frequently their high blood pressure, get treated early if they have cardiovascular disease or get tested regularly, stop smoking, avoid conflicts between spouses and stressful jobs, explore rural life more often and have healthy life quality.
