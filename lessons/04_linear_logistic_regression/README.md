# Objectives
Students will be able to
- Define and apply linear regression and logistic regression
- Show how and when to use these techniques
- Give practical and relevant examples from industry

# Linear Regression
## What is it?
- Given a set of data points, fine a line or curve that fits them the best.
- Useful for modeling the relationship between N input variables (*x*<sub>1</sub>, ..., *x*<sub>N</sub>) and *y*, some output, also called the target.
- Use it to make predictions

## Simple linear Regression
y = ax<sub>1</sub> + b

## Multivariable Regression
y = a<sub>1</sub>x<sub>1</sub> + ... + a<sub>n</sub>x<sub>n</sub> + b

## What are some examples?
- Predicting product revenues based on historical data (e.g. Disney)
- Predicting election outcomes
- Identifying stock market trends
- Recommending matches on dating sites (e.g. eHarmony)
- Determining credit score
- Analyzing the impact of price changes on units sold
- Assessing risk (e.g. health insurance companies modeling the relationship between customer age and insurance claims)

## How does it work?
- The algorithm tries to find the the line or curve that minimizes the square of the distances between the data and the line.
- This is called the *least squares* method. There are many different kinds but we'll focus on Ordinary Least Squares (OLS).
- The most common way of minimizing the distances is by way of *gradient descent*.

## Assumptions of the Model
- Our input variables are not riddled with measurement errors
- Input variables are not highly correlated
- How do we measure correlation?

## What are some things to look out for?
- Always graph the data. Here is a [basic tutorial on plotting](http://matplotlib.org/users/pyplot_tutorial.html) with `matplotlib`.
- See how linear regression fails for the Anscombe Quartet.
- For outliers, use robust linear regression.

## How do I know it's working
- R<sup>2</sup> tells us how well our model fits the data, but doesn't tell us how good our predictions are
- Use cross-validation, e.g. training set and test set similar to what we did with Naive Bayes.

## Set Up for Our Code
1. download [this csv](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/housing_prices.csv) on housing prices
2. move that dataset under your /repos/datasets/ directory on your local machine (NOT VAGRANT)
3. log into vagrant from the /vm/ directory as usual
4. run `sudo pip install statsmodels`
5. run `sudo ipython notebook --profile=dst`
6. paste the following code into iPython notebook and run it

```python
import csv
import numpy as np
# our regression library
import statsmodels.api as sm
# our plotting library
import matplotlib.pyplot as plot
# our 3d plotting utility
from mpl_toolkits.mplot3d import Axes3D

# open csv file and get the rows
with open('/home/vagrant/repos/datasets/housing_prices.csv', 'rb') as f:
    rows = [row for row in csv.reader(f)]

# the first row is the header, which looks like this: SIZE, NUMBER OF BEDROOMS, PRICE
# let's exclude the header from the data
header = rows[0]

# each row looks like this
# 3327.78, 3, 504838
rows = rows[1:]

# All of the data has been read in as strings, so we need to cast them to floats
# Let's separate the data into our input data and our target
input_data = np.array([
    [float(row[0]), float(row[1])] for row in rows
])

# Statsmodels does not use a y-intercept by default
# That means it's just trying to find y = ax instead of y = b + ax_1
# We want a y-intercept because it creates a better model.
# Since we're in 3 dimensions: size, bedroom count, price, technically it's a z-intercept
# So we'll use add_constant to add a column of 1s at the beginning of input_data
# so that turns a row like this: (6250, 3) into (1, 6250, 3)
input_data = sm.add_constant(input_data)
# The reason behind this is that if I want y = b + ax_1 but I only start with y = ax_1
# A way to get there is to now bump up to 2-variable linear regression and get this:
# y = bx_0 + ax_1 (still no intercept)
# But remember that every row in that first column = 1, so
# y = bx_0 + ax_1 = b(1) + ax_1 = b + ax_1
# Voila! We got an intercept of b

# Let's pull out the target data
target = np.array([float(row[2]) for row in rows])

# OLS stands for Ordinary Least Squares, the most common method of linear regression
regression_model = sm.OLS(target, input_data)
results = regression_model.fit()
# Show us some statistical summary of the model
print results.summary()

# Now we're ready to plot the data
fig = plot.figure()
ax = fig.add_subplot(111, projection='3d')
# first arg is variable_1 (size), then variable_2 (bedroom count), then the target (price)
ax.scatter(input_data[:, 1], input_data[:, 2], target)

# Run through our input data and see what our model would output
predictions = results.predict(input_data)

# To do the surface plot, follow this tutorial: http://matplotlib.org/examples/mplot3d/surface3d_demo.html
X, Y = np.meshgrid(input_data[:, 1], input_data[:, 2])
surface = ax.plot_surface(X, Y, predictions, color='yellow')

def predict(size, number_of_bedrooms):
    """
    Given a fresh piece of data (size, number of bedrooms)
    this will predict the price, based on our trained linear model.

    The output of this function is an array, e.g. [252776] which means
    the estimated price is $252,776.
    """
    return results.predict([1, size, number_of_bedrooms])

print "\n"
print "Now let's predict what a 6255 sqft home with 5 bedrooms would cost..."
print "....... ${}".format(predict(6255, 5)[0])
```

## Useful libraries to get familiar with
- [statsmodels](http://statsmodels.sourceforge.net/): for regressions and other statistical models
- [matplotlib](http://matplotlib.org/): for plotting

## Advanced techniques
- scaling features: makes it easier for gradient descent to converge quickly and train your model
- regularization: a technique for penalizing an overly complex model with too many dimensions; helps to prevent overfitting

# Logistic Regression
## What is it?
## What is it useful for?
## What are some examples?
## How do I use it?
### Code
### What are some pitfalls to look out for?
### How do I know it's working
## Logistic Regression vs Naive Bayes

# Homework
## Lab 1: Linear Regression
[Here](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/health_data.csv) is a dataset with the following columns:
- Age
- Years spent receiving their education
- Income divided by 10,000
- Number of visits to the doctor in the previous year

Use the first three columns to predict the number of doctors visits with a linear regression model.
**No need to graph it** since it'd be a 4dimensional plot. *#MindExplodes*

## Lab 2: Logistic Regression

# Reading
- K-nearest neighbors
- Usefulness of machine learning to industry
