<h1 align="center">Ex. 1   Data Cleaning and Outlier Detection & Removal</h1>


## AIM
### To read the given data and perform data cleaning and save the cleaned data to a file.

## Explanation
 Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

## Algorithm
### STEP 1
#### Read the given Data

### STEP 2
#### Get the information about the data

### STEP 3 
#### Remove the null values from the data

### STEP 4
#### Save the Clean data to the file

### STEP 5
#### Remove outliers using IQR

### STEP 6
#### Use zscore of to remove outliers

## Coding and Outputs

<h3 align="center">Data Cleaning</h3>

```py
import pandas as pd
import numpy as np
import seaborn as sns
import os 
df=pd.read_csv("SAMPLEIDS.csv")
df
```
![Screenshot 2024-03-05 135404](https://github.com/guru14789/exno1/assets/151705853/808e2533-0891-4d58-ae4c-cf038fee4d9e)

```py
df.isnull().sum()

```
![Screenshot 2024-03-05 135437](https://github.com/guru14789/exno1/assets/151705853/7294c2d5-dec9-4e86-80ce-e8dc772a8083)
```py
df.isnull().any()
```
![Screenshot 2024-03-05 135826](https://github.com/guru14789/exno1/assets/151705853/8b0f9039-fa45-48c2-bb76-b630e81721a3)


```py
df.dropna()
```
![Screenshot 2024-03-05 135924](https://github.com/guru14789/exno1/assets/151705853/4b2e025c-2e17-487b-9831-a41c7c690984)


```py
df.fillna(0)
```
![Screenshot 2024-03-05 140007](https://github.com/guru14789/exno1/assets/151705853/2539c28b-03df-4b0c-86ab-3742b291ac11)


```py
df.fillna(method = 'ffill')
```
![Screenshot 2024-03-05 140051](https://github.com/guru14789/exno1/assets/151705853/4a180a20-f91b-4cda-905f-d784698f09ee)


```py

df.fillna(method = 'bfill')
```
![Screenshot 2024-03-05 140129](https://github.com/guru14789/exno1/assets/151705853/fa16be83-2b1a-4017-99d8-2b1c48a0a0d6)



```py
df_dropped = df.dropna()
df_dropped
```
![Screenshot 2024-03-05 140209](https://github.com/guru14789/exno1/assets/151705853/209f7cce-6ad7-4c7c-8e31-7186ceb7246d)


```py
df.fillna({'GENDER':'FEMALE','NAME':'SREE','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![Screenshot 2024-03-05 140334](https://github.com/guru14789/exno1/assets/151705853/d4b47d4f-4813-462e-a825-0f668885ab87)


<hr>

<h3 align="center">IQR(Inter Quartile Range)</h3>
<hr>

```py
ir=pd.read_csv('iris.csv')
ir
```
![Screenshot 2024-03-05 140456](https://github.com/guru14789/exno1/assets/151705853/dffcc4f0-e068-4d5f-babd-8342221f0931)

```py
ir.describe()
```
![Screenshot 2024-03-05 140520](https://github.com/guru14789/exno1/assets/151705853/d664568d-38d6-4fbd-8a07-29a42f6fc3d0)

```py

sns.boxplot(x='sepal_width',data=ir)
```
![Screenshot 2024-03-05 140615](https://github.com/guru14789/exno1/assets/151705853/98895aba-5c1b-44d0-9832-94f0bd63e81d)




```py
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![Screenshot 2024-03-05 140754](https://github.com/guru14789/exno1/assets/151705853/9f0863fb-3bac-44f6-9891-8e3b6cc4f5fb)


```py

rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![Screenshot 2024-03-05 140826](https://github.com/guru14789/exno1/assets/151705853/12613a1d-8cbb-4cda-9306-58284123842b)


```py
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![Screenshot 2024-03-05 140852](https://github.com/guru14789/exno1/assets/151705853/cda9e272-b68a-452f-8130-b074a3342324)

```py
sns.boxplot(x='sepal_width',data=delid)
```
![Screenshot 2024-03-05 140921](https://github.com/guru14789/exno1/assets/151705853/a03d0dc7-62a0-4119-b963-fa0860299e82)

<hr>

<h3 align="center">Z-Score</h3>
<hr>

```py
import matplotlib.pyplot as plt
import scipy.stats as stats
```
```py
dataset=pd.read_csv("heights.csv")
dataset
```
![Screenshot 2024-03-05 141103](https://github.com/guru14789/exno1/assets/151705853/94a93de2-ed8c-43b0-a66f-2b7ebef68884)


```py
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```

```py
iqr = q3-q1
iqr
```
![Screenshot 2024-03-05 141232](https://github.com/guru14789/exno1/assets/151705853/2ebe7c9e-c765-4ae1-8872-82f94497b102)



```py
low = q1 - 1.5*iqr
low
```
![Screenshot 2024-03-05 141302](https://github.com/guru14789/exno1/assets/151705853/43bfb2e6-9148-4f3e-a9f4-38ab45b94b68)


```py
high = q3 + 1.5*iqr
high
```
![Screenshot 2024-03-05 141333](https://github.com/guru14789/exno1/assets/151705853/9999ace0-f6ac-4ceb-8a4a-ce16f8a29983)



```py
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![Screenshot 2024-03-05 141358](https://github.com/guru14789/exno1/assets/151705853/1276be99-87da-43f2-886b-9bb3a899a837)


```py
z = np.abs(stats.zscore(df['height']))
z
```
![Screenshot 2024-03-05 141432](https://github.com/guru14789/exno1/assets/151705853/35447c0d-8cef-429a-9def-c944efb592e4)

```py
df1 = df[z<3]
df1
```
![Screenshot 2024-03-05 141501](https://github.com/guru14789/exno1/assets/151705853/dcdb57de-57dd-49ee-aca0-2f90f3be29ad)


<hr>

## Result
 Hence the data was cleaned , outliers were detected and removed.
