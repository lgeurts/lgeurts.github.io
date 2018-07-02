---
layout: post
title: Study Notes - Artificial Intelligence (AI)
read_time: true  
comments: false
category: Education & Training
tags: [ Artificial Intelligence ]
---

These are ***personal notes***, broadly intended to cover basics for ***machine learning***, and ***artificial intelligence***.
They are intended to provide intuitive understandings of concepts that I encounter while wading my way through course materials and a host of online articles. 

If you are looking for a more comprehensive study, rest assured. There are many other resources out there which will help with that.

![Robot](/assets/artificial-intelligence.jpg)

Some final caveats:
* This post may not be helpful for your purposes. 
* This is still very much a work in progress and it will be changing a lot.
* Some content may be out of order, missing. Don't get upset.
* These notes are generated for markdown, so they unfortunately lack snazzy interactivity.
* Part of this material is adapted, sometimes directly copied, from elsewhere. I have tried to give credit where due. 

The raw notes are ***open sourced*** - should you encounter errors, have a better way of explaining something, don't hesistate to submit a pull request.

------------------------------------------------------------------------------

## **<u>Table of Contents</u>**

> 1. What is Machine Learning?
> 2. Techniques

------------------------------------------------------------------------------

### **1. What is Machine Learning?**

Machine learning provides the foundation for artificial intelligence. We train our software model using data e.g. the model learns from the training cases and then we use the trained model to make predictions for new data cases.

Let's start with a data set that contains historical records aka ***observations***. Every record includes numerical ***features*** (X) quantifying characteristics of the item we are working with. 

There are also values we try to predict (Y). We will use training cases to train the machine learning model so that it calculates a value for (Y), from the features in (X). Simply said, we're creating a ***function*** that operates on a set of features, (X), to produce predictions, (Y).

**There are five types of machine learning:**

* ***Supervised learning*** - the algorithm is given a pre-labeled training example to learn from.
* ***Unsupervised learning*** - the algorithm is given unlabeled examples.
* ***Semi-supervised learning*** - the algorithm uses a mix of labeled & unlabeled data.
* ***Active learning*** - similar to semi-supervised learning, but the algorithm can "ask" for extra labeled data based on what it needs to improve on.
* ***Reinforcement learning*** - actions are taken and rewarded or penalized, goal is maximizing lifetime/long-term reward (or vice versa).

*Ref: Neural Computing: Theory and Practice (1989) - Philip D. Wasserman.*

**Note:** Following course guidelines, we'll discuss the two most common methods; ***supervised*** and ***unsupervised***.

**Learning scenarios:**

In a ***supervised*** learning scenario, we start with  observations that include known values for the variable we want to predict. We call these ***labels***.

Because we are starting with data that includes the label we are trying to predict, we can train the model using only some data and hold the rest for evaluating our models performance. 

We'll then use a algorithm to train a model that fits features to the known label. 

As we started with a known label value, we can validate the model by comparing the value predicted by the function to the actual label value that we knew. Then, when we're happy that the model works, we can use it with new observations for which the label is unknown, and generate new predicted values.

In a ***unsupervised*** learning scenario, we don't have any known label values in our training data set. 

We'll train the model by finding similarities between observations. Once we have trained this model, more observations are added to a ***cluster*** of observations with akin characteristics. (Cluster = Group)

### **2. Techniques**

When we need to predict a numeric value, for example an amount of calories, we use a supervised learning technique called ***regression***. 

Let's take one male. We want to model calories burned while exercising. First we get some pre-liminary data, then put him on a fitness monitor and capture more data using features like age, weight, heart rate, and duration. 

In this case we know all features and have a known label value of 231 calories. So we need our algorithm to learn a function that operates of all exercise features to give us a net result of 231.

A sample of one person isn't likely to give a function that generalizes well. So we gather the same data from a large number participants, and then train the model using the bigger set of data. When done, and now having a new function that can be used to calculate our label (Y), we can finally plot the values of (Y), calculated for specific features of (X) values.

