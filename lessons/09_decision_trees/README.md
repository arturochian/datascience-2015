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
from sklearn import tree
from sklearn.cross_validation import train_test_split

df = pd.read_csv('https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/iris.csv')

print df.describe()

# split the data into 60% test set, 40% training set
training_set, test_set = train_test_split(df, test_size = 0.6)

# the features are the first 4 columns of the data, with the last column being the target class
feature_data = training_set[:, :4]
target_data = training_set[:, 4]

# train the tree
clf = tree.DecisionTreeClassifier(
    # dont split if the max number of samples on either side of the slice is less than 2
    min_samples_leaf=2)
clf = clf.fit(feature_data, target_data)

# prepare the test sets
test_feature_data = test_set[:, :4]
test_target_data = test_set[:, 4]

# make the predictions
predictions = clf.predict(test_feature_data)

# let's see how accurate it was
accuracy = np.where(predictions==test_target_data, 1, 0).sum() / float(len(test_target_data))

print accuracy
```

### Exercise: Try running the code 10 times. Does the accuracy change?

# Homework
## Lab 1
