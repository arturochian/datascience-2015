# Objectives
Students will be able to
- Define and apply the k-Nearest Neighbors classifier
- Give practical and relevant examples from industry

# Worksheets

# k-Nearest Neighbors (kNN) Classifier
## What is it?
- Given a set of data points,
- Useful for
- Use it

## What are some applications?
- [Financial distress predictions](http://www.academia.edu/4607757/Application_of_K-Nearest_Neighbor_KNN_Approach_for_Predicting_Economic_Events_Theoretical_Background)
- [Breast cancer diagnosis](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2243774/)
- Handwriting detection and other computer vision
- Customer segmentation

## How does it work?
- The algorithm tries to find the

## Assumptions of the Model

## What are some things to look out for?
- Curse of dimensionality
- More than 10 dimensions and we need to do dimensionality reduction

## How do I know it's working
- Use cross-validation

## Set Up for Our Code
1. download [this csv]()
2. move that dataset under your /repos/datasets/ directory on your local machine (NOT VAGRANT)
3. log into vagrant from the /vm/ directory as usual
5. run `sudo ipython notebook --profile=dst`
6. paste the following code into iPython notebook and run it

```python
Some code here...
```

## Advanced techniques for Building Good Models
- Dimensionality reduction
- Weighting

# Homework
## Lab 1: kNN vs Logistic
[Here]() is a dataset with the following columns:
- column 1: ...

### Part 1
- Apply k-Nearest Neighbors on subsets of the columns and using cross validation see how the accuracy changes.
- Now use all of the columns for your kNN classifier and see what the accuracy is.

### Part 2
- Use logistic regression on the data, perhaps bucketing some of the column data into discrete categories rather than being continuous values.
- Try logistic regression on subsets of the columns.

## Part 3
- Between logistic regression and kNN, which performed better in predicting which customers would sign on for a term deposit?

# Reading
- [Support Vector Machines]()
