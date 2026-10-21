---
layout: post
title: "Introduction to Neural Networks"
date: 2026-10-20 12:00:00 -0500
tags: [mlai, dl]
---

Today, I will provide an introduction to **neural networks**.

# Prerequisite: Linear Regression and Decision Trees

Neural networks may seem complicated, but essentially they combine
and extend upon the idea of linear regression and decision trees.

**First, what is linear regression?**
Linear regression is a statistical model mapping
an input $x \in \mathcal{X} \subset \mathbb{R}^p$
to an output $y \in \mathcal{Y} \subset \mathbb{R}$
using a line:

$$
y = \beta_0 + \beta^T x
$$

where $\beta \in \mathbb{R}^p$ is the parameter coefficients
for input $x$ while $\beta_0 \in \mathbb{R}$ is the bias.
However, most data $(x,y)$ do not follow a linear trend
(i.e. the model between $x$ and $y$ is not a line)
so a common modification is to perform some nonlinear transformation.

$$
y = \beta_0 + \beta^T \phi(x; V)
$$

where
$\phi(\cdot ; V): \mathcal{X}
\rightarrow \tilde{\mathcal{X}} \subset \mathbb{R}^{\tilde{p}}$
is some transformation possibly nonlinear with parameters $V$
and now $\beta \in \mathbb{R}^{\tilde{p}}$.

For example, if $x = (x_1,x_2)$, perhaps the data follow
a trigonometric trend say $y = 1 + 2\cos(5x_1) - 4\cos(3x_2) + \sin(x_1x_2)$,
then define $\phi(x; V) = \cos(V_1x_1) - \cos(V_2x_2) + \sin(V_3x_1x_2)$
where $V = (V_1,V_2,V_3) = (5,3,1)$ is given.
Then, $y = \beta_0 + \beta^T \phi(x;V)$ where the goal is to
accurately estimate $\beta_0 = 1$ and $\beta = (2,-4,1)$.

**Second, what is a decision tree?**
Decision trees is a statistical model mapping
an input $x \in \mathcal{X} \subset \mathbb{R}^p$
to an output $y \in \mathcal{Y} \subset \mathbb{R}$,
but instead of using a line, it uses partitions.
The idea is to split the input space $\mathcal{X}$
into different partitions so that each partition is associated with some
output value $y$.

For a simple example, suppose $x \in \mathbb{R}^2$
and $y = 1$ if $x$ is in the 1st quadrant, $2$ if in the 2nd quadrant, etc
and any points on the axis have $y = 0$.
Then, the goal of the decision tree is to find partitions
around the $x_1$-axis: $x_1 < 0$ and $x_1 = 0$ and $x_1 > 0$
and partitions around the $x_2$-axis: $x_2 < 0$ and $x_2 = 0$ and $x_2 > 0$.

- If $x_1 = 0$ or $x_2 = 0$, then $y = 0$.
- If $x_1 > 0$ and $x_2 > 0$, then $y = 1$.
- If $x_1 < 0$ and $x_2 > 0$, then $y = 2$.
- If $x_1 < 0$ and $x_2 < 0$, then $y = 3$.
- If $x_1 > 0$ and $x_2 < 0$, then $y = 4$.

Note the idea is simply to determine a sequence of or/and statements
to partition the input data $x$ in order to map to the output $y$.

The process of how linear regression estimates it parameters and
how decision trees determine its partitions will not be covered here
as it is unimportant for neural networks.



# Neural Networks

**So, how do neural networks extend upon both linear regression
and decision trees?**

First, consider linear regression.
Often, real-world data do not just follow a simple nonlinear model
like our trigonometric example.
In order to create more complex models, neural networks extend upon
linear models by stacking multiple nonlinear regression models,
which are referred to as layers.
The equation for the $\ell$-th layer:

$$
z_{\ell} = b_{\ell} + W_{\ell} f_{\ell-1}(x;\theta_{\ell-1})
\hspace{1cm}
f_{\ell}(x;\theta_{\ell}) = \phi_{\ell}(z_{\ell}; V_{\ell})
$$

where $f_{0}(x;\theta_0) = x$ is the original input data
and $\theta_{\ell} = (b_{\ell},W_{\ell})$ is the $\ell$-th layer parameters
and $\ell = \{0,1,2,...,L\}$ are the layer numbers.

**So, what is happening in this equation?**

First, consider the first layer $\ell = 1$.
Then, $z_1 = b_1 + W_1 f_0(x;\theta_0) = b_1 + W_1 x$
so $z_1$ is a linear regression on $x$
so $f_1(x;\theta_1) = \phi_1(z_1; V_1)$
is some nonlinear transformation $\phi_1(\cdot; V_1)$ on $z_1$.
Essentially, we are passing an input $x$ into the first layer
to be mapped to some new nonlinear input $f_1(x;\theta_1)$.

Then for $\ell = 2$, we pass $f_1(x;\theta_1)$
into $z_2 = b_2 + W_2 f_1(x;\theta_1)$
which is passed into $f_2(x;\theta_2) = \phi_2(z_2; V_2)$.
Then, we do the same for $\ell = 3$, then $\ell = 4$, etc until $\ell = L$.
So essentially, we are applying nonlinear transformations on
the original input data $x$ iteratively until we get a really complex model.

**But, even if the neural network is complex, how do we ensure the neural network approximates the true model well?**

This is where the idea of decision tree comes in!
We saw in the simple example that if the model finds the correct partitions,
decision trees can essentially determine the output $y$ precisely.
But, it is often that decision trees cannot find these partitions easily
since the partitions may not be separated easily using lines as in the example.

But as we noted earlier, the neural network transforms the original input data
into nonlinear features.
So if the paritions are not easily found in the
original input space $\mathcal{X}$ since the partitions may not be separated
by lines, then perform the partitions on the nonlinear feature space instead!
Obviously, these partitions may not exist on just one nonlinear feature space,
so instead of partitioning at any single layer, we partition at every layer to
refine the partitions from one nonlinear feature space to the next.

**So, we can use the idea of partitioning on the nonlinear feature space to approximate the true model more and more precisely. But, how do neural networks do this specifically?**

As in decision trees, we implement the concept of using a sequence of
and/or statements.
Note and/or statements are simply logic gates checking if either both, one,
or none of the conditions are true.
So, we choose some type of nonlinear transformation
$\phi_{\ell}(\cdot;V_{\ell})$ that acts like some logic gate.
Luckily, there is a one that is well-studied:
the Heavyside function $\phi_{\ell}(z_{\ell};V_{\ell}) = 1_{z_{\ell \geq 0}}$
so $\phi_{\ell}(z_{\ell};V_{\ell}) = 1$ if $z_{\ell} \geq 0$
and $\phi_{\ell}(z_{\ell};V_{\ell}) = 0$ if $z_{\ell} < 0$,
which acts like a logic gate!
These types of neural networks are called **Multilayer Perceptrons (MLPs)**.

However like deep decisions trees, if the number of layers is large,
the neural network acts like a decision tree just more complicated.
So, MLPs tends to overfit when training on input data
since if input data are different enough from each other
and with a large enough amount of logic gates,
we can create a large amount of small partitions that each
include at most one input data so essentially the model is just memorizing
the data it is trained on rather than finding any generalizable pattern.
Due to this reason and some other more technical reasons, using the heavyside
function is often not used especially in modern neural networks.
Instead, we use functions that approximates heavyside.
Below are a few of the more commonly used
(the $V_{\ell}$ is omitted in $\phi$ since usually not used):

- Sigmoid: $\phi_{\ell}(z_{\ell}) = \frac{1}{1 + e^{-z_{\ell}}}$
- Tanh: $\phi_{\ell}(z_{\ell}) = \tanh(z_{\ell})$
- ReLU: $\phi_{\ell}(z_{\ell}) = \max(0,z_{\ell})$

In most cases, most neural networks just default to ReLU.



# Summary

Neural networks are models combining and extending upon the
ideas of linear regression and decision trees by stacking multiple
linear regressions until to create nonlinear features, which are used to
create partitions similar to decision trees,
but instead in nonlinear feature spaces.
The equation for the $\ell$-th layer:

$$
z_{\ell} = b_{\ell} + W_{\ell} f_{\ell-1}(x;\theta_{\ell-1})
\hspace{1cm}
f_{\ell}(x;\theta_{\ell}) = \phi_{\ell}(z_{\ell}; V_{\ell})
$$

where $f_{0}(x;\theta_0) = x$ is the original input data
and $\theta_{\ell} = (b_{\ell},W_{\ell})$ is the $\ell$-th layer parameters
and $\ell = \{0,1,2,...,L\}$ are the layer numbers.

- $b_{\ell}$ is bias parameter for the $\ell$-th layer
- $W_{\ell}$ are the weight parameters for the $\ell$-th layer
- The dimension of the $\ell$-th layer denoted $D_{\ell}$ is the number of hidden units
- $f_{\ell}(x;\theta_{\ell})$ is usually referred to as neurons
- $\phi_{\ell}(\cdot;V_{\ell})$ are called the activation functions, which are usually ReLU

<img src="{{ '/images/neural_network.png' | relative_url }}" alt="Neural Network Visualization">

Note in this post, I only explained why neural networks
have the equation they do.
I did not include how neural networks are optimized to estimate
the parameter values or any commonly used techniques associated
with neural networks.
In fact, these types of neural networks are some of the most basic
with other, more complex types being dedicated for more interesting tasks
like computer vision and natural language processing.

