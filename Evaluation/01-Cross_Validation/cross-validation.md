# What is Cross-Validation?
![hmmm..](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRstlW16yoskxx4oaTwFPbBjLokjdEbvpgQnA&usqp=CAU)

 **Cross**-**validation is a** statistical technique which involves partitioning the data into subsets, training the data on a subset and use the other subset to evaluate the model's performance. To **reduce** variability we perform multiple rounds of **cross**-**validation** 

## Why Use Cross-Validation

So have you ever got excited over getting  90% accuracy on your test set, think again, did you actually got a 90% accuracy rate or was it just plain luck, well if you've been training your models using the **train_test_split** method then **YES!** , you got lucky,  but have you ever thought there could be a better way?


## How it works
There are different types of Cross Validation Techniques but the overall concept remains the same.

The procedure has a single parameter called k that refers to the number of groups that a given data sample is to be split into. As such, the procedure is often called k-fold cross-validation. When a specific value for k is chosen, it may be used in place of k in the reference to the model, such as k=10 becoming 10-fold cross-validation.

If k=5 the dataset will be divided into 5 equal parts and the below process will run 5 times, each time with a different holdout set.

- Take the group as a holdout or test data set

- Take the remaining groups as a training data set

- Fit a model on the training set and evaluate it on the test set

- Retain the evaluation score and discard the model

the there no fixed ratio in **Cross-Validation** method, you can choose whatever ratio you would like such as 80:20, 70:30, 90:10, you can choose the perfect value depending on the size of your dataset, although the sweet spot is considered 75:25.

## Will it improve accuracy?

**Cross-Validation** is usually used for estimating your model's performance by reducing the amount of randomness and it gives less variability in test-error, and it also help in reducing overfitting , Increasing the **k** can  improve the **accuracy** of the measurement of your accuracy, but it **does** not actually  improve the original **accuracy** you are trying to measure .


## Implementation

First we are gonna implement the **train_test_split** strategy and then compare it to **Cross-Validation** method.

For the sake of this Implementation  I am going to use the Iris dataset, which you can access using the **Sklearn** library.

To import the Iris dataset you can use the example below.

    from sklearn import datasets

    iris = datasets.load_iris()
    X = iris.data[:, :2]  
    y = iris.target
Using the standard  **train_test_split** method

	from sklearn.model_selection import train_test_split

	X_train, X_test, Y_train, Y_test = train_test_split(X, y, 
	test_size=0.25, random_state=0)

Preprocessing is 70% of the work, so I am going to standardize the independant variables

    from sklearn.preprocessing import StandardScaler

	sc = StandardScaler()
	X_train = sc.fit_transform(X_train)		
	X_test = sc.transform(X_test)
Fit the training set to  **LogisticRegression**
	

	from sklearn.linear_model import LogisticRegression

	lreg = LogisticRegression()
	lreg.fit(X_train, Y_train)
Model score

    score = lreg.score(X_test, Y_test)
	score
Final score is **0.684**

But notice if you change the value for  **random_state** you will get a different score.
***NOTE:*** Score after random_state set to 15 is **0.842**

You can see the dramatic change in the score, that's why **train_test_split** method is considerd inefficient

Now let's try **Cross-Validation**.

    from sklearn import datasets

	iris = datasets.load_iris()
	X = iris.data[:, :2]  
	y = iris.target
	
	#Preprocessing
	from sklearn.preprocessing import StandardScaler

	sc = StandardScaler()
	X = sc.fit_transform(X)
	
	#LogisticRegression
	from sklearn.linear_model import LogisticRegression
	lreg = LogisticRegression()

Simply import **cross_val_score** from **Sklearn**,and specify your estimator, and the number of splits you  would like.
***NOTE***:  **higher the number, the longer it takes.**
		

    from sklearn.model_selection import cross_val_score
    scores = cross_val_score(lreg, X, y, cv=5)
    scores.mean()
The **scores** variables contains all the scores from all the 5 splits, so what you can do is take the mean of all the values.
***Cross-Validation score is***         ** 0.806**

Dont go with score, the point of **Cross-Validation** is estimating your model's performance.

## Conclusion

**Cross-Validation** is a procedure used to avoid overfitting and estimate the skill of the model on new data, and there are common tactics that you can use to select the value of **k** for your dataset, what's more, the less randomness in your dataset the more sensible is your precision.



