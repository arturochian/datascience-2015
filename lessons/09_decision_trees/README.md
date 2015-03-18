# Objectives
Students will be able to
- Define and apply binary classification trees
- Explain the shortcomings of trees and how to make them competitive with other techniques

# Prework
- [2 min article on what CART Trees are](http://www.quora.com/What-is-a-classification-and-regression-tree-CART)

# Worksheets
- [Use a Flowchart Decision Tree](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Decision+Trees/DT_wksht_1.pdf)
- [Use a Plot-based Decision Tree](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Decision+Trees/DT_wksht_2.pdf)
- [Construct a Decision Tree](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Decision+Trees/DT_wksht_3.pdf)
- [Bootstrap Aggregation](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Decision+Trees/DT_wksht_4.pdf)

# What is a decision tree?
- Decision-making tool that uses a tree-like graph of decisions and consequences
- It repeatedly segments the data by making slices on a given axis until the data is nicely separated into leaves.

# What are the pros/cons of decision trees?
- Intuitive and simple
- Translates directly to nice boolean logic (series of nested if/elses)
- Not as good as the best methods out there, but can be if we use boosting/bagging/random forests to create an ensemble of trees

# Example
We are going to build a classifier that classifies iris plants into one of three classes: Setosa, Versicolour, and Virginica.

The classification will be based on four attributes:
- sepal length (cm)
- sepal width (cm)
- petal length (cm)
- petal width (cm)

[Here](https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.names) is more information on the attributes.

[Here](https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data) is the data.

Here's the code:
```python
import pandas as pd
import numpy as np
from sklearn import tree
from sklearn.cross_validation import cross_val_score

df = pd.read_csv('https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/iris.csv')

decision_tree_clf = tree.DecisionTreeClassifier(
    # dont split if the max number of samples on either side of the slice is less than 2
    min_samples_leaf=2)
features = ["sepal_length", "sepal_width", "petal_length", "petal_width"]

# use K-fold cross validation, with k=10 and get a list of accuracies
scores = cross_val_score(decision_tree_clf, df[features], df["target"], cv=5)

print "\nDECISION TREE:\n"
# print the accuracies
print scores
# print the average accuracy
print scores.mean()
# print the standard deviation of the scores
print np.std(scores)


# now let's try a bagging example
bagging_clf = BaggingClassifier(
    decision_tree_clf,
    # bag using 20 trees
    n_estimators=20,
    # the max number of samples to draw from the training set for each tree
    # there are 105 training samples, so each tree will have .8 * 105
    # data points each to train on, chosen randomly with replacement
    max_samples=0.8,
)

# use K-fold cross validation, with k=5 and get a list of accuracies
# this separates the data into training and test set 5 different times for us
# and finds out the accuracy in each case to get a sense of the average accuracy
scores = cross_val_score(bagging_clf, df[features], df["target"], cv=5)

print "\nDECISION TREE WITH BAGGING:\n"
# print the accuracies
print scores
# print the average accuracy
print scores.mean()
# print the standard deviation of the scores
print np.std(scores)
```

# Homework
# Lab 1: More with Iris Plants
Using the Iris data set in the code above,

- Use kNN to classify the Irises
- Use kNN with Bagging to classify the Irises

How did the mean and std deviation of accuracy compare with the Decision Tree and the Bagged Decision Tree?
