---
layout: post
title: Notes on Flux: The GitOps Kubernetes operator
read_time: true  
comments: false
category: Education & Training
tags: [ GitOps ]
---

------------------------------------------------------------------------------

## **<u>Table of Contents</u>**

> 1. What is Machine Learning?
> * 1.1 Functions
> * 1.2 Algorithms - Grouped by Learning Style
> * 1.3 Supervised v. Unsupervised
> 2. Techniques
> * 2.1 Regression
> * 2.2 Classification
> 9. In Practice

------------------------------------------------------------------------------

Flux is a tool that automatically ensures that the state of a cluster matches the config in git. It uses an operator in the cluster to trigger deployments inside Kubernetes, which means you don't need a separate CD tool. It monitors all relevant image repositories, detects new images, triggers deployments and updates the desired running configuration based on that (and a configurable policy).

The benefits are: you don't need to grant your CI access to the cluster, every change is atomic and transactional, git has your audit log. Each transaction either fails or succeeds cleanly. You're entirely code centric and don't need new infrastructure.

The raw notes are ***open sourced*** - should you encounter errors, have a better way of explaining something, don't hesitate to submit a pull request.
