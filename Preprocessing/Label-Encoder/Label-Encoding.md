

# Label-Encoding 
When starting in Machine Learning you might get confused between **Label-Encoding** and **OneHotEncoding**, both hold the same concept which is encoding categorical variables, but just because you're more familiar with one of the methods doesn't mean to use it on every dataset, it can have a significant effect on your dataset.

All machine learning models must have their dependant and independent variables in a numeric way, such as if you have a dataset where you have to predict a flower's species, and your input variables is the color of the flowers written as strings e.g. (red, blue, green, black, grey, etc).

The machine itself doesn't understand what you're feeding it, machines only understand numbers, so if you try to feed the model your input data without using **Label-Encoding** you will notice that it will return an error.

# How it works
Applying **Label-Encoding** is very simple,  **Label-Encoder** is a part of the SciKit Learn library, you can look for the documentation [here.](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html)

Let's start with an example from this dataset.
![Dataset](/home/s4lm_xi/mediums/Preprocessing/Label-Encoder/data_2.png)

here we have a dataset with 2 categorical columns(sex, smoker).

Label-Encoder will transform these columns into number, say in the sex column we have two classes male and female, so the **Label-Encoder** will mark female as **0** and male as **1**.

Same stuff with the **smoker** column, it will transform the first class with the value **0** which is **yes** and transform **no** to **1**.



# Implementation

First lets import **Label-Encoder** from the SciKit Learn library.

``from sklearn.preprocessing import LabeEncoder
encoder = LabelEncoder()``



Now let's fit and transform the categorical column, first we will transform the **sex** column.

after running this piece of code we'll see that the **sex** column has been replaced by numbers

```data['sex'] = encoder.fit_transform(data['sex'])```

![](/home/s4lm_xi/mediums/Preprocessing/Label-Encoder/data_3.png).

Now that we have encoded the **sex** column, let's move to the next categorical column which is **smoker**, using the same strategy you can encode the **smoker** column.

`	encoder_smoker = LabelEncoder()`

`data['smoker'] = encoder_smoker.fit_transform(data['smoker'])`

Here's all the encoded columns.

![](/home/s4lm_xi/mediums/Preprocessing/Label-Encoder/data_3.png).