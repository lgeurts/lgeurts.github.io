---
layout: post
title: Notes on Flux: The GitOps Kubernetes operator
read_time: true  
comments: false
category: Education & Training
tags: [ GitOps ]
---

These notes were briefly scrambled on a piece of paper while setting up Flux. Do not expect a full tutorial. Instead you will mostly see code snippets used during the process.

------------------------------------------------------------------------------

## **<u>Table of Contents</u>**

> 1. What is Flux?
> 2. Installing and Configuring Flux with GitHub
> * 2.1 Deploying Flux into a Cluster
> * 2.2 Verifying the Deployment and obtaining the RSA Key
> * 2.3 Implementing the RSA Key in GitHub
> * 2.4 Using fluxctl sync to synchronize the Cluster with a repository
> 3. 
> 9. In Practice

------------------------------------------------------------------------------

Flux is a tool that automatically ensures that the state of a cluster matches the config in git. It uses an operator in the cluster to trigger deployments inside Kubernetes, which means you don't need a separate CD tool. It monitors all relevant image repositories, detects new images, triggers deployments and updates the desired running configuration based on that (and a configurable policy).

The benefits are: you don't need to grant your CI access to the cluster, every change is atomic and transactional, git has your audit log. Each transaction either fails or succeeds cleanly. You're entirely code centric and don't need new infrastructure.

The raw notes are ***open sourced*** - should you encounter errors, have a better way of explaining something, don't hesitate to submit a pull request.
