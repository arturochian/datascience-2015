# Objective
Students will be able to
- do exploratory work with data sets
- comfortable convert categorical data into numerical data either by dummy variables or numerical encoding
- run different models on the data
- troubleshoot by inspecting data types
- investigate issues (or lack thereof) of multicollinearity using the numpy library

# Pre-work
- [15m glance through these tips on working with categorical data](http://nbviewer.ipython.org/github/rasbt/pattern_classification/blob/master/preprocessing/feature_encoding.ipynb)
- [2m read of this answer on multicollinearity](http://stats.stackexchange.com/a/100209)
- [8m read of these thoughts on multicollinearity](http://blog.minitab.com/blog/adventures-in-statistics/what-are-the-effects-of-multicollinearity-and-when-can-i-ignore-them)
- [8m read of this asnwer on using Python to detect multicollinearity](http://stackoverflow.com/a/25833792)
- Read through all of the code below before class.

For resources on the math behind the collinearity detection, you'll need to revisit eigenvalues and eigenvectors. [Here](https://www.khanacademy.org/math/linear-algebra/alternate_bases/eigen_everything/v/linear-algebra-introduction-to-eigenvalues-and-eigenvectors) is a nice 8 minute intro video from Khan academy. We will not be going over this math in class, just how to use numpy to check the collinearity matrix.

# The Code
We will be building a classifier to determine whether or not an applicant should be approved for credit. The feature names have been masked to protect the privacy of the individuals' data.

[Notebook 1: Exploration and Attempt 1](http://nbviewer.ipython.org/gist/suneel0101/8819fd96e0b855e1a8f9)
[Notebook 2: Use LabelEncoder](http://nbviewer.ipython.org/gist/suneel0101/759dc540077273d56742)
[Notebook 3: Use DictVectorizer](http://nbviewer.ipython.org/gist/suneel0101/b82a31f141a023284063)

# Homework (Lab 1):
Objective: build a classifier on [this Thyroid Disease data set](https://archive.ics.uci.edu/ml/datasets/Thyroid+Disease)

- Run all of the models on the data.
- Alter the value of `C` for the SVC (this is calling tuning) and try to improve its accuracy.
- Alter the value of `n_estimators` for the tree-based classifiers and try to improve the accuracy.
- Alter the value of `cv` when you run the models. What does this do?
- Change the Logistic penalty from 'l2' to 'l1'. How does that affect the accuracy?
