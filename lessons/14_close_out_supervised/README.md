# Objectives
Students will be able to
- recall the key learnings from the latest practicum
- explain how single and multi-layer neural networks work
- list some of the main tuning paramaters in a neural network
- tune those parameters in the code
- close out supervised learning

# Programme
1. Reflect briefly on the practicum, lessons learned
2. Review single-layer neural networks
3. Cover multi-layer neural networks and backpropagation
4. Explore the tuning parameters - there are many (epochs, number of hidden inputs in the hidden layer, learning rates, learning rate decay, momentum, etc)
5. The code exercise below: we will train a neural network
6. The end-of-section summary exercises below

# Pre-Work
- Review your notes on Naive Bayes, Logistic, kNN, SVM, Trees, Ensembles of Trees, and ANNs.
- Review your code from practicum no. 2.

# Worksheets
- [Momentum](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/ANNs_ctd/ANN_ctd_wksht_1.pdf)

# Code Exercses
We'll be working again with the MNIST set but this time we'll try our hands at training the neural network.

[Here's](http://nbviewer.ipython.org/gist/suneel0101/8e26f317b5ecc0f012b9) the iPython notebook to get you started. It also contains the instructions for the exercise.

# End-of-Section Summary Exercises and Homework
## Instructions
- We'll separate into groups of 3-4 and go through each of the below sections.
- The order of the algorithms will be somewhat randomized.
- One group will present their answers in the front of the class. This group will be selected at random.
- The answers to this exercise must be submitted as homework and should be kept as a guide for future datascience.

## Naive Bayes
1. What kind of input (categorical/continuous) does the Naive Bayes classifier take?
2. Can the Naive Bayes classifier do multi-class classification?
3. What does the 'Bayes' in Naive Bayes refer to?
4. What does the 'Naive' in Naive refer to?
5. When should we use Naive Bayes?
6. When should we definitely NOT use Naive Bayes?
7. How does Naive Bayes do with high dimensionality?
8. Does this classifier give us an interpretable probability?
9. What parameters can we tune, if any?

## Logistic Regression
0. What is the equation for logistic regression?
1. What kind of input does Logistic take?
2. Can it handle high dimensional input?
3. What is regularization and what is it for?
4. When should we regularize?
6. Does this classifier give us an interpretable probability?
7. What parameters can we tune?

## k Nearest Neighbors
0. What does the k in k Nearest Neighbors refer to?
1. If k is too, high what can happen?
2. Should we scale our features? What happens if we don't?
3. When should we use k Nearest Neighbors?
4. When should we definitely NOT use k Nearest Neighbors?
5. Can k Nearest Neighbors handle high dimensionality?
6. Given a k-neighborhood of points from different classes, say A, B and C, how do we decide which class wins in that neighborhood?
7. What are some ways that we can weight the votes? Why would we want to do so?
8. What parameters can we tune?
9. Do we get an interpretable probability?

## Support Vector Machines
0. How does SVM separate the data?
1. What happens when we can't? What do we do?
2. What is the kernel trick?
3. What does regularization mean for SVMs?
4. Can SVMs handle high dimensionality?
5. When should we use SVMs? What kinds of applications in particular?
6. When should we NOT use SVMs?
7. What can happen when we use an aggressive kernel function?
8. What parameters can we tune?
9. Do we get an interpretable probability?

##  Trees & Ensembles of Trees
0. How does a classification tree separate the data?
1. What kind of inputs?
1. What are some problems with single trees?
2. Why do we use ensembles of trees?
3. Describe bagging
4. Describe random forests
5. Why are these techniques better than single trees?
6. Do we get an interpretable probability?
7. What are some parameters we can tune?
8. When should we use trees?
9. When should we NOT use trees?
10. Can we use trees for regression, not just classification?
11. When to use regression trees vs linear regression?

## ANNs
0. How do the inputs and the weights play a role in classifying a new sample?
1. What is the equation of the perceptron?
1. What does logistic function or the threshold function have to do with anything?
1. How do we train the weights?
2. How does a multi-layer perceptron work?
3. When should we use ANNs? What kinds of applications?
4. Why should we NOT use ANNs?
5. How does the training difficulty compare with the other algorithms?
6. What are some of the parameters we can tune?
7. How do we get a probability interpretation?
8. What kind of inputs (continuous or categorical)?
8. Can we do multi-class classification?
9. Can we use ANNs for regression, not just classification?
