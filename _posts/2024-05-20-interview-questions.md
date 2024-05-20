---
layout: post
title: Interview questions
date: 2024-05-15 20:00:00
description: Introduction to NLP
tags: interview
categories: sample-posts
toc:
  sidebar: left
---

# Most popular questions

## Bias/variance tradeoff

The conflict in trying to simultaneously minimize these two sources of error that prevent supervised learning algorithms from generalizing beyond their training set.

The bias error is an error from erroneous assumptions in the learning algorithm. High bias can cause an algorithm to miss the relevant relations between features and target outputs (underfitting).
The variance is an error from sensitivity to small fluctuations in the training set. High variance may result from an algorithm modeling the random noise in the training data (overfitting).

## Train/validation set

Train set consists of a substantial portion of your data that the model sees and learns from.

Validation set is a separate subset of your data used to assess the model's performance on unseen data during the development phase. We don't train the model on the validation set directly. 
The model hasn't been "memorizing" the validation data  during training, so it provides a more objective measure of how well the model generalizes to new data.  By evaluating the model's performance on the validation set with different hyperparameter configurations, we can identify the settings that lead to the best performance.

The split between training and validation sets is typically around 80/20, but it can vary depending on the dataset size. You NEVER use test set as validation set.

## Linear/logistic regression

Linear is used for regression, as it predicts continous variables.  It models the relationship between a dependent variable (what you want to predict) and one or more independent variables (features) using a linear equation.

Logistic regression tackles binary classification problems. It takes in features and predicts the probability of an instance belonging to one of two classes. Uses the sigmoid function to map the linear equation's output to a probability between 0 and 1. Logistic regression squishes the linear regression output into a sigmoid curve, making it suitable for probability prediction between two classes.

Softmax regression is the multi-class version of logistic regression. It's used for classification problems with more than two categories.  Softmax regression uses the softmax function, which generalizes the sigmoid function to output a probability distribution over multiple classes, ensuring all probabilities sum to 1.

All these regessions are solved using gradient descent. Model is randomly initialized, error is calculated (MSE, log loss, cross-entropy loss).

Log loss for 2 labels: $L(y, p) = -(y\log p + (1-y)\log(1-p))$.

And multiple: $-\sum y \log p$

Optimization techniques as Adam or momentum

## PCA/LDA

These are dimentionality reduction techniques, meaning they reduce the number of features in your data while trying to preserve the most important information.

PCA is an unsupervised learning technique. It doesn't require class labels (like cat or dog) in your data.
Focuses on Variance: PCA identifies the directions of greatest variance in the data and projects the data onto these directions. These directions are called principal components (PCs).

LDA, in contrast, is a supervised learning technique. It leverages class labels to find the directions that best discriminate between different classes.
Focuses on Class Separation: LDA finds a lower-dimensional projection that maximizes the separation between classes, while still preserving the overall variance of the data.
Think of it as: Imagine the same cloud of data points but colored by class. LDA finds a projection that best separates these colored clusters.

## Clustering
K-Means (partitioning data into pre-defined k clusters), Hierarchical clustering (building a hierarchy of clusters)

K-Means starts by randomly selecting k data points as initial centroids (cluster centers). Each data point is assigned to the closest centroid based on a distance metric.  The centroids are recomputed as the mean of the data points assigned to each cluster.

Hierarchical clustering uses linkage methods to determine how similar clusters are for merging (agglomerative) or splitting (divisive). Common linkage methods include single linkage (based on the minimum distance between any two points), complete linkage (based on the maximum distance), and average linkage (based on the average distance between all points in two clusters).

## Gausian mixture model
A Gaussian mixture is a function that is composed of several Gaussians, each identified by $k$. So what about using a soft clustering instead of a hard one? 

## Decision trees vs neural net

Decision trees are highly interpretable. You can easily understand the logic behind each prediction by following the tree structure and decision rules. This is a major advantage for debugging and gaining insights into the model's reasoning.
Robustness: Decision trees are less prone to overfitting compared to neural networks, especially with techniques like pruning.  
Decision trees can become complex and cumbersome for data with very high dimensionality.
Feature Importance: While interpretable, decision trees don't inherently provide feature importances, which can be challenging for understanding which features contribute most to the model's performance.

## Metrics

Accuracy: The most basic metric, representing the proportion of correct predictions (True Positives + True Negatives) divided by the total number of predictions.

Precision: Measures the proportion of true positives among predicted positives (True Positives / (True Positives + False Positives)). It reflects how well the model avoids false positives.

Recall: Measures the proportion of true positives identified by the model (True Positives / (True Positives + False Negatives)). It reflects how well the model avoids false negatives.

F1-Score: A harmonic mean of precision and recall, combining both aspects into a single metric. F1 is particularly useful when dealing with imbalanced class distributions.

AUC-ROC (Area Under the ROC Curve):  ROC (Receiver Operating Characteristic) curve depicts the trade-off between true positive rate (recall) and false positive rate (1-specificity) for different classification thresholds. AUC-ROC measures the area under this curve, providing a model performance measure independent of classification thresholds.

Mean Squared Error (MSE):  Measures the average squared difference between predicted and actual values. Lower MSE indicates better model fit.

Root Mean Squared Error (RMSE):  Square root of MSE, expressed in the same units as the target variable. Easier to interpret the magnitude of error compared to MSE.

Mean Absolute Error (MAE):  Measures the average absolute difference between predicted and actual values. Less sensitive to outliers compared to MSE.

R-squared (R²): Represents the proportion of variance in the dependent variable explained by the independent variables in the model. Ranges from 0 (no explanatory power) to 1 (perfect fit).

