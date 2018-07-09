---
layout: post
title: Study Notes - Artificial Intelligence (AI)
read_time: true  
comments: false
category: Education & Training
tags: [ Artificial Intelligence ]
---

These are my ***personal notes***, broadly covering the BASICS necessary for ***machine learning*** and ***artificial intelligence***.

Some final caveats:
* This post may not be helpful for your purposes. 
* This is still very much a work in progress and it will be changing a lot.
* Some content may be out of order, missing. Don't get upset.
* These notes are generated in markdown, so they unfortunately lack snazzy interactivity.
* Part of this material is adapted, sometimes directly copied, from elsewhere. I have tried to give credit where due. 

The raw notes are ***open sourced*** - should you encounter errors, have a better way of explaining something, don't hesitate to submit a pull request.

------------------------------------------------------------------------------

## **<u>Table of Contents</u>**

> 1. What is Machine Learning?
> 2. Techniques: regression & classification

------------------------------------------------------------------------------

### **1. What is Machine Learning?**

Machine learning provides the foundation for artificial intelligence. We train our software model using data e.g. the model learns from the training cases and then we use the trained model to make predictions for new data cases.

Let's start with a data set that contains historical records aka ***observations***. Every record includes numerical ***features*** (X) quantifying characteristics of the item we are working with. 

There are also values we try to predict (Y). We will use training cases to train the machine learning model so that it calculates a value for (Y), from the features in (X). Simply said, we are creating a ***function*** that operates on a ***set*** of features, (X), to produce predictions, (Y).

At heart, a function is the mapping from a set in a ***domain*** to a set in a ***codomain***.

![Function](/assets/artificial-intelligence/function.png)

*Ref: [Mathworld Wolfram](http://mathworld.wolfram.com/) - Eric W. Weisstein.*

**There are five types of machine learning:**

* ***Supervised learning*** - the algorithm is given a pre-labeled training example to learn from.
* ***Unsupervised learning*** - the algorithm is given unlabeled examples.
* ***Semi-supervised learning*** - the algorithm uses a mix of labeled & unlabeled data.
* ***Active learning*** - similar to semi-supervised learning, but the algorithm can "ask" for extra labeled data based on what it needs to improve on.
* ***Reinforcement learning*** - actions are taken and rewarded or penalized, goal is maximizing lifetime/long-term reward (or vice versa).

*Ref: Book: Neural Computing: Theory and Practice (1989) - Philip D. Wasserman.*

**Note:** Following course guidelines, we'll discuss the two most common methods; ***supervised*** and ***unsupervised***.

**Learning scenarios:**

In a ***supervised*** learning scenario, we start with  observations that include known values for the variable we want to predict. We call these ***labels***.

Because we are starting with data that includes the label we are trying to predict, we can train the model using only some data and hold the rest for evaluating our models performance. 

We'll then use a algorithm to train a model that fits features to the known label. 

As we started with a known label value, we can validate the model by comparing the value predicted by the function to the actual label value that we knew. Then, when we're happy that the model works, we can use it with new observations for which the label is unknown, and generate new predicted values.

In a ***unsupervised*** learning scenario, we don't have any known label values in our training data set. 

We'll train the model by finding similarities between observations. Once we have trained this model, more observations are added to a ***cluster*** of observations with alike characteristics. (Cluster = Group)

### **2. Techniques**

#### **Regression**

When we need to predict a numeric value, for example an amount of calories, we use a supervised learning technique called ***regression***. 

Let's take one male. We want to model calories burned while exercising. 

First we get some pre-liminary data (age: 34, gender: 1, weight: 60, height: 165), then put him on a fitness monitor and capture additional information. Now what we do is model the calories burned using features from his exercise like his heart rate: 134, temperature: 37, and duration: 25. 

In this case we know all features and have a known label value of 231 calories. So we need our algorithm to learn a function, that operates of all the males exercise features to give us a net result of 231.

> * `F([34, 1, 60, 165, 134, 37, 25]) = 231`

A sample of one person isn't likely to give a function that generalizes well. So we gather the same data from a large number participants, and then train the model using the bigger set of data. 

> * `F([X1, X2, X3, X4, X5, X6, X7]) = Y`

Now having a new function that can be used to calculate label (Y), we can finally plot the values of (Y), calculated for specific features of (X) values on a chart:

:-----------------:|:-----------------:
<img src="/assets/artificial-intelligence/plotted-chart-1.png" align="left" width="285" height="160" alt=""> | <img src="/assets/artificial-intelligence/plotted-chart-2.png" align="right" width="285" height="160" alt="">

And we can interpolate any new values of (X) to predict an unknown (Y).

As we started with data that includes the label we try to predict, we can train the model using some data and keep the rest for evaluating the models performance. Then we can use the model to predict (F) of (X) for evaluation data, and compare the predictions or scored labels to the actual labels that we know to be true.

:-----------------:|:-----------------:
<img src="/assets/artificial-intelligence/plotted-chart-3.png" align="left" width="285" height="160" alt=""> | <img src="/assets/artificial-intelligence/plotted-chart-4.png" align="right" width="285" height="160" alt="">

The difference between the predicted and actual levels are called the ***residuals***. And they can tell us something about the error level in the model. 

We can measure the error in the model using ***root-mean-square error*** or (***RMSE***) and ***mean absolute error*** (***MAE***).

:-----------------:|:-----------------:
<img src="/assets/artificial-intelligence/plotted-chart-5.png" align="left" width="285" height="160" alt=""> | <img src="/assets/artificial-intelligence/plotted-chart-6.png" align="right" width="285" height="160" alt="">

Both are absolute measures of error in the model. For example, having an RMSE value of 5 would mean that the standard deviation of error from our test error is 5 calories. An error of 5 calories seems to indicate a reasonably good model, but let's suppose we are predicting how long an exercise session takes. An error of 5 hours would be a very bad model.

You might want to evaluate the model using relative metrics to indicate a more general level of error as a relative value between 0 and 1. ***Relative absolute error*** (***RAE***) and ***relative squared error*** (***RSE***) produce metrics where the closer to 0 the error, the better the model.

***Coefficient of determination*** (***CoDR***) or ***R squared***, is another relative metric, but this time a value closer to 1 indicates a good fit for the model.

:-----------------:|:-----------------:
<img src="/assets/artificial-intelligence/plotted-chart-7.png" align="left" width="285" height="160" alt=""> | <img src="/assets/artificial-intelligence/plotted-chart-8.png" align="right" width="285" height="160" alt="">
 
#### **Classification**

Another kind of supervised learning is called ***classification***.

Classification is a technique that we can use to predict which class, or category, something belongs to. Its simplest variant is the binary classification where we predict whether entities belong to one of two classes (true or false).

Example, we take a number of patients in a health clinic, gather some personal details (age: 23, pregnancy: 1, glucose: 171, BMI: 43.5), run tests, and identify which patients are diabetic and which are not.

We can learn a function that can be applied to the patient features and give the result 1 for patients that are diabetic:

> * `F([23, 1, 171, 43.5]) = 1`

and 0 for patients that aren't.

Generally, a binary classifier is a function that

