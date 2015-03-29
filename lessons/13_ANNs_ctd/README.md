# Objectives
Students will be able to
- explain the backpropagation algorithm
- use momentum and adaptive learning rates to achieve faster convergence
- run a deep belief network on the MNIST handwritten digits dataset

# Pre-work
- [20m Medium Article on Google and Deep Learning, interview with Geoffrey Hinton](https://medium.com/backchannel/google-search-will-be-your-next-brain-5207c26e4523)
- [20m TED talk by Jeremy Howard on Deep Learning](http://www.ted.com/talks/jeremy_howard_the_wonderful_and_terrifying_implications_of_computers_that_can_learn?language=en)

# Worksheets
- [Adding Momentum to Our Training Procedure](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/ANNs_ctd/ANN_ctd_wksht_1.pdf)
- [Adaptive Learning Rate](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/ANNs_ctd/ANN_ctd_wksht_2.pdf)
- [Neural Network Artists](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/ANNs_ctd/ANN_ctd_wksht_3.pdf)

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

Download the dataset [here](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/train.csv) and place it under your `/datascience/repos/datasets/` directory.

[Here's](http://nbviewer.ipython.org/gist/suneel0101/6316c4567c9538f02573) the ipython notebook.

Befoer we open up iPython notebook, we'll need to install two things once on the Vagrant machine:

```python

sudo pip install theano
sudo pip install nolearn

```

# Lab 1 (Homework if not finished in class)
## Tuning the learning rate
- Run for epochs=5, learn_rates=.01
- Run for epochs=5, learn_rates=.05
- Run for epochs=5, learn_rates=.1
How does it change?

## Tuning the decay rate
Pick the best one from above and now let's tune the decay rtae.
- Run for learn_rate_decays=.8
- Run for learn_rate_decays=.5
- Run for learn_rate_decays=.3

## Tuning the hidden layer size
Pick the best from the previous two experiments and now we'll tune the hidden layer size.
- Instead of 300 hidden units, try 500 hidden units
- Try 100 hidden units
- Try 10 hidden units
Which one did the best?

It's hard to train these things!
