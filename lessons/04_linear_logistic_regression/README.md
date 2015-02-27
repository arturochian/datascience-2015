# Objectives
Students will be able to
- Define and apply linear regression and logistic regression
- Show how and when to use these techniques
- Give practical and relevant examples from industry

# Linear Regression
## What is it?
- Given a set of data points, fine a line or curve that fits them the best.
- Useful for modeling the relationship between N input variables (*x*<sub>1</sub>, ..., *x*<sub>N</sub>) and *y*, some output, also called the target.
- Use it to make predictions

## Simple linear Regression
```
y = ax<sub>1</sub> + b
```

## Multivariable Regression
```
y = a<sub>1</sub>x<sub>1</sub> + ... + a<sub>n</sub>x<sub>n</sub> + b
```

## What are some examples?
- Predicting product revenues based on historical data (e.g. Disney)
- Predicting election outcomes
- Identifying stock market trends
- Recommending matches on dating sites (e.g. eHarmony)
- Determining credit score
- Analyzing the impact of price changes on units sold
- Assessing risk (e.g. health insurance companies modeling the relationship between customer age and insurance claims)

## How does it work?
- The algorithm tries to find the the line or curve that minimizes the square of the distances between the data and the line.
- This is called the *least squares* method. There are many different kinds but we'll focus on Ordinary Least Squares (OLS).

## Assumptions of the Model
- Our input variables are not riddled with measurement errors
- Input variables are not highly correlated
- How do we measure correlation?

## What are some things  to look out for?
## How do I know it's working
## Show me the code
## Useful parts of `statsmodel' library

# Logistic Regression
## What is it?
## What is it useful for?
## What are some examples?
## How do I use it?
### Code
### What are some pitfalls to look out for?
### How do I know it's working
## Logistic Regression vs Naive Bayes

# Homework
## Lab 1: Linear Regression
## Lab 2: Logistic Regression

# Reading
- K-nearest neighbors
- Usefulness of machine learning to industry

# References
- http://www.cpgtrends.com/2014/07/marketing-modeling-mix-and-linear-regression/
-
