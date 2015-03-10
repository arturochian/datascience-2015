# Objective
- Define and apply SVMs for binary classification

# Worksheets
- [Hyperplanes in Two Dimensions](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/SVM/SVM_worksheet_1.pdf)
- [Enlarging the Feature Space to Separate Non-Separable Data](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/SVM/SVM_worksheet_2.pdf)
- [Dot Products and the Kernel Function](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/SVM/SVM_worksheet_3.pdf)

# What is a Support Vector Machine?
- A binary linear classification algorithm that separates our classes geometrically in space.
- We can extend it to multi-class classification

# Some applications of SVMs
- image recognition (hand-written characters, facial recogntion)
- classify proteins and other chemical compounds
- natural language processing (convert text into some numerical vectorsof the features)
- [financial applications](http://www.svms.org/finance/) like
- bioinformations ([cancer classification](http://www.ntu.edu.sg/home/elpwang/PDF_web/05_SVM_basic.pdf))
- gene expression data classification
- recommendation engines (e.g. [news article recommendation engine](http://www.cs.cmu.edu/~anatoleg/gershman-wolfe-fink-carbonell.pdf))
- speech recognition

# What is a hyperplane?
If we have a hyperplane in **p** dimensions, we can describe it with the following equation:
a<sub>0</sub> + a<sub>1</sub>x<sub>1</sub> + ... a<sub>p</sub>a<sub>p</sub> = 0

**Question**: If p = 2, what is the hyperplane?

Terminology: (a<sub>1</sub>, ..., a<sub>p</sub>) is called the **normal vector** because it perpendicular to the surface of the hyperplane it describes.

# Definition of separating hyperplane
Given two classes A and B, an input vector X gets classified as Y where Y = 1 if X is in class A and Y = -1 if X is in class B.

Then we call a hyperplane f(X) = 0 separating if Y * f(X) > 0 for all X in the dataset.

# Maximal Margin Classifier
Given an infinite family of hyperplanes that could separate the classes, how do we choose?

**Answer**: Find the one that makes the biggest gap (margin) between the two classes.

# Problems with hyperplanes
## Non-separable data
Often our data is not simply separable with a hyperplane.

If the number of samples is less than the number dimensions, than yes we can always find a hyperplane. This is the case in areas like genomics.

But when number of samples exceeds the number of dimensions, we will not always be able to find a separating hyperplane.

## Noisy data
Noisy data can really affect the solution for the maximal margin classifier, so the hyperplane separation method is **NOT** robust.

Support Vector Classifiers are our saving grace!

# SVCs
- maximizes a **soft margin**
- helps solve the noisiness issue and in many cases the non-separable data, but not always!

Feature expansion can help us!

# Feature expansion
- Enlarge the set of features x<sub>1</sub>, ..., x<sub>n</sub> by adding transformations like x<sub>1</sub><sup>2</sup>, x<sub>1</sub>x<sub>2</sub>, x<sub>1</sub>x<sub>2</sub><sup>2</sup>,... as features.
- Kernel trick lets us get the benefits of a higher-dimensional space without the computational complexity

# The Code: Handwritten Digit Recognizer
[Check it the iPython notebook here](http://nbviewer.ipython.org/gist/suneel0101/9b665a2dd71bf60d50da)

```python
import matplotlib.pyplot as plt

from sklearn import datasets
# our support vector machine classifier!
from sklearn import svm

# load digits dataset
digits = datasets.load_digits()

# let's see what this dataset is all about
print digits.DESCR

# let's see what keys this digits object has
print digits.keys()

# Let's see what classes we want to put digits into
print digits.target_names

# Let's pic one and see what it looks like
first_digit = digits.data[0]
print first_digit

# But what do all of those columns mean!?!?!
# Let's go to the whiteboard and find out...

# let's see what the first digit was tagged as
print digits.target[0]

# now let's see what digits.images[0] is
# it's just the first_digit array reshaped as an 8 x 8 matrix
print digits.images[0]

# let's instantiate our Support Vector Classifier
classifier = svm.SVC(gamma=.0001, C=100)

# how many data points do we have?
print len(digits.data)

# let's createa  training set of the first 1597 of the 1797 data points
x_training, y_training = digits.data[:-200], digits.target[:-200]

# now let's train the classifier on the training data
classifier.fit(x_training, y_training)

print "Prediction {}".format(classifier.predict(digits.data[1600]))
print digits.target[1600]

# show the image
plt.imshow(
    digits.images[1600],
    cmap=plt.cm.gray_r,
    interpolation="nearest"
)
plt.show()

# Wow!!!! Let's see what the accuracy is
# Let's go from digits.data[-200] all the way to digits.data[-1]
correct = 0
indices = range(-200, 0)
for i in indices:
    # if we were correct
    if classifier.predict(digits.data[i])[0] == digits.target[i]:
        correct += 1
accuracy = float(correct) / len(indices)

print "SVC Accuracy: {}".format(accuracy)

# Let's try using kNN
from sklearn.neighbors import KNeighborsClassifier

knn_clf = KNeighborsClassifier(n_neighbors=25)
# train the classifier
knn_clf.fit(x_training, y_training)

# Let's see what the accuracy is
# Let's go from digits.data[-200] all the way to digits.data[-1]
correct = 0
indices = range(-200, 0)
for i in indices:
    # if we were correct
    if knn_clf.predict(digits.data[i])[0] == digits.target[i]:
        correct += 1
accuracy = float(correct) / len(indices)

print "kNN Accuracy: {}".format(accuracy)

# Let's try with Logistic Regression
from sklearn.linear_model import LogisticRegression

log_reg = LogisticRegression()
log_reg.fit(x_training, y_training)

# Let's see what the accuracy is
# Let's go from digits.data[-200] all the way to digits.data[-1]
correct = 0
indices = range(-200, 0)
for i in indices:
    # if we were correct
    if log_reg.predict(digits.data[i])[0] == digits.target[i]:
        correct += 1
accuracy = float(correct) / len(indices)

print "Logistic Regression Accuracy: {}".format(accuracy)
```

# Homework
## Lab 1: Playing around with the handwritten digit recognizer

1. What happens to the accuracy when you change `gamma` in the SVM to .01? .1? 1? 0?
2. What happens to the accuracy when you train the SVM on the first 500 samples? first 1700 samples?
