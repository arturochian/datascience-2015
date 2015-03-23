# Objectives
Students will be able to
- define and explain regression trees
- explain linear regression vs tree regression
- use the ensemble methods of bagging, boosting and random forests for both regression and classification

# Pre-work
- [5m answer on Quora on Random Forests in layman's terms](http://qr.ae/QvDfy)
- [5m worksheet we didn't get to tackle last time](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Decision+Trees/DT_wksht_4.pdf)
- 30m reading through the code below

# Worksheets
- [Tree Regression Cost](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Trees+Continued/trees_continued_wksht_1.pdf)
- [Bagging Regression Trees](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Trees+Continued/trees_continued_wksht_2.pdf)
- [Measuring Variable Importance](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Trees+Continued/trees_continued_wksht_3.pdf)
- [Gradient Boosting](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Trees+Continued/trees_continued_wksht_4.pdf)

# Regression Trees
- similar to classification trees in that we try to separate the data with a sequence of slices on the input axes
- in classification, the cost function we were trying to minimize was the mis-classification rate
- in regression, the cost function is the residual sum of squares (RSS)

# Bagging for Regression Trees
- regression trees have the same issue of high variance as their classification tree analog. small variations in the underlying training set could lead to drastically different trees
- in classification, we 'bagged' trees by bootstrapping M random subsamples of the data and training M trees and taking the **majority vote** of those trees
- in regression, we bootstrap those M trees but instead, we take the **average* of the M tree predictions

# Measuring Variable Importance
- In regression, if we have p input features and N slices, we can measure the relative of a feature in 1,...p by comparing the total reduction in RSS across the axes.
- Similarly in classification, we can measure the total reduction in the [Gini impurity](http://en.wikipedia.org/wiki/Decision_tree_learning#Gini_impurity)  measure.

# Lab 1: Tree Regression
[Here](http://nbviewer.ipython.org/gist/suneel0101/4dedee4dbeffe0e1bbf8) is the corresponding iPython notebook.
Below is the full, uninterrupted code.

```python
from sklearn.datasets import load_boston
from sklearn.cross_validation import cross_val_score, train_test_split
from sklearn.tree import DecisionTreeRegressor
boston = load_boston()

print boston.DESCR

reg = DecisionTreeRegressor()

# split into training 80% and test 20%
X_train, X_test, y_train, y_test = train_test_split(boston.data, boston.target, test_size=0.3, random_state=42)
reg.fit(X_train, y_train)

# what's the R^2 on the test set? .847, pretty good!
print "R^2 {}".format(reg.score(X_test, y_test))

# how many slices?
print "Tree depth: {}".format(reg.tree_.max_depth)

# these are the feature importances; the ones with e-01 are more important.
reg.feature_importances_

# let's try linear regression
from sklearn.linear_model import LinearRegression
linear_reg = LinearRegression()

# split into training 80% and test 20%
X_train, X_test, y_train, y_test = train_test_split(boston.data, boston.target, test_size=0.3, random_state=42)
linear_reg.fit(X_train, y_train)

# what's the R^2 on the test set? .847, pretty good!
print "R^2 {}".format(linear_reg.score(X_test, y_test))
```


# What are Random Forests?
- similar to bagging, we bootstrap M trees based on random subsamples of the training data
- but at each node when we decide to split, instead of considering all of the axes 1, ..., p, we only consider a random subset of those axes
- usually the random subset of axes is of size sqrt(p), where p is the total number axes (a.k.a features)
- this procedure is the same for classification as it is for regression

# Boosting Trees
- another way of taking an average of trees, except unlike bagging and random forests, it's *sequential*
- in random forests and bagging, we treat all trees alike and take the majority vote or average
- in boosting, we start with a simple tree that maybe has a lot of error (called a weak learner since it gets a lot of stuff wrong) and we add on trees to it to fit its error
- here's the procedure
1. create a simple small tree to fit the data, call it f<sub>1</sub>
2. look at the residual errors and fit a tree to predict the residual errors and call it f<sub>2</sub>
3. add f<sub>1</sub> and f<sub>2</sub>, discounting the latter, so f= f<sub>1</sub> + af<sub>2</sub>, where a (or alpha) is the learning rate or shrinking parameter.
4. rinse and repeat

This is called **gradient boosting* because it is an analogous problem to gradient descent. The smaller we make a, the more trees are required to accurately fit the data but it's less prone to overfitting.

The beauty of this method is that each indivudal f<sub>i</sub> is quite simple and weak in predictive power, but their weighted sum is sophisticated and accurate.

The analog for classification is AdaBoost, but we won't get into the math here because it's quite a bit harder.

# General Techniques
Bagging and boosting are general techniques that can be used not just on tree classifiers but other classifiers as well.

# Lab 2: Ensemble Classification to Diagnose Breast Cancer
[Here](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/wd_breast_cancer.csv) is the data.

[Here](https://archive.ics.uci.edu/ml/machine-learning-databases/breast-cancer-wisconsin/wdbc.names) is a description of the data.

[Here](http://nbviewer.ipython.org/gist/suneel0101/015d235afba42d466274) is the iPython notebook.

Below is the full, uninterrupted code.

```python
import pandas as pd
import numpy as np
from sklearn.cross_validation import cross_val_score
from sklearn import tree
from sklearn import ensemble
from sklearn import neighbors
from sklearn import linear_model
from sklearn import svm

df = pd.read_csv(
    'https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/wd_breast_cancer.csv',
    # this csv has no column names. There are 32 inputs, all measurements that are detailed here:
    # https://archive.ics.uci.edu/ml/machine-learning-databases/breast-cancer-wisconsin/wdbc.names
    header=None)

# The first column is just the id, so it's not important
# The second column is the diagnosis, either M (malignant) or B (benign)

# for documentation on how this indexing works: http://pandas.pydata.org/pandas-docs/dev/indexing.html
target = df[1]
feature_data = df.iloc[:,2:]

print "\nDECISION TREE\n"
decision_tree_clf = tree.DecisionTreeClassifier()
scores = cross_val_score(decision_tree_clf, feature_data, target, cv=5)
print "Mean: {}".format(scores.mean())
print "Std Dev: {}".format(np.std(scores))

print "\nRANDOM FOREST\n"
# see what happens as we bump up the number of estimators
random_forest_clf = ensemble.RandomForestClassifier(n_estimators=10)
scores = cross_val_score(random_forest_clf, feature_data, target, cv=5)
print "Mean: {}".format(scores.mean())
print "Std Dev: {}".format(np.std(scores))

print "\nBOOSTED TREES\n"
boosted_clf = ensemble.AdaBoostClassifier(n_estimators=10)
scores = cross_val_score(boosted_clf, feature_data, target, cv=5)
print "Mean: {}".format(scores.mean())
print "Std Dev: {}".format(np.std(scores))

print "\nkNN\n"
knn_clf = neighbors.KNeighborsClassifier(n_neighbors=7)
scores = cross_val_score(knn_clf, feature_data, target, cv=5)
print "Mean: {}".format(scores.mean())
print "Std Dev: {}".format(np.std(scores))

print "\nLogistic\n"
logistic_clf = linear_model.LogisticRegression()
scores = cross_val_score(logistic_clf, feature_data, target, cv=5)
print "Mean: {}".format(scores.mean())
print "Std Dev: {}".format(np.std(scores))

print "\nSVC\n"
# C is a tuning a parameter (remember it's our error budget for how much slack we give the hyperplane)
# mess around with C and see what happens
support_vector_clf = svm.LinearSVC(C=3)
scores = cross_val_score(support_vector_clf, feature_data, target, cv=5)
print "Mean: {}".format(scores.mean())
print "Std Dev: {}".format(np.std(scores))
```

## Exercises on this code
1. Change the SVC error budget C to 0.5, 1, 5, 10, 100. Which is the most accurate?
2. Change the n_estimators for AdaBoost and RandomForest to 5, 10, 20, 50. Which of each is the most accurate?
3. Find the most important variables according to the RandomForest classifier. Remember that we had to first `fit()` the classifier to a specific training set. Refer to the tree regression code earlier on in this document for an example of how to do so.

# Homework (Lab 3): Image Recognition
**Objective**: Predict what number a certain image is based on 4 attributes extracted from the imgae.

[Here](https://archive.ics.uci.edu/ml/datasets/banknote+authentication) is the data.

1. Save the data to a file and read it in.
2. Run all of the classifiers we've learned so far on it.
3. Tune the classifiers to maximize their predictive power.
4. How accurate were you able to get each classifier? Which one(s) performed the best?
