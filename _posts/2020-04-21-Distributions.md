---
layout: article
title: Random Variables and Distributions
tags: probability Mathematics
aside:
    toc: true
  
---

I hope this article serves as a basic introduction to the terminology of probability theory!

## Random Variables

Considering that an **experiment** is a procedure that produces well defined outcomes, like taking a course and finishing with a certain grade letter, we see that a **random variable** is a function which maps random outcomes from experiments to numerical values $X : \Omega \to R $. 

For example we could allow people to shop at supermarkets and let our random variable X = the number of infected shoppers with Covid-19 or X = the number of A's you finish your degree with at University. The set of all outcomes in an experiment is called the **sample space** usually denoted by $\Omega$. 

Typicallly Random Variables are denoted by a capital letter and if they map to a finite or countably infinite range, then we say it is a *discrete* random variable. Now if you consider a RV with an uncountably infinite sample space it is said to be a *continuous* variable. An example of this would be mapping the heights of all humans on earth to a continuous random variable X. 

The computing of the probability that our *discrete* random variable X takes on some value x is called the Probability Mass Function (PMF) or  **distribution** of our random variable.

$$  P(X = x) = f_{x}(x)$$

Going back to the height example, there is an infinite precision associated with every random variable X, as it can take on values of X = 5'8.24353556", X = 5'8.865347", etc. So we instead compute the probability that our random variable X takes on some interval value $ x \in [a,b]$ in a Probability Density Function (PDF) to arrive at the **distribution** of our random variable.

$$ P(X = x \in [a,b]) = P(a \leq X \leq b) = \int^{b}_{a}f_{x}(x)dx $$

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

$$ f_{x}(k) = {n \choose k} \cdot P^k \cdot (1-P)^{n - k}$$

The intuition underlying this PMF is that we would like to know the probability of **k** occurances of a random variable occur in **n** trials.  


In addition, we can derive expressions for the Expectation Value and Variance. Suppose $X \sim Binom(n, P)$ then:

$$ E[x] = n \cdot P \\ Var(x) = n \cdot P(1 - P) $$

### Negative Binomial Distribution

Instead of being interested in knowing the probability of *k* occurances of a random variable occur in *n* trials, we instead focus on the probability that it takes **n** trials to achieve **k** occurances of a random variable. If you have n independent bernoulli trials with probability of succcess p and you are interested in the number of trials until success then we say $x \sim NB(k , p)$, who's probability mass function is:

$$f_x(n) = P(X = n) = { n - 1 \choose k - 1} \cdot P^k \cdot (1-P)^{n - k}$$

If we choose the occurances of the random variable to be $k = 1$, we can observe a special case of the Negative Binomial Distribution called the *Geometric Distribution*. Since ${ m \choose 0} = 1 $ we can reduce this equation to:

$$f_x(n) = P(X = n) = P \cdot (1-P)^{n - 1}$$

We can think of this taking *n* trials in total to achieve a single success, or also z repeated failures if $z = n-1$ before a success. 

$$E[x] = \frac{1}{P}$$

$$Var(x) = \frac{1 - P}{P^2}$$

### Geometric Distribution

When we repeat an experiment with a binary sample space repeatedly obtaining the same outcome until a different outcome with probability $P$ occurs, we see that our random variable exhibits this special type of distributions.

We can quickly see it's PMF is:

$$ f_{x}(k) = P(X = k) = (1 - P)^k \cdot P$$

Typically we use this when we would like to know the probability that *k* failures happen in an experiment before a success. It's unique expectation are variance values are as follows:

$$E[x] = \frac{1 - P}{P}$$

$$Var(x) = \frac{1 - P}{P^2}$$

### Uniform Distribution

If a random variable has an equal probability of occuring in a finite range [a,b] then it is said to follow a *Uniform Distribution*. $X \sim Unif(a,b)$ will be defined as habing a Probability Density Function:

$$f_{x}(x) = \begin{cases}
\frac{1}{b - a} & \text{if } a \leq x \leq b\\
0  & \text{otherwise} \\
\end{cases}$$


$$E[x] = \frac{a + b}{2}$$

$$Var(x) = \frac{(a - b)^2}{12}$$

## Guassian (Normal) Distribution

Many physical phenomenon are modelled after this distribution. In fact, this distribution deserves it's own blogpost. For now, we say a continuous random variable $X \sim Norm( \mu, \sigma^2)$ if it satisifies this Probability Density Function:

$$f_x(x) = \frac{1}{\sigma \sqrt{2\pi}} e^{\frac{-1}{2}\big( \frac{x - \mu}{\sigma} \big)^2}$$


$$E[x] = \mu$$

$$Var(x) = \sigma$$

## Other things...

This article will continually get updated as the quarter continues... Stay tuned!


## References

**Elementary Probability for Applications**, Rick Durret, 1st edition.
