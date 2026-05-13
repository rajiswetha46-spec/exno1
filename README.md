<img width="758" height="580" alt="Screenshot 2026-05-13 161942" src="https://github.com/user-attachments/assets/c6caf9b5-d4c7-4c93-990c-d00f3b2d5f40" /># Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output:
```
import pandas as pd
import numpy as np
import seaborn as sns
import scipy.stats as stats
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import seaborn as sns
import scipy.stats as stats
import matplotlib.pyplot as plt

# Read dataset
df = pd.read_csv("SAMPLEIDS.csv")
df
df.head()
df.tail()
df.info()
df.describe()
df.isnull().sum()
df.isnull().any()

df.dropna()
df.fillna(0)
df.fillna(method='ffill')
df.fillna({'GENDER':'MALE','NAME':'SRI'})
```
<img width="447" height="427" alt="Screenshot 2026-05-13 161622" src="https://github.com/user-attachments/assets/f2847b84-5fdc-40fe-acef-fa393de55a41" />
<img width="1002" height="745" alt="Screenshot 2026-05-13 161633" src="https://github.com/user-attachments/assets/6b26f562-7759-4d16-96e8-506dae2643f5" />

```
# Iris dataset
ir = pd.read_csv("iris.csv")
ir
ir.describe()
```
<img width="502" height="307" alt="Screenshot 2026-05-13 161832" src="https://github.com/user-attachments/assets/9859c264-7126-46c8-aa9d-6b97aafa3524" />


```
import pandas as pd
 #BOXPLOT BEFORE OUTLIER REMOVAL 
sns.boxplot(x='sepal_width', data=ir)
plt.title("Boxplot Before Removing Outliers")
plt.show()
```
<img width="702" height="593" alt="Screenshot 2026-05-13 161841" src="https://github.com/user-attachments/assets/7c48375f-655b-4d7f-9b48-1c8f68b475c0" />


```
#SCATTER PLOT BEFORE CLEANING 
ir.plot.scatter(x='sepal_length', y='sepal_width', title="Before Removing Outliers")
plt.show()
```

<img width="721" height="587" alt="Screenshot 2026-05-13 161850" src="https://github.com/user-attachments/assets/39724761-9db4-4a90-ae5b-691e78d05708" />


```
# IQR METHOD
Q1 = ir.sepal_width.quantile(0.25)
Q3 = ir.sepal_width.quantile(0.75)
IQR = Q3 - Q1
print(IQR)
```

<img width="122" height="37" alt="Screenshot 2026-05-13 161907" src="https://github.com/user-attachments/assets/8794c295-0492-4cd9-bc93-cba49ebfdd53" />


```
# Outliers
ran = ir[((ir.sepal_width < (Q1 - 1.5 * IQR)) | (ir.sepal_width > (Q3 + 1.5 * IQR)))]
ran['sepal_width']

# Remove outliers
ran = ir[~((ir.sepal_width < (Q1 - 1.5 * IQR)) | (ir.sepal_width > (Q3 + 1.5 * IQR)))]
ran['sepal_width']
```


<img width="486" height="273" alt="Screenshot 2026-05-13 161915" src="https://github.com/user-attachments/assets/67e2e2b5-da00-4178-b010-d8cee7631053" />


```
#  BOXPLOT AFTER IQR 
sns.boxplot(x='sepal_width', data=ran)
plt.title("Boxplot After IQR")
plt.show()

# SCATTER AFTER IQR 
ran.plot.scatter(x='sepal_length', y='sepal_width', title="After IQR Outlier Removal")
plt.show()
```


<img width="781" height="603" alt="Screenshot 2026-05-13 161932" src="https://github.com/user-attachments/assets/202bda56-d850-482b-be5d-7f6edeaf5f6e" />



```
# Z-SCORE METHOD
z = np.abs(stats.zscore(ir['petal_length']))
z

ir1 = ir[z < 3]
ir1

# SCATTER AFTER Z-SCORE
ir1.plot.scatter(x='petal_length', y='petal_width', title="After Z-score Outlier Removal")
plt.show()
```


<img width="758" height="580" alt="Screenshot 2026-05-13 161942" src="https://github.com/user-attachments/assets/e3d8b0c7-d8f8-435f-9377-16eccd3a9cc8" />



# Result:
The given data has been successfully read, cleaned by handling duplicates and missing values, and saved to a new file named cleaned_data.csv.

