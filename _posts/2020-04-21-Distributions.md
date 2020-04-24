---
layout: article
title: Random Variables and Distributions
tags: probability
aside:
    toc: true
  
---

I hope this article serves as a basic introduction to the terminology of probability theory!

## Random Variables

Considering that an **experiment** is a procedure that produces well defined outcomes, like taking a course and finishing with a certain grade letter, we see that a **random variable** is a function which maps random outcomes from experiments to numerical values $X : \Omega \to R $. For example we could allow people to shop at supermarkets and let our random variable X = the number of infected shoppers with Covid-19 or X = the number of A's you finish your degree with at University. The set of all outcomes in an experiment is called the **sample space** usually denoted by $\Omega$. Typicallly Random Variables are denoted by a capital letter and if they map to a finite or countably infinite range, then we say it is a *discrete* random variable.

The computing of the probability that our *discrete* random variable X takes on some value x is called the Probability Mass Function (PMF) or  **distribution** of our random variable.

$$ f_{x}(x) = P(X = x)$$
## Expectation and Variance

We are interested in various functions of random variables. In the long run of repeatedly conducting experiments, if your sample space is finite your outcome average will arrive at the **expected value**, the first of these functions, defined as:

$$ E[x] = \mu  = \sum_{x \in X} x \cdot f_{x}(x)$$

This is also referred to as the mean, average, or center of mass when simply $ E[x]$. Admittedly it looks odd to see an average in this context but the intuition being the equation is that the PMF is the weight for each value your random variable takes. Even though this equation calculates the theoretical mean of this discrete variable, sometimes it can take on decimal values. 


In general, expected value is a function who could take in another function as argument to produce a new function. The mean simply referred to when $ g(x) = x$. Here we see a general form of expected value.

$$ E[g(x)] = \sum_{x \in X} g(x) \cdot f_{x}(x)$$

Another function of random variables is called the variance. It is defined as:

$$ E[(x - \mu)^2] = Var(x) = \sum_{x \in X} (x - \mu)^2 \cdot f_{x}(x) $$

It describes how spread apart data is from eachother in the random variable distribution. Another way of showing the value of variance can be shown as follows:


$$ \sum_{x \in X} (x - \mu)^2 \cdot f_{x}(x)  \\ = \sum_{x \in X} (x^2 - 2x\mu + \mu^2) \cdot f_{x}(x) \\ = \sum_{x \in X} x^2\cdot f_{x}(x) + \sum_{x \in X} -2x\mu \cdot f_{x}(x) + \sum_{x \in X} \mu^2 \cdot f_{x}(x) \\ = \sum_{x \in X} x^2\cdot f_{x}(x) -2\mu \cdot \sum_{x \in X} x \cdot f_{x}(x) + \mu^2 \cdot \sum_{x \in X} 1 \cdot f_{x}(x) \\ = E[x^2] - 2E[x]^2 + E[x]^2 = E[x^2] - E[x]^2 = E[x^2] - \mu^2 $$

Thus $$ Var(x) = E[x^2] - \mu^2$$

## Special Types of Distributions

Now when we deal with 

### Bernoulli Distribution

A discrete random variable X is said to follow a Bernoulli distribution if the sample space is binary. We see the PMF is as follows: 

$$ f_{x}(x) = \begin{cases}
P & \text{if } x = 1,\\
1- P  & \text{if } x = 0\\
\end{cases}$$

In addition, we can derive expressions for the Expectation Value and Variance. Suppose $X \sim Bern(P)$ then:

$$ E[x] = P $$
$$ Var(x) = P(1 - P) $$

### Binomial Distribution

The result of **n** independent Bernoulli Trials is referred to as a Binomial Distribution. We find: 

$$ f{x}(x) = {n \choose k} \cdot P^k \cdot (1-P)^{n - k}$$

The intuition underlying this PMF is that we would like to know how many **k** occurances of a random variable occur in **n** trials.  


In addition, we can derive expressions for the Expectation Value and Variance. Suppose $X \sim Binom(n, P)$ then:

$$ E[x] = n \cdot P $$
$$ Var(x) = n \cdot P(1 - P) $$


### Geometric Distribution

When we repeat an experiment with a binary sample space over and over so long as the same random variable occurs, we see that our random variable exhibits this special type of distributions.

We can quickly see it's PMF is:

$$ f_{x}(x) = \sum_{x \in X} (1 - p)^k \cdot P$$

### Other things...

This article will continually get updated as the quarter continues... Stay tuned!
