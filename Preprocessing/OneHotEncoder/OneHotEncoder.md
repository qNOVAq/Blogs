# What Is OneHotEncoder

**OneHotEncoder** is an encoder that transforms a categorical column to a binary column where each column represents each category from the original column.



# Why Use OneHotEncoder

**one hot encoding** allows the representation of categorical data to be more expressive.  Many machine learning algorithms cannot work with categorical data  directly. The categories must be converted into numbers before being fitted to the model



# How It Works

The features are encoded using a one-hot (aka 'one-of-K' or 'dummy') encoding scheme. This creates a  binary column for each category and returns a sparse matrix or dense  array (depending on the sparse parameter) By default, the encoder  derives the categories based on the unique values in each feature.



#  What Is get_dummies

It's used to convert a categorical variable into ***dummy/indicator variables.***

**get_dummies** holds the same concept as **OneHotEncoder**, but get_dummies is mainly used for ***exploratory analysis***,



# OneHotEncoder VS get_dummies

For **Machine Learning**, you almost definitely want to use **OneHotEncoder**. For other tasks like simple analyses, you might be able to use **get_dummies**, which is a bit more convenient.

**Onehotencoding** can allow you to interact with Categorical variables in relation to **pre-processing** when you wish to more directly interact with and modulate the Data in terms of known **Parametrics**

**OneHotEncoder** allows for greater interactions and modifications - when you want to more directly interact with how the formulation of Categories should be, but when using **get_dummies** you're hands are tied.

Basically, **get_dummies** is used in an exploratory analysis, whereas **OneHotEncoder** in computation and estimation.

# When To Use OneHotEncoder 

#### Example

<img src="/home/s4lm_xi/mediums/Preprocessing/OneHotEncoder/data_1.png" style="zoom:120%;" />

**OneHotEncoder** is best used on columns where the categories are in **ordinal** order, in the example above we can see that the **region** column is categorical, if we use the **LabelEncoder** on the **region** column then the model will misunderstand the data to be in some kind of order, where the categories with the value of **1** are better than the categories with the value of **0**, which is completely false.

#### Conclusion

Only apply **OneHotEncoder** to the **ordinal** columns, while on the other hand when applying **LabelEncoder** only apply them on **nominal** columns.



# Implementation

### What Is The Dummy Variable Trap

The **Dummy Variable trap** is a scenario in which the independent **variables** are multicollinear a scenario in which two or more **variables** are highly correlated.

in simple words, one variable can be predicted from the other,

To overcome the **Dummy Variable Trap** you must use **one less dummy variable**(n-1) than the categorical values.



#### Implementation

**OneHotEncoder ** is a part of the **SciKit Learn** Library, let's import it and apply it on our dataset.



This is the dataset.

<img src="/home/s4lm_xi/mediums/Preprocessing/OneHotEncoder/data_1.png" style="zoom:125%;" />



Now let's see how many unique values we have in the **region** column.

`data.region.value_counts()`

<img src="/home/s4lm_xi/mediums/Preprocessing/OneHotEncoder/data_3.png" style="zoom:120%;" />

As you can see we have 4 different categories(southeast, northwest, southwest, northeast)

Now let's apply **OneHotEncoder** using the **ColumnTransformer** from the **SciKit Learn** library.

```from sklearn.preprocessing import OneHotEncoder
from sklearn.compose import ColumnTransformer

ct = ColumnTransformer([('encoder', OneHotEncoder(), [5])], remainder='passthrough')

data = np.array(ct.fit_transform(data))
```

For the first **ColumnTransformer** parameter we need to pass, list of (name, transformer, columns) tuples specifying the transformer objects to be applied to subsets of the data.

For the name you can write anything in your mind, for the transformer, you have to specify which transformer you would like to use, in our case we'll use the **OneHotEncoder** transformer, and for the columns, we need to specify the index of the column that we would like to transform.

Here I transformed the data into a DataFrame again just so we can visualize our results

```data = pd.DataFrame(data)
data = pd.DataFrame(data)
data.head()
```

<img src="/home/s4lm_xi/mediums/Preprocessing/OneHotEncoder/data_4.png" style="zoom:120%;" />

Just like we expected the **region** column has been transformed into 4 different binary columns, which are the first 4 columns.



Let's not forget about the **Dummy Variable Trap**, we have to take only (n-1) columns, which means now we have to drop the first dummy column or the last one, its doesn't make a difference which one you drop, but keep in mind that you have to drop at least one dummy column.



You can do the following to drop the first dummy column.

```data = data.iloc[:, 1:]
data = data.iloc[:, 1:]
data.head()
```

After running the following piece of code you should have the first column dropped.

<img src="/home/s4lm_xi/mediums/Preprocessing/OneHotEncoder/data_5.png" style="zoom:120%;" />



For more information please refer to the [OneHotEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html) and [ColumnTransformer](https://scikit-learn.org/stable/modules/generated/sklearn.compose.ColumnTransformer.html) Documentation.