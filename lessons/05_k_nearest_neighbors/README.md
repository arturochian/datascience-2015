# Objectives
Students will be able to
- Define and apply the k-Nearest Neighbors classifier
- Give practical and relevant examples from industry

# Worksheets

# k-Nearest Neighbors (kNN) Classifier
## What is it?
- Given a set of data points that have been classified, when a new data point comes in, associate it with the class that is most heavily represented within the smallest ball that contains k neighbors.

## What are some applications?
- [Financial distress predictions](http://www.academia.edu/4607757/Application_of_K-Nearest_Neighbor_KNN_Approach_for_Predicting_Economic_Events_Theoretical_Background)
- [Breast cancer diagnosis](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2243774/)
- Handwriting detection and other computer vision
- Customer segmentation

## How does it work?
- The algorithm tries to find the
- Usually use the Euclidean distance function
- How do we select k? k ~ sqrt(n) where n is the number of dimensions.

## What are some things to look out for?
- [Curse of dimensionality](http://en.wikipedia.org/wiki/Curse_of_dimensionality)
- More than 10 dimensions and we need to do dimensionality reduction

## How do I know it's working
- Use cross-validation

## Set Up for Our Code
### Classify wine as high-quality or not based on its attributes

1. download [this csv]()
2. move that dataset under your /repos/datasets/ directory on your local machine (NOT VAGRANT)
3. log into vagrant from the /vm/ directory as usual
5. run `sudo ipython notebook --profile=dst`
6. paste the following code into iPython notebook and run it

```python
# ****** First, let's choose which value of K will do the best ******
import pandas as pd
import pylab as pl
from sklearn.neighbors import KNeighborsClassifier


df = pd.read_csv("https://s3.amazonaws.com/demo-datasets/wine.csv")

# This creates an array of Trues and False, uniformly distributed such that
# around 30% of the items will be True and the rest will be False
test_idx = np.random.uniform(0, 1, len(df)) <= 0.3

# The training set will be ~30% of the data
train = df[test_idx==True]
# The test set will be the remaining, ~70% of the data
test = df[test_idx==False]

features = ['density', 'sulphates', 'residual_sugar']

results = []
# range(1, 51, 2) = [1, 3, 5, 7, ...., 49]
for n in range(1, 51, 2):
    clf = KNeighborsClassifier(n_neighbors=n)
    # train the classifier
    clf.fit(train[features], train['high_quality'])
    # then make the predictions
    preds = clf.predict(test[features])
    # very simple and terse line of code that will check the accuracy
    # documentation on what np.where does: http://docs.scipy.org/doc/numpy/reference/generated/numpy.where.html
    # Here is a simple example: suppose our predictions where [True, False, True] and the correct values were [True, True, True]
    # The next line says, create an array where when the prediction = correct value, the value is 1, and if not the value is 0.
    # So the np.where would, in this example, produce [1, 0, 1] which would be summed to be 2 and then divided by 3.0 to get 66% accuracy
    accuracy = np.where(preds==test['high_quality'], 1, 0).sum() / float(len(test))
    print "Neighbors: %d, Accuracy: %3f" % (n, accuracy)

    results.append([n, accuracy])

results = pd.DataFrame(results, columns=["n", "accuracy"])

pl.plot(results.n, results.accuracy)
pl.title("Accuracy with Increasing K")
pl.show()

# ****** Now, let's see how accurate the predictor is ******
results = []
# let's try two different weighting schemes, one where we don't worry about the distance
# another where we weight each point by 1/distance
for w in ['uniform', 'distance']:
    clf = KNeighborsClassifier(3, weights=w)
    w = str(w)
    clf.fit(train[features], train['high_quality'])
    preds = clf.predict(test[features])

    # For an explanation of this line, refer to my explanation of this same line above
    accuracy = np.where(preds==test['high_quality'], 1, 0).sum() / float(len(test))
    print "Weights: %s, Accuracy: %3f" % (w, accuracy)

    results.append([w, accuracy])

results = pd.DataFrame(results, columns=["weight_method", "accuracy"])
print results
```

The above code was taken from [this blog post](http://blog.yhathq.com/posts/classification-using-knn-and-python.html). I merely added some documentation.

### Separate into Groups and Improve the kNN classifier
- add other features from the data
- change the value of k


## Advanced techniques for Building Good Models
- Dimensionality reduction
- Weighting the votes

# Homework
## Lab 1: kNN vs Logistic
- [Here](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/bank-additional-full.csv) is a dataset on a direct marketing campaign run by a Portuguese bank and the output y is whether or not they subscribed to a term deposit.
**Note**: the columns are delimited by semicolons rather than commas. Just pass `delimiter=';'` as a keyword argument in the call `pandas.read_csv(.....)` when you read the data in.

- [Here](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/bank-additional-names.txt) is a description of what each column means.

### Part 1
- Apply k-Nearest Neighbors on subsets of the columns and using cross validation see how the accuracy changes.
- Now use all of the columns for your kNN classifier and see what the accuracy is.

### Part 2
- Use logistic regression on the data, perhaps bucketing some of the column data into discrete categories rather than being continuous values.
- Try logistic regression on subsets of the columns.

## Part 3
- Between logistic regression and kNN, which performed better in predicting which customers would sign on for a term deposit?

# Reading
- [Support Vector Machines in laymen's terms](http://www.quora.com/What-does-support-vector-machine-SVM-mean-in-laymans-terms)
