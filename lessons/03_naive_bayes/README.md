# Objective
### Students will be able to define, derive and apply the Naive Bayes Classifier.

# Slides
- This time, there were just a few. Most of our learning was through the worksheets and whiteboarding. Regardless, here are the slides: https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/slides/naive_bayes_slides.pdf

# Worksheets
- [Worksheet 1: Univariate Conditional Probability on Tweets](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Worksheet_1_conditional_probability_univariate.pdf)
- [Worksheet 2: Multivariate Conditional Probability on Tweets](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Worksheet_2_conditional_probability_multivariate.pdf)

# Example of Naive Bayes
## Lab 1: Our First Naive Bayes Classifier
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
# built-in python library for interacting with .csv files
import csv
# natural language toolkit is a great python library for natural language processing
import nltk
# built-in python library for utility functions that introduce randomness
import random


def get_length_bucket(tweet_length):
    """
    buckets the tweet length into either short / medium / long
    """
    if tweet_length < 20:
        return short
    elif tweet_length < 80:
        return "medium"
    else:
        return "long"


def twitter_features(tweet):
    """
     Returns a dictionary of the features of the tweet we want our model
    to be based on, e.g. tweet_length.

    So if the tweet was "Hey!", the output of this function would be
    {
        "length": "short"
    }

    If the tweet was "Hey this is a really great idea and I think that we should totally implement this technique",
    then the output would be
    {
        "length": "medium"
    }
    """
    return {
        "length": get_length_bucket(tweet)
    }


def get_feature_sets():
    """
    # Step 1: This reads in the rows from the csv file which look like this:
    0, I'm so sad
    1, Happy!

    where the first row is the label; 0=negative, 1=positive
    and the second row is the body of the tweet

    # Step 2: Turn the csv rows into feature dictionaries using `twitter_features` function above.

    The output of this function run on the example in Step 1 will look like this:
    [
        ({"length": "short"}, 0), # this corresponds to 0, I'm so sad
        ({"length": "short"}, 1) # this corresponds to 1, Happy!
    ]

    You can think about this more abstractly as this:
    [
        (feature_dictionary, label), # corresponding to row 0
        ... # corresponding to row 1 ... n
    ]
    """
    # open the file, which we've placed at /home/vagrant/repos/datasets/clean_twitter_data.csv
    # 'rb' means read-only mode and binary encoding
    f = open('/home/vagrant/repos/datasets/clean_twitter_data.csv', 'rb')

    # let's read in the rows from the csv file
    rows = []
    for row in csv.reader(f):
        rows.append(row)

    # now let's generate the output that we specified in the comments above
    output_data = []

    # let's just run it on 10,000 rows first, instead of all 1.5 million rows
    # when you experiment with the `twitter_features` function to improve accuracy
    # feel free to get rid of the row limit and just run it on the whole set
    for row in rows[:10000]:
        # Remember that row[0] is the label, either 0 or 1
        # and row[1] is the tweet body

        # get the label
        label = row[0]

        # get the tweet body and compute the feature dictionary
        feature_dict = twitter_features(row[1])

        # add the tuple of feature_dict, label to output_data
        data = (feature_dict, label)
        output_data.append(data)

    # close the file
    f.close()
    return output_data


def get_training_and_validation_sets(feature_sets):
    """
    This takes the output of `get_feature_sets`, randomly shuffles it to ensure we're
    taking an unbiased sample, and then splits the set of features into
    a training set and a validation set.
    """
    # randomly shuffle the feature sets
    random.shuffle(feature_sets)

    # get the number of data points that we have
    count = len(feature_sets)
    # 20% of the set, also called "corpus", should be training, as a rule of thumb, but not gospel.

    # we'll slice this list 20% the way through
    slicing_point = int(.20 * count)

    # the training set will be the first segment
    training_set = feature_sets[:slicing_point]

    # the validation set will be the second segment
    validation_set = feature_sets[slicing_point:]
    return training_set, validation_set


def run_classification(training_set, validation_set):
    # train the NaiveBayesClassifier on the training_set
    classifier = nltk.NaiveBayesClassifier.train(training_set)
    # let's see how accurate it was
    accuracy = nltk.classify.accuracy(classifier, validation_set)
    print "The accuracy was.... {}".format(accuracy)


def predict(classifier, new_tweet):
    """
    Given a trained classifier and a fresh data point (a tweet),
    this will predict its label, either 0 or 1.
    """
    return classifier.classify(twitter_features(new_tweet))


# Now let's use the above functions to run our program
print "Let's use Naive Bayes!"
our_feature_sets = get_feature_sets()
print "Size of our data set: {}".format(len(our_feature_sets))
our_training_set, our_validation_set = get_training_and_validation_sets(our_feature_sets)
print "Now training the classifier and testing the accuracy..."
run_classification(our_training_set, our_validation_set)
```

## Accuracy Contest
- Separate in to groups of 2 or 3.
- Experiment with the feature set.
- With a training set of 20% of the shuffled data, test set of 80% of the shuffled data, compete to get the highest accuracy classifier.


# Homework
## Lab 2: SMS Spam Detection Classifier
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
