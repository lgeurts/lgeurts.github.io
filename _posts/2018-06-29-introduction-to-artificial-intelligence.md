---
layout: post
title: My Study Notes - Introduction to Artificial Intelligence (AI)
read_time: true  
comments: true
category: Education & Training
tags: [ Artificial Intelligence ]
---

![AI](/assets/artificial-intelligence.jpg)

**What is Machine Learning?**

Machine learning provides the foundation for artificial intelligence. We train our software model using data e.g. the model learns from the training cases and then we use the trained model to make predictions for new data cases.

Let's start with a data set that contains historical records aka ***observations***. Every record includes numerical features (X) quantifying characteristics of the item we are working with. 

There are also values we try to predict (Y). We will use training cases to train the machine learning model so that it calculates a value for (Y), from the features in (X). Simply said, we're creating a ***function*** that operates on a set of features, (X), to produce predictions, (Y).

There are two common kinds of machine learning, ***supervised*** and ***unsupervised***. 

In a ***supervised*** learning scenario, we start with  observations that include known values for the variable we want to predict. We call these ***labels***.

Because we are starting with data that includes the label we are trying to predict, we can train the model using only some data and hold the rest for evaluating our models performance. 

First step, using an algorithm to train a model that fits the features to the known label. 

As we started with a known label value, we can validate the model by comparing the value predicted by the function to the actual label value that we knew. Then, when we're happy that the model works, we can use it with new observations for which the label is unknown, and generate new predicted values.

In a ***unsupervised*** learning scenario, we don't have any known label values in our training data set. 

We train the model by finding similarities between observations. Once we trained the model, every new observation is added to a group (cluster) of observations with similar characteristics.



