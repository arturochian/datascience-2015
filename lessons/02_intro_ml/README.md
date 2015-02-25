# Numpy Practice

0. Use `arange` to create an array of the numbers from 0 to 100.
1. Create two arrays [1, 3, 5] and [2, 4, 6] and add them.
2. Create a 3-by-6 matrix and then find out its dimensionality using `ndim`.
3. In the aforementioned matrix, use `dtype` to discover the data types within the matrix.
4. Create a 4-by-5 matrix full of zeros using `zeros`. Then, create a 5-by-4 matrix full of ones using `ones`.
5. Use `reshape` to turn the array from Question 1 into a 10-by-10 matrix.
6. Given two 2-by-2 arrays A and B of your creation, do `A * B` and `dot(A, B)`. What's the difference?
7. Given the array in Question 1, set every 2nd element to 31415. (Hint: use the third parameter in list slicing)
8. Write a function that takes any arbitrary multidimensional array (aka matrix) and returns just the nth column. Hint: the function will look like `def retrieve_column(matrix, n)`.


Diabetes Example of Linear Regression in iPython notebook:
```python
import pylab as pl
import numpy as np
from sklearn import datasets, linear_model

# Load the diabetes dataset
diabetes = datasets.load_diabetes()

# diabetes.data is a 442 x 10 matrix
# new axis will turn it into a 442 x 1 x 10 matrix
diabetes_X = diabetes.data[:, np.newaxis]

# Then suppose we just want to use one feature of the data (one of the input variables)
# to create our line of best fit, then let's just pick the first one
diabetes_temp = diabetes_X[ :, :, 0]

# now if you check diabetes_temp.shape, you'll see a 442 x 1 matrix
# if we did NOT do the newaxis step, diabetes_temp.shape would be a 442-long list of numbers, not a matrix.
# This is a problem because the regression_model.fit() method expects the training data to be a list of vectors, since
# the data have multiple variables. In our case we're just simplifying it to use one variable but the python method
# is general.

# Segmenting the input data into a training set and a test set
# 20% of the data (corpus) should be training, the rest the test.
input_data = diabetes_temp
training_data_X = diabetes_temp[:88]
test_data_X = diabetes_temp[88:]

# Segmenting the target (output data) into a training set and a test set.
training_data_Y = diabetes.target[:88]
test_data_Y = diabetes.target[88:]

# Train our linear regression model
regression_model = linear_model.LinearRegression()

# Let's train the model on the input and ouput training sets
regression_model.fit(training_data_X, training_data_Y)

print "Here's the variance score: {}".format(regression_model.score(test_data_X, test_data_Y))

# Let me initialize a scatter of the data
pl.scatter(test_data_X, test_data_Y,  color='black')

# Then let me plot it
pl.plot(test_data_X, regression_model.predict(test_data_X), color='blue')

# Dont show the xticks and ytick values
pl.show()
```

# Explanation of `np.newaxis` and why we used it
The reason we used `np.newaxis` is because the regression .fit() method expects the training data to be a matrix (list of lists) rather than just a list.

I'll walk through this step-by-step below. Please Slack the public channel with any follow up questions. I'm going to walk through what happened when we did not use `np.newaxis` and then what was different about when we did use it.

Our objective: Pick one feature of the diabetes data, not all 10 variables, and then create a line of best fit. Again, a "feature" just means one of the input variables, any of the 10 physiological measurements in `diabetes.data`

Suppose we did not use newaxis and just wanted to pick the first feature of the data:

```
import pylab as pl
import numpy as np
from sklearn import datasets, linear_model

# Load the diabetes dataset
diabetes = datasets.load_diabetes()

# diabetes.data is a 442 x 10 matrix since we have 442 rows of data
# and 10 columns corresponding to 10 different physiological measurements
# of the patient
diabetes = datasets.load_diabetes()

# let's pick the first feature, the 0th column
# we want to get a 442 x 1 matrix
diabetes_temp_data = diabetes.data[:, 0]

# now let's see what diabetes_temp_data's shape is
diabetes_temp_data.shape

# it's (442,). it's not a 442 x 1 matrix like we wanted
# so when we try to use the regression_model.fit() method
# it's going to throw a tuple error!

# let's choose the first 88 rows (20% of the data)
# to be our training set
training_data_X = diabetes_temp_data[:88]

# and let's get the first 88 rows of the target data
training_data_Y = diabetes.target[:88]

# now let's create an instance of LinearRegression
# that we'll use to fit to the data
regression_model = linear_model.LinearRegression()

# Let's train the model on the input and ouput training sets
regression_model.fit(training_data_X, training_data_Y)
# And we get a tuple error!
```

That is because the .fit() method expects training_data_X to be a matrix (aka a list of lists), not a simple list.

(Here's)[http://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html#sklearn.linear_model.LinearRegression.fit] the documentation on the .fit method.

So we use `np.newaxis` to insert a new dimension of size 1:

```python
diabetes_X = diabetes.data[:, np.newaxis]
# diabetes_X is now a 442 x 1 x 10 matrix

diabetes_temp_data  = diabetes_X[:, :, 0]
# diabetes_temp_data.shape show it now to be a 442 x 1 matrix
# which is a list of lists (aka a matrix), which is the exact
# format that the .fit() method expects
# so it does NOT throw an error.
```

## A simple example to illustrate how np.newaxis works
```python
import numpy as np

# let's create a tiny array
a = np.array([1, 2, 3, 4])
# and turn it into a 2 x 2 matrix
# let's do this twice, because we'll try 2 different things
b = a.reshape(2, 2)
c = a.reshape(2, 2)

x = b[np.newaxis, :]
x[0]
x[1] # should throw an error since we've just wrapped the whole array in an array

y = c[:, np.newaxis]
y[0]
y[1]
```

# Homework
- http://www.regentsprep.org/regents/math/algebra/APR3/PracCond.htm


# Reading
- http://www.countbayesie.com/blog/2015/2/18/bayes-theorem-with-lego
- http://en.wikipedia.org/wiki/Bayes%27_theorem
- http://www.quora.com/In-laymans-terms-how-does-Naive-Bayes-work
- http://www.nltk.org/book/ch06.html
- https://www.youtube.com/watch?v=4Lb-6rxZxx0
