# Objectives
Students will be able to
- confidently tune parameters for the other classifiers we've studied
- run a deep belief network on the MNIST handwritten digits dataset
- explain the backpropagation algorithm
- use momentum and adaptive learning rates to achieve faster convergence

# Pre-work
- ~45m Review [these notebooks from the Practicum](https://github.com/suneel0101/datascience-2015/tree/master/lessons/11_practicum_01#the-code)

# Worksheets
- [Adding Momentum to Our Training Procedure](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/ANNs_ctd/ANN_ctd_wksht_1.pdf)
- [Adaptive Learning Rate](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/ANNs_ctd/ANN_ctd_wksht_2.pdf)

# Backpropagation
- an algorithm for updating the weights in a multilayer perceptron
- utilizes the Chain Rule of derivatives
- not the only way to update weights but certainly much more feasible than genetic algorithms that seek to mimic natural selection

# ANNs for Regression
- we can use ANNs for regression as well
- loss function is the MSE (mean squared error)
- output units correspond to the y we want to predict

# Challenges of training ANNs
- gradient is unstable the more complex (deep) the network gets

# Approaches to better convergence
- momentum in the weight updates
- adaptive learning rate
- tune the network size
- try different architectures

# Convolutional Neural Networks (CNNs)
- seriously state of the art in NLP, speech recognition, machine vision, even video classification
- biologically inspired
- nice intro article [here](http://colah.github.io/posts/2014-07-Conv-Nets-Modular/)

# ConvNetJS
- Let's check [this](http://cs.stanford.edu/people/karpathy/convnetjs/demo/cifar10.html) out
- Live demo of state of the art image classification

# Code Example: Handwritten Character Recognition
We're going to beat Random Forest with a Deep Belief Network.

## Setup
Before we open up iPython notebook, we'll need to install two things once on the Vagrant machine:

```python

sudo pip install theano
sudo pip install nolearn
```

## Exercise 1: Downloading the Data
1. Download the dataset [here](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/train.csv) and place it under your `/datascience/repos/datasets/` directory.
2. Read the data into a pandas DataFrame.
3. Segment the data into `feature_data` and `target_data`
4. Using `train_test_split` to segment the data into 30% test set, 70% training set.
5. We can't use all the data otherwise it'll take too long to train the models, so let's just take the first 1/8th of the data.

## Exercise 2: Tuning a Random Forest
1. Run Random Forest on the data.
2. Parameter Tuning (Number of Trees): Graph the accuracy of the Random Forest against the following values of `n_estimators`: 5, 20, 100, 500.
3. Parameter Tuning (Tree Depth): Graph the accuracy of the Random Forest against the following values of `max_depth`: 10, 20, 40.
4. Parameter Tuning (How many features to randomly sample at each node): Holding `n_estimators=100`, `max_depth=20`, now graph the accuracy against the following values of `max_features`: ["auto", "log2", 0.3] (auto means at each node we should consider slices on sqrt(number of features), log2 means we consider log2(number of features) and .3 means we consider .3 * number of features.

## Exercise 3: Tuning an SVC
1. Run an SVC on the data with `kernel='rbf'` (Radial basis function) and `C=1`. What is `C` again?
2. Parameter Tuning: Graph the accuracy against the following values of kernel: ['linear', 'poly', 'sigmoid']. How does the accuracy change?
3. Parameter Tuning: Graph the accuracy of the SVC against the following values of the regularization parameter `C`: .001, .01, .1

## Exercise 4: Tuning Logistic Regression
1. Run LogisticRegression on the data.
2. Parameter Tuning: Graph the accuracy of the Logistic Regression against the following values of `C`: .001, .01, .1, 1, 10, 50.
3. Parameter Tuning: Choosing the optimal value of `C`, and let's graph the accuracy against our tuning of the regularization penalty, using the following values of penalty: 'l1', 'l2'

## Exercise 5: Run Random Forest on Full Dataset
1. Go through the tuning paramters in exercise 1, but this time for the full dataset.
2. What is the best choice for `n_estimators`?
3. What is the best choice for `max_depth`?
4. What is the best choice for `max_features`?
5. Print out the  [`classification_report`](http://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html).

## Exercise 6: Tuning a Deep Belief Neural Network
I'll walk us through an example and show some improvements via tuning.

As an exercise, try the following:
### Tuning the learning rate
- Run for epochs=5, learn_rates=.01
- Run for epochs=5, learn_rates=.05
- Run for epochs=5, learn_rates=.1
How does it change?

### Tuning the decay rate
Pick the best one from above and now let's tune the decay rtae.
- Run for learn_rate_decays=.8
- Run for learn_rate_decays=.5
- Run for learn_rate_decays=.3

### Tuning the hidden layer size
Pick the best from the previous two experiments and now we'll tune the hidden layer size.
- Instead of 300 hidden units, try 500 hidden units
- Try 100 hidden units
- Try 10 hidden units

# Practicum 2 Notebook
[Here](http://nbviewer.ipython.org/gist/suneel0101/36d4e44b89a8b847dbe5) is the iPython notebook with all the code from the second practicum.

# Homework (due April 8)
- Decide on Data set & problem you want to solve for the final project
- Feel free to reach out to me or Sonia if you have questions about this!

# Further Material If Interested
- [Intro to RBMs](http://blog.echen.me/2011/07/18/introduction-to-restricted-boltzmann-machines/)
- [Coursera on NNs by Goeffrey Hinton](https://class.coursera.org/neuralnets-2012-001/lecture)
