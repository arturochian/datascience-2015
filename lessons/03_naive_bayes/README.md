# Overview
## Objective: Learn the underpinning and intuition behind Naive Bayes Classifier and apply the classifier to some real problems.

# Slides
- This time, there were just a few. Most of our learning was through the worksheets and whiteboarding. Regardless, here are the slides: https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/slides/naive_bayes_slides.pdf

# Worksheets
- [Worksheet 1: Univariate Conditional Probability on Tweets](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Worksheet_1_conditional_probability_univariate.pdf)
- [Worksheet 2: Multivariate Conditional Probability on Tweets](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Worksheet_2_conditional_probability_multivariate.pdf)

# Example of Naive Bayes
## Lab: Our First Naive Bayes Classifier
### Objective: Learn how to use the nltk library's NaiveBayesClassifier and experiment with features to improve the accuracy of the classifier.
We will create a Twitter Sentiment Analysis Classifier.

## Download the Data
1. Download the data from here: https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/clean_twitter_data.csv
2. Create a directory under your local machine's (not vagrant) /repos/ folder called /datasets/
3. Move the `clean_twitter_data.csv` file to /datasets/

## SSH into the Vagrant Machine
1. Once in, run `sudo pip install nltk`
2. Then boot up ipython notebook: `sudo ipython notebook --profile=dst` and open up the notebook in Chome.

## Run This Code
Paste this code into notebook:

```python
import nltk
...
```
## Accuracy Contest
- Separate in to groups of 2 or 3.
- Experiment with the feature set.
- With a training set of 20% of the shuffled data, test set of 80% of the shuffled data, compete to get the highest accuracy classifier.


# Homework
## Lab: SMS Spam Detection Classifier
### Objective: Create a Naive Bayes Classifier that accurately classifies SMSs as spam vs ham
Create a new repo called `supervised-learning-algos`. Within this repo, add a top-level README of something to the effect of:
```
In this repository, I demonstrate mastery of the most common supervised learning algorithms:
- Linear Regression
- Logistic Regression
- Naive Bayes Classifier
- K-Nearest Neighors
- Support Vector Machines
- Artificial Neural Networks
- Random Forests
- Decision Trees

```
Then create a directory under `supervised-learning-algos` called `naive-bayes`.
Under `naive-bayes` create a README.md with the description of this SMS spam detection problem and the link below to the data source so that folks looking at your GitHub will be able to verify how awesome you are.

- Data source: https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/sms_spam_or_ham.csv
- Warning: **Do not open in excel!** - this will mess up the encoding and you'll have to delete the file and re-download it.
- Description of data: each row is of the form "label, body" where label is either spam or ham (not spam) and body is the SMS body.
- Description of challenge: Using code similar to what we did for Twitter sentiment analysis, create a classifier and experiment with the feature set to most accurately predict whether an SMS is spam or ham.

# Reading for next time
## Linear Regression (Review)
- [Simple Linear Regression (8min)](https://www.youtube.com/watch?v=KsVBBJRb9TE)
- [Least Squares Minimization (7min)](https://www.youtube.com/watch?v=coQAAN4eY5s)
- [Multivariate Regression (20min)](https://www.youtube.com/watch?v=dQNpSa-bq4M)
- [Explanation of R^2 test](http://blog.minitab.com/blog/adventures-in-statistics/regression-analysis-how-do-i-interpret-r-squared-and-assess-the-goodness-of-fit)

## Logistic Regression (Preview)
- [Layman's explanation of logistic regression](http://qr.ae/EbWax)
- [Layman's explanation of the "math" behind logistic regression](http://qr.ae/EbWJ3)
