# Exno:1
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

# Coding and Output
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS (1).csv")
df
```
![Screenshot 2025-05-01 224954](https://github.com/user-attachments/assets/909d2869-42ff-4994-995c-968875135ad5)

```
df.info()
```
![Screenshot 2025-05-01 224935](https://github.com/user-attachments/assets/f883c056-adbd-48ef-a05b-3ab47313b8af)

```
df.describe()
```
![Screenshot 2025-05-01 224928](https://github.com/user-attachments/assets/6e4f6ce5-c74e-4924-b858-8bfeb1986a6f)

```
df.shape
```
![Screenshot 2025-05-01 224925](https://github.com/user-attachments/assets/bbc92bb8-87f0-465a-b194-2f0082aad9b1)

```
df.shape[0]
```
![Screenshot 2025-05-01 224919](https://github.com/user-attachments/assets/b560ac21-8bda-435a-a7d9-8e2cb493ce15)

```
df.isnull()
```
![Screenshot 2025-05-01 224914](https://github.com/user-attachments/assets/ca57e398-1dc4-4070-8ae2-5d67f37bd186)

```
df.notnull()
```
![Screenshot 2025-05-01 224906](https://github.com/user-attachments/assets/c05a4e22-dc47-4a4b-b8bd-6ed45c4d03cf)

```
df.dropna(axis=1)
```
![Screenshot 2025-05-01 224858](https://github.com/user-attachments/assets/083dd278-4178-45ff-9ff3-1aca59b23208)

```
df.dropna(axis=0)
```
![Screenshot 2025-05-01 224852](https://github.com/user-attachments/assets/91fdf202-cd36-45da-af52-4f6285c73d12)

```
dfs=df[df['TOTAL']>310]
dfs
```
![Screenshot 2025-05-01 224845](https://github.com/user-attachments/assets/f8220a69-533f-452a-99af-06551aac3098)

```
dfs=df[df['NAME'].str.startswith(('R','E'))&(df['AVG']>100)]
dfs
```
![Screenshot 2025-05-01 224838](https://github.com/user-attachments/assets/2e5a059d-744f-4bff-91f0-7efd8ab51b87)

```
df.iloc[[0,5,6,7,10],[2,10,11]]
```
![Screenshot 2025-05-01 224832](https://github.com/user-attachments/assets/b83366b8-356c-4de3-a51b-fba9aaae47b9)

```
df.iloc[5:17,0:5]
```
![Screenshot 2025-05-01 224827](https://github.com/user-attachments/assets/5cfbaefb-7179-4f20-8d67-e7febd5e1061)

```
df.isnull().sum()
```
![Screenshot 2025-05-01 224822](https://github.com/user-attachments/assets/d4ecb987-65e6-4e9c-bccc-2a5c8cb69043)

```
df.fillna({'TOTAL':df['TOTAL'].mean()}, inplace=True)
df.fillna({'AVG':df['AVG'].mean()}, inplace=True)
df
```
![Screenshot 2025-05-01 224807](https://github.com/user-attachments/assets/60bcad89-f07f-4546-9f2b-72d7d9faaf96)

```
mn=df.TOTAL.mean()
mn
```
![Screenshot 2025-05-01 224744](https://github.com/user-attachments/assets/6c7db352-4b84-48cc-8dee-ec14e17c5ef2)
# IQR(Inter Quartile Range)
```
import pandas as pd
import numpy as np
import seaborn as sns
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
![Screenshot 2025-05-01 224734](https://github.com/user-attachments/assets/2ce051d8-021c-4759-9727-60713a85232a)

```
sns.boxplot(data=af)
```
![Screenshot 2025-05-01 224728](https://github.com/user-attachments/assets/c6b1361f-fcd2-4ea6-92b9-bfb54c71d75e)

```
sns.scatterplot(data=af)
```
![Screenshot 2025-05-01 224700](https://github.com/user-attachments/assets/c5d3d2dc-7ca1-46b5-9448-0090b1bcca27)

```
q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
iqr
```
![Screenshot 2025-05-01 224655](https://github.com/user-attachments/assets/86ea06ba-2c22-46a0-b148-009b4f8d6b2d)

```
Q1=np.percentile(af,25)
Q3=np.percentile(af,75)
IQR=Q3-Q1
IQR
```
![Screenshot 2025-05-01 224650](https://github.com/user-attachments/assets/de554938-6bb4-4d87-b8b0-2a9a044e3ece)

```
lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR
upper_bound
```
![Screenshot 2025-05-01 224646](https://github.com/user-attachments/assets/eb2d858d-6dab-456c-af05-34eb4167358c)

```
lower_bound
```
![Screenshot 2025-05-01 224631](https://github.com/user-attachments/assets/e6258c96-e88a-4aea-9e9f-2def7637c47a)

```
outliers = [x for x in age if x < lower_bound or x > upper_bound]
print("Q1:", Q1)
print("Q3:", Q3)
print("Lowewr Bound:", lower_bound)
print("Upper Bound:", upper_bound)
print("Outliers:", outliers)
```
![Screenshot 2025-05-01 224621](https://github.com/user-attachments/assets/2de4c419-b489-419c-8850-618b2b38acab)

```
af=af[((af>=lower_bound)&(af<=upper_bound))]
af
```
![Screenshot 2025-05-01 224552](https://github.com/user-attachments/assets/7bb548dd-1cfb-4876-98f0-59b179daeaca)

```
af.dropna()
```
![Screenshot 2025-05-01 224546](https://github.com/user-attachments/assets/1c305b28-8454-45be-a999-7301b3079bd5)

```
sns.boxplot(data=af)
```
![Screenshot 2025-05-01 224541](https://github.com/user-attachments/assets/e3c4a347-b51e-46fb-a5f4-1ef6aee1ffb4)

```
sns.scatterplot(data=af)
```
![Screenshot 2025-05-01 224536](https://github.com/user-attachments/assets/63554545-7415-4c26-a707-30c70d1a4ba2)
# Z - SCORE
```
data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean=np.mean(data)
std=np.std(data)
print('mean of data set is',mean)
print('std. deviation is', std)
```
![Screenshot 2025-05-01 224531](https://github.com/user-attachments/assets/72140da8-fd20-48a4-8daf-0fcc0b38da05)

```
threshold=3
outlier=[]
for i in data:
  z=(i-mean)/std
  if z>threshold:
    outlier.append(i)
print('outlier in dataset is',outlier)
```
![Screenshot 2025-05-01 224527](https://github.com/user-attachments/assets/76c3f442-34d0-4785-a25d-01840425cd32)

```
import pandas as pd
import numpy as np
import seaborn as sns
from scipy import stats
data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
df=pd.DataFrame(data)
df
```
![Screenshot 2025-05-01 224501](https://github.com/user-attachments/assets/b4d53b70-6a45-4ae5-b0fc-0866ff41ba17)

```
z=np.abs(stats.zscore(df))
print(df[z>3])
```
![Screenshot 2025-05-01 224340](https://github.com/user-attachments/assets/030e85ae-3679-4176-a213-5ec642fe3df8)

```
val=[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]
out=[]
def d_o(val):
  ts=3
  m=np.mean(val)
  sd=np.std(val)
  for i in val:
    z=(i-m)/sd
    if np.abs(z)>ts:
      out.append(i)
  return out
op=d_o(val)
op
```
![Screenshot 2025-05-01 224334](https://github.com/user-attachments/assets/e0190c10-7242-4e0a-bfd1-9c88d6e13c1d)

```
import pandas as pd
import numpy as np
import seaborn as sns
from scipy import stats
id=pd.read_csv("/content/iris.csv")
id
```
![Screenshot 2025-05-01 224327](https://github.com/user-attachments/assets/2b677e08-e3ea-4a28-a66c-d5a032877f5f)

```
sns.boxplot(x='sepal_width',data=id)
```
![Screenshot 2025-05-01 224319](https://github.com/user-attachments/assets/d79c2787-451c-4c74-aa66-ede8b499b69a)

```
c1=id.sepal_width.quantile(0.25)
c3=id.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
print(iq)
```
![Screenshot 2025-05-01 224311](https://github.com/user-attachments/assets/9eed8271-7035-4989-a372-b2f510c2113b)

```
rid=id[((id.sepal_width<(c1-1.5*iq))|(id.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![Screenshot 2025-05-01 224302](https://github.com/user-attachments/assets/9be35e93-6f10-4969-acb9-8eaa47153ff9)

```
delid=id[~((id.sepal_width<(c1-1.5*iq))|(id.sepal_width>(c3+1.5*iq)))]
delid
```
![Screenshot 2025-05-01 224256](https://github.com/user-attachments/assets/adbc6f3c-0062-45a9-8c29-107dd1f4e2d1)

```
sns.boxplot(x='sepal_width',data=delid)
```
![Screenshot 2025-05-01 224246](https://github.com/user-attachments/assets/ae258129-3446-4284-9a30-772aa05a4e2b)


        
# Result
        Thus the outliers are detected and removed in the given file using IQR and Z-Score Method
