# Objectives
Students will be able to:
- recap and close-out supervised learning
- explain and use k-means clustering
- explain and use hierarchical clustering

# Pre-Work

# Unsupervised Learning
The objective of unsupervised learning is to **identify patterns in the data**.

Examples:
- Clustering
- Density Estimation
- Dimensionality Reduction

### Action: Students, brainstorm example applications of unsupervised learning.

# K-means Clustering
Simplest approach to clustering:
- We are given some data D, consisting of x<sup>(i)</sup>, each of which is a p-dimensional vector.
- Our task is to group the data into K groups. We specify K beforehand.

## An Application
Suppose we have census data and want to do *market segmentation* - subgroup the people from the census in such a way that we can better target advertisements.

## Intuition
Here's the intuition behind K-means clustering:
- There are certain points which are the centers of the clusters
- The points in that cluster are nearer to the center of that cluster than they are to the center of a different cluster.

## Procedure
### Action: Draw the K-means clustering procedure step-by-step on the board.
Assume K clusters, with *unknown* centers c<sub>1</sub>, ..., c<sub>k</sub>, each of which is a p-dimensional vector.

A good measure of how good a cluster is is the sum of squared distances of the points to the center of that cluster. Then we'll sum that over all the clusters to see how good our choice of centers were.

We want to minimize the sum over all the clusters of the sum of square distances of points to the center of the cluster they belong to.

It's difficult to minimize this analytically, so we'll need an algorithm to help us do this.

### Action: Explain the math behind the procedure on the board.
K-means do this iteratively by the following:

1. Initialize the centers c<sub>1</sub>, ..., c<sub>k</sub> to be arbitrary, distinct points from the dataset.
2. Choose the optimal assignment of points to clusters given by the centers above. Call this assignment of points to centers A. We do this by assigning each point to the center nearest to it.
3. Now that the assignment is fixed, choose the optimal centers for that assignment A.
4. Repeat 2 and 3 until convergence, a.k.a. the assignments don't change on subsequent iterations.

Side Note: This alternating minimization in steps 2 and 3 is a special case of the Expectation Maximization (EM) algorithm.

# Hierarchical Clustering
Unlike K-means, we do not specify how many clusters we want. In the end, we have a tree-like representation of the data.

There are different kind sof hierarchical clustering, but we will focus on the most common kind: *bottom up* (a.k.a. agglomerative) hierarchical clustering.

We build a hierarchy in a "bottom-up" fashion.

## Procedure
1. Start with each point in its own cluster
2. Identify the two closest clusters and merge them.
3. Repeat step 2 until all points are in a single cluster.

### Action: Show video illustration from dataschool.io.

Once we've constructed the tree of clusters from the bottom-up, we can cut it off at a certain height to get the number of clusters we desire. The lower we cut the tree, the more clusters we get.

## How to determine closeness of two clusters
### Action: Draw the different types of linkage on the board.

Given two clusters A and B, we want to compute the dissimilarity between them, called *linkage*. There a couple of ways we can do this:

- Complete: compare all pairwise dissimilarities between points in A and B and take the maximum of these dissimilaritys to be the linkage.
- Single: Same as complete, except we take the minimum of these dissimilarities to be the linkage.
- Average: We take the avergae of the pairwise dissimilarities..
- Centroid: Dissimilarity between the centroid of cluster A and the centroid of cluster B.

Note that above, we will often use Euclidean distance as the measure of dissimilarity. An alternative is correlation-based distance, which is a measure of how correlated the features of two separate observations are.

## Example applications
### Hierarchical Clustering on Breast Cancer Data

### K-Means Clustering on Crime Data

# Practical Advice for Clustering
- Scaling of the data matters

For hierarchical clustering,
- How we measure dissimilarity measure matters
- What type of linkage we choose matters

For either K-means or hierarchical, How many clusters to choose? See Elements of Statistical Learning Chapter 13 for more details.
- No agreed upon answer
- Not well-solved
- Usually decide qualitatitvely

# Exercises (to be submitted as Homework)

# Resources
- [Document clustering with Scikit learn](http://scikit-learn.org/dev/auto_examples/text/document_clustering.html)
- [How Cloudera Scaled K-Means](http://blog.cloudera.com/blog/2013/03/cloudera_ml_data_science_tools/)
- [Clustering US Senators with K-Means](http://blog.dataquest.io/blog/plotting-senators/)
- [Tutorial on K-means](https://datasciencelab.wordpress.com/2013/12/12/clustering-with-k-means-in-python/)
- [Lecture Videos on Clustering](http://www.dataschool.io/15-hours-of-expert-machine-learning-videos/)
