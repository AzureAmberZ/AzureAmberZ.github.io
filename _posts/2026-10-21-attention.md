---
layout: post
title: "Attention"
date: 2026-10-18 12:00:00 -0500
tags: [mlai, dl, nlp]
---

Hello, everyone.
Today, I will cover the idea used in the fundamental building blocks of modern
Large Language Models (LLMs) known as <span style="color:red">**Attention**</span>.

# Understanding Attention in General

One of the endgoals of LLMs is to create chatbots,
which is the idea that given some text, the model should be able to generate a coherent response to perform some task usually answering a question.

**But, how do we generate a response that is coherent?
or a response that is actually perform the task?**

So, before we can learn how to generate a response, we first need a way
to understand how words are related to each other.
But, learning how words or specifically language works is really complicated,
which depends on the language, culture, contextual understanding, etc, etc.
The field of Natural Language Processing (NLP) had and are still continuing
to research this topic.

But, one ground-breaking paper proposed in 2017 titled "Attention is All You Need"
provided a very intuitive way to think about words can relate to each other.
The idea is that words are dynamically related to other words based
on context and structure, but this can be measured by assign an attention score
between an input word and every other word.
In other words, given a word, how much should that word be paying "attention"
to the other words.
The formula for Attention is simply:

$$
Attn(Q,K,V)
= softmax(\frac{QK^T}{\sqrt{D}})V
$$

where:

- $Q \in \mathbb{R}^{m \times D}$ is the query matrix
- $K \in \mathbb{R}^{n \times D}$ is the key matrix
- $V \in \mathbb{R}^{n \times C}$ is the value matrix
- $D$ is the size of the queries and keys

So what is this formula actually computing?
Let simplify by first considering only a single output $q \in \mathbb{R}^D$
known as a <span style="color:blue">**query**</span>.
The query is compared to each input $k_1, ..., k_n \in \mathbb{R}^D$
known as <span style="color:orange">**keys**</span>
where $K = (k_1,...,k_n) \in \mathbb{R}^{n \times D}$
in order to choose between their corresponding values $v_1, ..., v_n \in \mathbb{R}^C$
known as <span style="color:pink">**values**</span>
where $V = (v_1,...,v_n) \in \mathbb{R}^{n \times C}$.
Specifically, this comparison is computed using a weighted average:

$$
Attn(q,K,V) = \sum_{i=1}^n \alpha_i(q,K) v_i
\hspace{0.5cm}
\alpha_i(q,K) \in [0,1] \text{ s.t. } \sum_{i=1}^n \alpha_i(q,K) = 1
$$

where $\alpha_i(q,K)$ are known as the **attention weights**.
In other words, query is compares to keys by placing more weight
or percentage of its "attention" on keys that it is more related to.
Note the weights $\alpha_i(q,K)$ are dynamic in the sense that
(1) the values vary depending on the given query $q$,
(2) the values vary based on the entire input $K$,
and (3) the weights changes based on which values $v_i$ it requires more
based on keys that is more related by indexing over $i$.

First, let's address the $\sum_{i=1}^n \alpha_i(q,K) = 1$ constraint.
A common way to make values sum up to $1$ is to apply a softmax function
similar to multi-class classification models:

$$
\alpha_i(q,K) = S_i([\alpha(q,k_1), ..., \alpha(q,k_n)])
= \frac{e^{\alpha(q,k_i)}}{\sum_{j=1}^n e^{\alpha(q,k_j)}}
$$

This way, $\sum_{i=1}^n \alpha_i(q,K) = 1$
while every $\alpha(q,k_i) \in \mathbb{R}$ is free to be ANY real number.
There are many ways $\alpha(q,K)$ can be computed, but the most popular
is **scaled dot-product attention**:

$$
\alpha(q,K) = \frac{q \cdot k}{\sqrt{D}}
$$

Recall the angle $\theta$ between two vectors $q$ and $k$
is $\cos(\theta) = \frac{q \cdot k}{|q| |k|}$.
Thus, scaled dot-product attention is measuring the similarity
between the query and key vectors by measuring how close the angle
between the vectors are.
$\sqrt{D}$ is included as a normalization factor behaving like $|q| |k|$;
The details of why it is specifically $\sqrt{D}$ is not important to be covered here.
So overall, the attention weight is computed as:

$$
\alpha_i(q,K)
= \frac{e^{q \cdot k_i}}{\sum_{j=1}^n e^{q \cdot k_j}}
= softmax(\frac{qK^T}{\sqrt{D}})V
$$

So essentially, attention is using the idea of dictionaries
such that given a query, we want to "match" the query to similar keys to
get the associated values from those similarily matched keys.
But, instead of "matching" to any key exactly like in dictionaries,
we only perform a soft "match" by comparing if the query and the keys are
similar by their angles.

For multiple queries $q_1, ..., q_m \in \mathbb{R}^D$
with $Q \in \mathbb{R}^{m \times D}$, then:

$$
Attn(Q,K,V)
= softmax(\frac{QK^T}{\sqrt{D}})V
$$

where the softmax is applied within each row of $\frac{QK^T}{\sqrt{D}}$.

# Applying Attention to Data

**Great! Now, how do we apply the idea of attention given input data $x_1, ..., x_n \in \mathbb{R}^d$ where $X = (x_1, ..., x_n) \in \mathbb{R}^{n \times d}$ to connect to output data $y_1, ..., y_m \in \mathbb{R}^c$ where $Y = (y_1, ..., y_m) \in \mathbb{R}^{m \times c}$?**

The idea is convert the input and output data into keys, values, and queries
using **embedding matrices**.
Let:

- $W^K \in \mathbb{R}^{d \times D}$ be embedding matrix to generate the keys
- $W^V \in \mathbb{R}^{d \times C}$ be embedding matrix to generate the values
- $W^Q \in \mathbb{R}^{c \times D}$ be embedding matrix to generate the queries

Then:

- Keys: $K = X W^K \in \mathbb{R}^{n \times d} \times \mathbb{R}^{d \times D} = \mathbb{R}^{n \times D}$
- Values: $V = X W^V \in \mathbb{R}^{n \times d} \times \mathbb{R}^{d \times C} = \mathbb{R}^{n \times C}$
- Queries: $Q = Y W^Q \in \mathbb{R}^{m \times c} \times \mathbb{R}^{c \times D} = \mathbb{R}^{m \times D}$

Then, the attention can be computed using such $K, V, Q$.
Note all the computations other than the softmax are just matrix multiplications
so attention is really easy and fast to compute.

# Summary

Modern LLMs utilize the idea of attention to help model learn how words
are related to each other in a dynamic way by extending upon the idea of dictionaries.
Specifically, the formula for attention is:

$$
Attn(Q,K,V)
= softmax(\frac{QK^T}{\sqrt{D}})V
$$

where:

- $Q \in \mathbb{R}^{m \times D}$ is the query matrix
- $K \in \mathbb{R}^{n \times D}$ is the key matrix
- $V \in \mathbb{R}^{n \times C}$ is the value matrix
- $D$ is the size of the queries and keys

Given input data $X = (x_1, ..., x_n) \in \mathbb{R}^{n \times d}$
and output data $Y = (y_1, ..., y_m) \in \mathbb{R}^{m \times c}$,
the idea of attention can be implemented using:

- Embedding key matrix $W^K \in \mathbb{R}^{d \times D}$ to generate $K = X W^K$
- Embedding value matrix $W^V \in \mathbb{R}^{d \times C}$ to generate $V = X W^V$
- Embedding query matrix $W^Q \in \mathbb{R}^{c \times D}$ to generate $Q = Y W^Q$

Below is a visualization of attention:

<img src="{{ '/images/attention.png' | relative_url }}" alt="Attention Visualization">

Note attention is a major part of LLMs, it is only a part of that LLMs use
in order to become coherent chatbots. I only covered a small part of attention here
that the field of NLP have utilized and improved upon.

References
- Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention is all you need. In I. Guyon, U. Von Luxburg, S. Bengio, H. Wallach, R. Fergus, S. Vishwanathan, & R. Garnett (Eds.), Advances in Neural Information Processing Systems (Vol. 30, pp. 5998–6008). Curran Associates, Inc. https://proceedings.neurips.cc/paper_files/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html




