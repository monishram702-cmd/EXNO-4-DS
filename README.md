# EXNO:4-DS
# AIM:
To read the given data and perform Feature Scaling and Feature Selection process and save the
data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Scaling for the feature in the data set.
STEP 4:Apply Feature Selection for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE SCALING:
1. Standard Scaler: It is also called Z-score normalization. It calculates the z-score of each value and replaces the value with the calculated Z-score. The features are then rescaled with x̄ =0 and σ=1
2. MinMaxScaler: It is also referred to as Normalization. The features are scaled between 0 and 1. Here, the mean value remains same as in Standardization, that is,0.
3. Maximum absolute scaling: Maximum absolute scaling scales the data to its maximum value; that is,it divides every observation by the maximum value of the variable.The result of the preceding transformation is a distribution in which the values vary approximately within the range of -1 to 1.
4. RobustScaler: RobustScaler transforms the feature vector by subtracting the median and then dividing by the interquartile range (75% value — 25% value).

# FEATURE SELECTION:
Feature selection is to find the best set of features that allows one to build useful models. Selecting the best features helps the model to perform well.
The feature selection techniques used are:
1.Filter Method
2.Wrapper Method
3.Embedded Method

# CODING :
```
 # Import Required Libraries
import numpy as np
import pandas as pd
from sklearn.preprocessing import StandardScaler, MinMaxScaler, MaxAbsScaler,␣
↪RobustScaler
#-----------------------------
# Feature Scaling using BMI.csv
#-----------------------------
# Load Dataset
df = pd.read_csv('Bmi.csv') # Make sure bmi.csv is in the same directory
print("Original Dataset:")
print(df.head())
# Handle Missing Values
df = df.dropna()
#-----------------------------
# 1. Standard Scaling
#-----------------------------
df_std = df.copy()
scaler_std = StandardScaler()
df_std[['Height', 'Weight']] = scaler_std.fit_transform(df_std[['Height',␣
↪'Weight']])
print("\nStandard Scaled Data:")
print(df_std.head())
#-----------------------------
# 2. Min-Max Scaling
#-----------------------------
df_minmax = df.copy()
1
scaler_minmax = MinMaxScaler()
df_minmax[['Height', 'Weight']] = scaler_minmax.
↪fit_transform(df_minmax[['Height', 'Weight']])
print("\nMin-Max Scaled Data:")
print(df_minmax.head())
#-----------------------------
# 3. MaxAbs Scaling
#-----------------------------
df_maxabs = df.copy()
scaler_maxabs = MaxAbsScaler()
df_maxabs[['Height', 'Weight']] = scaler_maxabs.
↪fit_transform(df_maxabs[['Height', 'Weight']])
print("\nMaxAbs Scaled Data:")
print(df_maxabs.head())
#-----------------------------
# 4. Robust Scaling
#-----------------------------
df_robust = df.copy()
scaler_robust = RobustScaler()
df_robust[['Height', 'Weight']] = scaler_robust.
↪fit_transform(df_robust[['Height', 'Weight']])
print("\nRobust Scaled Data:")
print(df_robust.head())
# Save scaled datasets
#df_std.to_csv("BMI_StandardScaled.csv", index=False)
#df_minmax.to_csv("BMI_MinMaxScaled.csv", index=False)
#df_maxabs.to_csv("BMI_MaxAbsScaled.csv", index=False)
#df_robust.to_csv("BMI_RobustScaled.csv", index=False)
print("\nFeature Scaling Completed Successfully.")
 #ImportRequiredLibraries
import numpy asnp
import pandas as pd
fromsklearn.feature_selectionimport SelectKBest,chi2,f_classif,RFE,␣
↪SelectFromModel
fromsklearn.model_selectionimport train_test_split
fromsklearn.ensembleimport RandomForestClassifier
fromsklearn.linear_modelimport LogisticRegression
fromsklearn.preprocessingimport MinMaxScaler
fromsklearn.metricsimport accuracy_score
#FisherScoreLibrary
#from skfeature.function.similarity_basedimportfisher_score
# Load Dataset
#-----------------------------
df = pd.read_csv("income(1) (1).csv")
print("Dataset Preview:")
print(df.head())
#-----------------------------
# Encode Categorical Variables
#-----------------------------
categorical_columns = ['JobType', 'EdType', 'maritalstatus', 'occupation',
'relationship', 'race', 'gender', 'nativecountry']
df[categorical_columns] = df[categorical_columns].astype('category').
↪apply(lambda x: x.cat.codes)
# Encode Target Variable if needed
if df['SalStat'].dtype == 'object':
df['SalStat'] = df['SalStat'].astype('category').cat.codes
#-----------------------------
# Separate Features and Target
#-----------------------------
X = df.drop(columns=['SalStat'])
y = df['SalStat']
#-----------------------------
# Scale Data for Chi-Square (Non-negative required)
#-----------------------------
scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(X)
#-----------------------------
# Filter Method: Chi-Square
#-----------------------------
selector_chi2 = SelectKBest(score_func=chi2, k=6)
selector_chi2.fit(X_scaled, y)
selected_features_chi2 = X.columns[selector_chi2.get_support()]
print("\nChi-Square Selected:", list(selected_features_chi2))
#-----------------------------
# Filter Method: ANOVA
#-----------------------------
selector_anova = SelectKBest(score_func=f_classif, k=5)
selector_anova.fit(X, y)
selected_features_anova = X.columns[selector_anova.get_support()]
print("\nANOVA Selected:", list(selected_features_anova))


```


# OUTPUT :

<img width="471" height="212" alt="Screenshot 2026-03-12 205919" src="https://github.com/user-attachments/assets/3ac5f85a-1671-436a-9999-d7ad64090df4" />
<img width="470" height="527" alt="Screenshot 2026-03-12 205932" src="https://github.com/user-attachments/assets/fb785ec4-d57f-4cbe-8d97-ceee84ebc869" />
<img width="445" height="198" alt="Screenshot 2026-03-12 205943" src="https://github.com/user-attachments/assets/8a0d7a98-c06e-47ba-81e3-9831d7af4aa9" />
<img width="506" height="712" alt="Screenshot 2026-03-12 205951" src="https://github.com/user-attachments/assets/e713cbff-f1d2-4822-be58-a6275a6e3fda" />
<img width="952" height="233" alt="Screenshot 2026-03-12 210002" src="https://github.com/user-attachments/assets/f7802180-3895-4926-bbfd-247302a613d9" />
<img width="881" height="891" alt="Screenshot 2026-03-12 210019" src="https://github.com/user-attachments/assets/7984bdac-c824-41a9-8620-f2e3016f3a64" />



       
# RESULT:

We  Successfully  read the given data and perform Feature Scaling and Feature Selection process and save thedata to a file.
