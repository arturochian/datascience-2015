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

diabetes_X = diabetes.data[:, np.newaxis]

# Picking one feature, in particular the second feature
diabetes_temp = diabetes_X[ :, :, 3]

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
