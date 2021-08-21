---
layout: post
title:  "Making sense of optimization frameworks"
date:   2021-08-18 09:25:15 +0200
categories: optimization data-science
author: Paul Boes
---

# Making sense of optimization frameworks

In this post, I would like to develop a systematic approach towards the question which optimization framework is the right one to tackle a given problem. I want to do this by means of creating something like a decision tree. As it will turn out, there are a number of criteria that will include

- What is the dimension of the object over which we optimize?
- Can we efficiently evaluate membership in the feasibility region?
- Can we efficiently evaluate the value of the objective function?
- Do we know the objective function? Do we know it analytically?
- Do we maybe have partial knowledge?
- Do we need a solution quickly or is optimality more important?


## What do Facebook Ax and Nevergard and Botorch do exactly?

Botorch and Ax (which sits on top of Botorch) are focussed on Bayesian Optimization, while Nevergrad focusses on Black-box optimization.

### Bayesian Optimization

Following the presentations in [here](https://arxiv.org/abs/1807.02811) and [here](https://distill.pub/2020/bayesian-optimization/), Bayesian optimization uses Bayesian inference to solve the problem that is to find

$$\min_{x \in A} f(x), $$

in situations in which 
- $x \in \mathbb{R}^d$ with $d$ is not too large ($\sim20$). 
- membership in $A$  can be checked efficiently
- $f$ is continuous but otherwise unknown and very costly to evaluate, so that the aim is to use as few queries to $f$ as possible.
- queries to $f$ only return the function value and no additional information.

Applications for Bayesian optimization include hyper parameter serach, experiment design, system design more generally. See again [Fraziers great tutorial](https://arxiv.org/abs/1807.02811) for a list of applications.

The basic process looks as follows: 
1. You define a prior distribution, which is parametrized and assigns to every possible sequence of queries $x_1,x_2,\dots$ a probability of measuring a corresponding sequence of function values $f(x_1),f(x_2),\dots$. 
2. The parameters of the distribution are adapted to new samples, creating a new posterior distribution for every new sample.
3. Given a current posterior, the next sample is chosen according to a so-called acquisition function that attempts to choosen points that are likely to generate smaller function values than the current minimum value encountered so far. 

### Black-box optimization

 Following this [book chapter](https://link.springer.com/chapter/10.1007/978-3-030-66515-9_2), we define a black-box optimization problem as follows: There exist 

#### BBO Suites

- [Google Vizier](https://cloud.google.com/ai-platform/optimizer/docs/overview), See also their [paper](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/bcb15507f4b52991a0783013df4222240e942381.pdf)

- [Facebook Nevergrad](https://facebookresearch.github.io/nevergrad/)

  

