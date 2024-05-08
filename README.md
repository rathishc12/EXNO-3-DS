## EX NO:3-Feature Encoding and Transformation



## NAME    : RATHISH KUMAR C
## ROLL NO : 212222100043


# AIM :
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM :
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING :
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation :
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT :
```
import pandas as pd
df=pd.read_csv("Encoding Data.csv")
df
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/5dc96622-b405-49e7-8e83-2bc97fa16b1c)

## ORDINAL ENCODING 
```
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
pm=['Hot','Warm','Cold']
e1=OrdinalEncoder(categories=[pm])
e1.fit_transform(df[["ord_2"]])
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/039c9db9-e1c4-4e8e-834a-02753e31bc32)
```
df['bo2']=e1.fit_transform(df[["ord_2"]])
df
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/8f23eed7-7115-4c7b-82be-f9ebe9a0eca3)

## LABEL ENCODING 
```
le=LabelEncoder()
dfc=df.copy()
dfc['ord_2']=le.fit_transform(dfc['ord_2'])
dfc
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/dac7bbcd-4692-4dd6-9a9d-92fc5ac8a231)

## ONEHOT ENCODER 
```
from sklearn.preprocessing import OneHotEncoder
ohe=OneHotEncoder(sparse=False)
df2=df.copy()
enc=pd.DataFrame(ohe.fit_transform(df2[['nom_0']]))
df2=pd.concat([df2,enc],axis=1)
df2
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/2aec88c7-5880-4bbf-b25d-75bf9182b43b)
```
pd.get_dummies(df2,columns=["nom_0"])
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/ccc51ab7-89cc-44c4-b6b3-07c22ac7dfa4)

## BINARY ENCODER 
```
pip install --upgrade category_encoders
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/5055492c-250f-4640-bca2-11fdcee5a08a)
```
from category_encoders import BinaryEncoder
df=pd.read_csv("data.csv")
df
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/91dc3619-7ab2-4239-a7fb-365ece990da1)
```
be=BinaryEncoder()
nd=be.fit_transform(df['Ord_2'])
dfb=pd.concat([df,nd],axis=1)
dfb
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/e55abfe4-59c7-46c2-9b52-10430069aa55)

## TARGET ENCODER
```
from category_encoders import TargetEncoder
te=TargetEncoder()
cc=df.copy()
new=te.fit_transform(X=cc["City"],y=cc["Target"])
cc=pd.concat([cc,new],axis=1)
cc
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/dd410324-c216-4cc6-bf3d-4f08aeff3baf)

## DATA TRANSFORMATION
```
import pandas as pd
from scipy import stats
import numpy as np
df=pd.read_csv('/content/Data_to_Transform.csv')
df
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/e3c93bb9-27b7-4476-9b59-d1493848255d)
```
df.skew()
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/79ee9981-6ceb-4383-a619-fb72b88ee84b)
```
np.log(df["Highly Positive Skew"])
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/159b9243-8a01-4415-a76d-cb4bf404929c)
```
np.reciprocal(df["Moderate Positive Skew"])
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/a21910bf-adee-4ed2-924e-a376b48d1d58)
```
np.square(df["Highly Positive Skew"])
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/949c4178-c93d-4203-8fcb-a59a998de342)
```
df["Highly Positive Skew_boxcox"], parameters=stats.boxcox(df["Highly Positive Skew"])
df
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/24d1baca-8790-4777-929f-a0a4ad17e391)
```
df["Moderate Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Moderate Negative Skew"])
df
```

![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/34702852-319b-4d95-960a-49a6b247b7cc)

```
df["Highly Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Highly Negative Skew"])
df.skew()
```
![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/a86cc4df-3fe4-4961-affd-ef345e6d5072)

```
import seaborn as sns
import statsmodels.api as sm
import matplotlib.pyplot as plt
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/2ca87cd1-ee7a-4e7a-b5eb-ca5e7a90bf45)

```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
plt.show()
```
![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/9df78fe1-5609-466e-9dcf-1a16582659fb)

```
sm.qqplot(df["Highly Negative Skew_1"],line='45')
plt.show()
```
![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/051dd119-ab74-411a-b2be-e827fdb86a4c)

```
dt=pd.read_csv("titanic_dataset.csv")
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
dt["Age_1"]=qt.fit_transform(dt[["Age"]])
sm.qqplot(dt['Age'],line='45')
plt.show()
```
![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/02648949-35aa-40ce-a9e3-35cba7ed88bd)

```
sm.qqplot(dt['Age_1'],line='45')
plt.show()
```
![image](https://github.com/23005529/EXNO-3-DS/assets/139842207/d816e32f-ef3f-488d-a506-71b87d583911)

# RESULT :

Finally, perform Feature Encoding and Transformation process is executed successfully.

       
