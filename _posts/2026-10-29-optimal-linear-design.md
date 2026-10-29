---
layout: post
title: "Introduction to Optimal Design"
date: 2026-10-29 12:00:00 -0500
tags: [statistics, design]
---

Hello, everyone.
Today, I will introduce the idea of optimal design specifically for linear models.

# What is Optimal Design?

As its name implies, optimal design is a class of experimental designs
that optimizes some statistical criterion, usually minimizing the variance
of the model's parameters in some way.

There are several topics that are covered in the field of optimal design.
Some popular topics include:

- Optimal Design for Nonlinear Models
- Algorithm-based Optimal Designs
- Optimal Subdata Selection

Note in general that optimal design makes a huge assumption:
It assumes that the proposed model to fit the data is true
in order to perform optimization.
Thus, each model proposed to fit a data generally have different optimal designs.
Despite this limitation, optimal design is still popular since
if the model appears to fit the data well, we still like to know how
the data should be collected in order to make the model as accurate as possible.

# Optimal Design for Linear Models

A linear model has the form $y_i = x_i^T \theta + \epsilon_i$
where $\epsilon_i$ is usually assumed to be
independent Gaussian error $\epsilon_i \sim N(0,\sigma^2)$
and $x_i,\theta \in \mathbb{R}^p$.
For multiple observations $x_1,...,x_n$ with responses $y_1,...,y_n$,
define $X = (x_1,...,x_n) \in \mathbb{R}^{n \times p}$
and $Y = (y_1,...,y_n) \in \mathbb{R}^n$.
Thus in matrix form, the linear model $Y = X\theta + \epsilon$
where $\epsilon \sim N(0,\sigma^2 I_n)$.

Given $X$, a common way to estimate $\theta$ is to
minimize the least squares criterion $|Y - X\theta|^2$
or to maximize the likelihood
$(2\pi\sigma^2)^{-\frac{n}{2}} \exp(-\frac{1}{2\sigma^2} |Y-X\theta|^2)$,
which are equivalent for linear models.
This has been well-studied and its estimator, which is unbiased,
is widely known in the field of statistics
(assuming $X$ is linearly independent):

$$
\hat{\theta} = (X^TX)^{-1} X^T Y
$$

This means the variance of the estimator is:

$$\begin{align*}
    Var(\hat{\theta})
    &= (X^TX)^{-1} X^T Var(Y) X (X^TX)^{-1} \\
    &= (X^TX)^{-1} X^T \sigma^2 I_n X (X^TX)^{-1} \\
    &= \sigma^2 (X^TX)^{-1}
\end{align*}$$

Since $\sigma^2$ is constant, then the objective is to minimize
$(X^TX)^{-1}$ is some way.
Note $X^T X$ is called the **Information Matrix**


An **exact design of size $n$** as defined $(x_i,n_i)$
is a collection of $k$ distinct points $x_1,...,x_k$
where $n_i$ is the number of times $x_i$ appears with $N = \sum_{i=1}^k n_i$.
Then, the Information Matrix is defined as:

$$
I(\theta) = \sum_{i=1}^k \frac{n_i}{n} x_i x_i^T \in \mathbb{R}^{p \times p}
$$

Note $I(\theta)$ is the inverse of $Var(\hat{\theta})$.
However since $n_i$ are natural numbers,
optimizing $I(\theta)$ is often difficult since the problem
is essentially a discrete optimization problem finding the exact natural numbers
for $n_i$ for each $x_i$.


To make this easier, it is often converted into a continuous optimization problem
by letting $\frac{n_i}{n} \in \mathbb{R}$.
For small sample size $n$, this may not be equivalent to the discrete version,
but for large sample size $n$, the continuous version is often
very similar to the discrete version.
In other words, consider the **approximate design**
$(w_i,n_i)$ where $x_i$ are distinct
and $\sum_{i=1}^k w_i = 1$ with $w_i \geq 0$.
The information matrix becomes:

$$
I(\theta) = \sum_{i=1}^k w_i x_i x_i^T \in \mathbb{R}^{p \times p}
$$

Thus, the goal is to find the weights $w_i$ associated with data $x_i$
that optimizes $I(\theta)$ in some way.
In other words, which how much (i.e. $w_i$) of each data (i.e. $x_i$)
should be collected in order to minimize the variance of the model's parameters.

# Summary

Optimal design is a class of experimental design that usually minimizes
the variance of the model's parameter by deciding which data should be collected.

For linear models $Y = X\theta + \epsilon$ and approximate design
$(w_i,n_i)$ where $x_i$ are distinct
and $\sum_{i=1}^k w_i = 1$ with $w_i \geq 0$,
we aim to optimize
the information matrix $I(\theta) = \sum_{i=1}^k w_i x_i x_i^T$ in some way.
Some common statistical criterion are:

- A-Optimality: Minimize the sum of the parameters' variances,
which is $Tr(Var(\hat{\theta})) \propto Tr(I^{-1}(\theta))$.
- D-Optimality: Maximize the confidence ellipsoid of the parameters,
which is $\log(|Var(\hat{\theta})|) \propto -\log(|I(\theta)|)$

In this post, I introduced the idea of optimal design using linear models
and some common statistical criterions to optimize.
However, this idea has been extended to more complex topics
like nonlinear models, algorithmic optimality, and subdata selection.


