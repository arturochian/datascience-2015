# Objectives
Students will be able to
- Define, explain and apply the gradient descent algorithm
- Explain how stochastic and gradient descent differ
- Define and explain regularization and how it plays a role in our models
- Compare and contrast the different techniques we've learned so far

# Prework
- [9-minute Review of Derivatives](https://www.khanacademy.org/math/differential-calculus/taking-derivatives/derivative_intro/v/calculus-derivatives-1) - I would suggest doing some practice questions or watching a few more of these videos. You should feel comfortable taking derivatives of polynomials.
- [5-minute Review of the Chain Rule](https://www.khanacademy.org/math/differential-calculus/taking-derivatives/chain_rule/v/chain-rule-with-triple-composition) - You should feel comfortable differentiating a composition of polynomials.
- [11-minute Review of Partial Derivatives](https://www.khanacademy.org/math/differential-calculus/taking-derivatives/chain_rule/v/chain-rule-with-triple-composition) - You should be able to take partial derivatives of a multivariate polynomial.

# Worksheets
- [Gradient Descent in One Variable](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Gradient+Descent/GD_worksheet_1.pdf)
- [Gradient Descent for Ordinary Least Squares, Two Variables](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/worksheets/Gradient+Descent/GD_Worksheet_2.pdf)

# What is gradient descent?
An algorithm to minimize functions, useful to use because we're always trying to minimize some cost function to fit our data accurately. It involves moving in the direction of steepest descent until we hit the minimum.

# What is stochastic gradient descent?
A more efficient way to find the minimum of a function by randomly sampling the training set and updating our parameters based on the gradient with respect to that single training data point as opposed to the entire set.

# What is regularization
A technique to prevent overfitting where we reduce the magnitude of the coefficients of our linear equation so that we get a simpler, smoother hypothesis.

# Homework
This was supposed to be assigned last class but we didn't get to it, so it's being assigned this class.

## Lab 1: More SVM for Text Classification - due on Mar 23
### Part 1: Try other models
Run logistic regression, kNN, and Naive Bayes on the Newsgroups categorization, using the same CountVectorizer and Tfidf.  Do they perform better or worse? Why do you think that is?

### Part 2: Use all categories
- Run the SVM on all categories of the Newsgroups data set. How does the accuracy do?
- What happens when we remove the l2 regularization? Switch it to l1 and see what happens.

## Lab 2: Back to the Twitter data
- Run the SVM on the [twitter data](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/datasets/clean_twitter_data.csv), just with the CountVectorizer and Tfidf. Feel free to add other features if you like.
- How does it perform?
