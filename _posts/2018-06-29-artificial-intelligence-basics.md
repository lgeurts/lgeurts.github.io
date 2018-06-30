---
layout: post
title: Study Notes - Artificial Intelligence Basics
read_time: true  
comments: false
category: Education & Training
tags: [ Artificial Intelligence ]
---

![AI](/assets/artificial-intelligence.jpg)

**What is Machine Learning?**

Machine learning provides the foundation for artificial intelligence. We train our software model using data e.g. the model learns from the training cases and then we use the trained model to make predictions for new data cases.

Let's start with a data set that contains historical records aka ***observations***. Every record includes numerical ***features*** (X) quantifying characteristics of the item we are working with. 

There are also values we try to predict (Y). We will use training cases to train the machine learning model so that it calculates a value for (Y), from the features in (X). Simply said, we're creating a ***function*** that operates on a set of features, (X), to produce predictions, (Y).

There are two kinds of machine learning, supervised and unsupervised. 

In a ***supervised*** learning scenario, we start with  observations that include known values for the variable we want to predict. We call these ***labels***.

Because we are starting with data that includes the label we are trying to predict, we can train the model using only some data and hold the rest for evaluating our models performance. 

We'll then use an algorithm to train a model that fits the features to the known label. 

As we started with a known label value, we can validate the model by comparing the value predicted by the function to the actual label value that we knew. Then, when we're happy that the model works, we can use it with new observations for which the label is unknown, and generate new predicted values.

In a ***unsupervised*** learning scenario, we don't have any known label values in our training data set. 

We'll train the model by finding similarities between observations. Once we have trained this model, new observations are added to a ***cluster*** of observations with akin characteristics.

**Techniques**

When we need to predict a numeric value, for example an amount of calories, we use a supervised learning technique called ***regression***. 

Let's take one male. We want to model calories burned while exercising. First we get some pre-liminary data, then put him on a fitness monitor and capture more data using features like age, weight, heart rate, and duration. 

In this case we know all features and have a known label value of 231 calories. So we need our algorithm to learn a function that operates of all exercise features to give us a net result of 231.


