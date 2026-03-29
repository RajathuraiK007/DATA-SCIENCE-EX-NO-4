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

# CODING AND OUTPUT:

```
import pandas as pd
from sklearn.preprocessing import StandardScaler, MinMaxScaler, MaxAbsScaler, RobustScaler
df=pd.read_csv("C:\\Users\\G.POORNIMA DEVI\\Downloads\\bmi.csv")
sclr=MinMaxScaler()
df['Height_scaled_minmax']=sclr.fit_transform(df[['Height']])
df
```

<img width="1313" height="627" alt="image" src="https://github.com/user-attachments/assets/9051a347-7006-4b77-aef3-f0b97c02175a" />

```
scl=RobustScaler()
df['Weight_scaled_robust']=scl.fit_transform(df[['Weight']])
df
```

<img width="1396" height="549" alt="image" src="https://github.com/user-attachments/assets/bef91538-c02b-42f3-8acd-cf8e798654d1" />

```
scale=MaxAbsScaler()
df['Height_scaled_maxabs']=scale.fit_transform(df[['Height']])
df
```

<img width="1356" height="553" alt="image" src="https://github.com/user-attachments/assets/ab407787-6dd8-4536-9ae9-280053ff2294" />

```
scaler=StandardScaler()
df['Weight_scaled_std']=scaler.fit_transform(df[['Weight']])
df
```

<img width="1318" height="564" alt="image" src="https://github.com/user-attachments/assets/f2bffe59-01ea-4bbf-9950-780bbe30c6e3" />


```
#Filter Selection
import pandas as pd
from sklearn.feature_selection import SelectKBest, chi2
from sklearn.preprocessing import LabelEncoder, MinMaxScaler
df=pd.read_csv("C:\\Users\\G.POORNIMA DEVI\\Downloads\\bmi.csv")
df['Gender_encoded']=encoder.fit_transform(df['Gender'])
X=df.drop(['Gender','Gender_encoded'],axis=1)
y=df['Gender_encoded']
scaler=MinMaxScaler()
X_scaled=scaler.fit_transform(X)
selector=SelectKBest(score_func=chi2,k=2)
selector.fit_transform(X_scaled,y)
print(X.columns[selector.get_support()].tolist())
```

<img width="1374" height="306" alt="image" src="https://github.com/user-attachments/assets/5251e3f7-3125-4ebc-8dd8-fc1afd3f0d4a" />

```
#Wrapper Selection
import pandas as pd
from sklearn.linear_model import LogisticRegression
from sklearn.feature_selection import RFE
from sklearn.preprocessing import LabelEncoder

df=pd.read_csv("C:\\Users\\G.POORNIMA DEVI\\Downloads\\bmi.csv")
le=LabelEncoder()
df['Gender_encoded']=le.fit_transform(df['Gender'])
X=df.drop(['Gender','Gender_encoded'],axis=1)
y=df['Gender_encoded']

model=LogisticRegression()
rfe=RFE(estimator=model, n_features_to_select=2)
rfe.fit(X,y)
Wrapper_cols=X.columns[rfe.support_].tolist()
print(Wrapper_cols)
```

<img width="1346" height="382" alt="image" src="https://github.com/user-attachments/assets/ea6a67ca-65cf-41e0-b77e-d4ee6691c911" />

```
#Embedded Method
import pandas as pd
from sklearn.preprocessing import LabelEncoder, StandardScaler
from sklearn.linear_model import Lasso

df=pd.read_csv("C:\\Users\\G.POORNIMA DEVI\\Downloads\\bmi.csv")

le=LabelEncoder()
df['Gender_encoded']=le.fit_transform(df['Gender'])

X=df.drop(['Gender','Gender_encoded'],axis=1)
y=df['Gender_encoded']

scaler=StandardScaler()
X_scaled=scaler.fit_transform(X)

lasso=Lasso(alpha=0.01)
lasso.fit(X_scaled,y)

importance = pd.Series(lasso.coef_, index=X.columns)
selected=importance[importance!=0].index.tolist()
print(selected)
```

<img width="1342" height="483" alt="image" src="https://github.com/user-attachments/assets/fafc1470-10ae-4719-bd10-c18a473b0431" />


# RESULT:

