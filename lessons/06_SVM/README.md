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

# How does it work?
- Maximal Margin Classifier
- Expand the feature set if we need to project to a higher-dimensional space
- Kernel trick lets us get the benefits of a higher-dimensional space without the computational complexity

# The Code: Handwritten Digit Recognizer
[Check it out here](http://nbviewer.ipython.org/gist/suneel0101/9b665a2dd71bf60d50da)

# Homework
## Lab 1: Playing around with the handwritten digit recognizer

1. What happens to the accuracy when you change `gamma` in the SVM to .01? .1? 1? 0?
2. What happens to the accuracy when you train the SVM on the first 500 samples? first 1700 samples?
