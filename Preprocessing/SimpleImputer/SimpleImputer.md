# Handling Missing Values

### What Is SimpleImputer

The **SimpleImputer** class provides basic strategies for imputing missing values. Missing values can be **imputed** with a provided constant value, or using the statistics (mean, median, or most frequent) of each column in which the missing values are located.

<img src="https://media.giphy.com/media/3oKIPlLZEbEbacWqOc/giphy.gif" style="zoom:150%;" />

### Checking For Missing Values

Python libraries represent missing numbers as **nan** which is short for ***"not a number"***.  You can detect which cells have missing  values, and then count how many there are in each column with the following piece of code.

<img src="/home/s4lm_xi/mediums/Preprocessing/SimpleImputer/data_1.png" style="zoom:120%;" />

```missing values
data.isnull().sum()
```

<img src="/home/s4lm_xi/mediums/Preprocessing/SimpleImputer/data_2.png" style="zoom:120%;" />

This is a very basic strategy for checking the existence of missing values. As you can see we have 22 missing values present in the **charges** column.



### Solutions

##### 1- Basic Option: Drop Columns 

If your data contains missing values you can simply just drop the columns with the missing values, to do so here's an example.

First check which column contains the missing values

```check for missing values
data.isnull().sum()
```

<img src="/home/s4lm_xi/mediums/Preprocessing/SimpleImputer/data_2.png" style="zoom:120%;" />

We can observe that the **charges** column contains missing values, let's drop it.

```Dropping column
data = data.drop('charges', axis=1)
```





##### 2- Better Alternative: Imputation

Imputation fills in the missing value with some number. The imputed value won't be exactly right in most cases, but it usually gives more  accurate models than dropping the column entirely.

Example.

```Implementation
from sklearn.impute import SimpleImputer
import numpy as np

si = SimpleImputer(missing_values= np.nan, strategy= 'median')

data = si.fit_transform(data)
```

###### Parameters

1. **missing_values**: number, string, np.nan (default) or None

   The placeholder for the missing values. All occurrences of `missing_values` will be imputed. 

2. **strategy**: string, default=’mean’

   The imputation strategy.

   1. If **"mean”**, then replace missing values using the mean along each column. Can only be used with numeric data.

   2. If **“median”**, then replace missing values using the median along each column. Can only be used with numeric data.

To examine the parameters in detail, please refer to the [Documentation](https://scikit-learn.org/stable/modules/generated/sklearn.impute.SimpleImputer.html).



This is the result after applying imputation.

<img src="/home/s4lm_xi/mediums/Preprocessing/SimpleImputer/data_3.png" alt="Result" style="zoom:120%;" />

### Strategy

Choosing an inappropriate strategy can result in bad model performance, to pick the best strategy you have to check the presence of outliers.

 ##### What Are Outliers 

A value that "lies outside" (is much smaller or larger than) most of the other values in a set of data. For **example** in the scores 25,29,3,32,85,33,27,28 both 3 and 85 are "**outliers**".

See also: [Visualizing Outliers](https://flowingdata.com/2018/03/07/visualizing-outliers/).



##### Solution

To be able to find outliers you can easily plot your dataset, to check the existence of the outliers.

This is a very basic method to check for outliers

1. First Method

   ```histogram
   data.hist(figsize=(25,15), bins=25)
   ```

   <img src="/home/s4lm_xi/mediums/Preprocessing/SimpleImputer/data_4.png" alt="histogram" style="zoom:120%;" />

2. Second Method

   ```Boxplot
   import matplotlib.pyplot as plt
   import seaborn as sns
   
   plt.figure(figsize=(20,15))
   
   plt.subplot(331)
   sns.boxplot(x= data.charges)
   
   plt.subplot(332)
   sns.boxplot(x= data.bmi)
   
   plt.subplot(333)
   sns.boxplot(x= data.bmi)
   ```

   <img src="/home/s4lm_xi/mediums/Preprocessing/SimpleImputer/data_5.png" alt="Boxplot" style="zoom:120%;" />

As should be obvious we have the most outliers in the charges column, and they're exceptionally high, so using the **mean** strategy wouldn't be efficient.

In that case, using the **median** would be much better because it will calculate the median value of the column, and the outliers won't affect as much.

here are numerous techniques you can use, more information will be available in the [Documentation](Documentation).



