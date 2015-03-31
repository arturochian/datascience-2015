# Objectives
Students will be able to
- explain the backpropagation algorithm
- use momentum and adaptive learning rates to achieve faster convergence
- run a deep belief network on the MNIST handwritten digits dataset

# Pre-work
- ~60m Review [these notebooks from the Practicum](https://github.com/suneel0101/datascience-2015/tree/master/lessons/11_practicum_01#the-code)

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

# Code Example
We're going to beat Random Forest with a Deep Belief Network

## Setup
Before we open up iPython notebook, we'll need to install two things once on the Vagrant machine:

```python

sudo pip install theano
sudo pip install nolearn
```

## Exercise 1: Downloading the Data
1. Download the dataset [here](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/train.csv) and place it under your `/datascience/repos/datasets/` directory.
2. Read the data into a pandas DataFrame
3. Segment the data into `feature_data` and `target_data`

## Exercise 2: Tuning a Random Forest
1. Run Random Forest on it
2. We notice that it takes a long time to run, so run it just on half of the data. We will be running it on half of the data from now on.
3. Parameter Tuning (Number of Trees): Graph the accuracy of the Random Forest against the foll
owing 5 values of `n_estimators`: 5, 20, 100, 1000, 2000.
4. Parameter Tuning (Tree Depth):
5. Parameter Tuning (How many features to randomly sample at each node):

## Exercise 3: Tuning an SVC:
1. Run an SVC with `kernel='rbf'` (Radial basis function) and `C=50`
2. Parameter Tuning: Graph the accuracy of the SVC against the following values of the regularization parameter `C`: .001, .01, .1, 1, 10, 50.
3. Parameter Tuning: Choosing the optimal C from the previous question, run the SVC with kernel='linear'. How does the accuracy change?
4. Parameter Tuning: Using `kernel='rbf'`, C equal to the optimal C, graph the accuracy of SVC against the following 5 different values of `gamma`: .0001, .001, .01, .1, 1.

## Exercise 4: Tuning Logistic Regression
1. Run LogisticRegression on the data.
2. Parameter Tuning: Graph the accuracy of the Logistic Regression against the following values of `C`: .001, .01, .1, 1, 10, 50.
3. Parameter Tuning: Choosing the optimal value of `C`, pass in the l1-norm regularization penalty `penalty='l1'` into the instantiation of the LogisticRegression(). How does the accuracy change?

## Exercise 5: Tuning a Deep Belief Neural Network
I'll walk us through an example.

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

# Further Material If Interested
- [Intro to RBMs](http://blog.echen.me/2011/07/18/introduction-to-restricted-boltzmann-machines/)
- [Coursera on NNs by Goeffrey Hinton](https://class.coursera.org/neuralnets-2012-001/lecture)
