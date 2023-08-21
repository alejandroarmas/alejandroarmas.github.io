+++
title = "Random Variables and Distributions"
author = "Alejandro Armas"
tags = ["Probability", "Mathematics"] 
date = 2020-04-21
+++

I hope this article serves as a basic introduction to the terminology of probability theory!

## Random Variables

Considering that an **experiment** is a procedure that produces well defined outcomes, like taking a course and finishing with a certain grade letter, we see that a **random variable** is a function which maps random outcomes from experiments to numerical values  {{< katex "X : \Omega \to R " true />}} . The set of all possible numerical values attainable is called the **support** of the random variable.

For example we could allow people to shop at supermarkets and let our random variable Y = the number of infected shoppers with Covid-19 or X = the number of A's you finish your degree with at University. The set of all outcomes in an experiment is called the **sample space** usually denoted by  {{< katex "\Omega" true />}} .

Typicallly Random Variables are denoted by a capital letter and if they map to a finite or countably infinite range, then we say it is a *discrete* random variable. Now if you consider a RV with an uncountably infinite sample space it is said to be a *continuous* variable. An example of this would be mapping the heights of all humans on earth to a continuous random variable X. 

The computing of the probability that our *discrete* random variable X takes on some value x is called the Probability Mass Function (PMF) or  **distribution** of our random variable.

 {{< katex >}}   P(X = x) = f_{x}(x) {{< /katex >}} 

Going back to the height example, there is an infinite precision associated with every random variable X, as it can take on values of X = 5'8.24353556", X = 5'8.865347", etc. So we instead compute the probability that our random variable X takes on some interval value  {{< katex " x \in [a,b]" true />}}  in a Probability Density Function (PDF) to arrive at the **distribution** of our random variable.

 {{< katex >}}  P(X = x \in [a,b]) = P(a \leq X \leq b) = \int^{b}_{a}f_{x}(x)dx  {{< /katex >}} 

## Expectation and Variance

We are interested in various functions of random variables. In the long run of repeatedly conducting experiments, if your sample space is finite your outcome average will arrive at the **expected value**, the first of these functions, defined as:

 {{< katex >}}  E[x] = \mu  = \sum_{x \in X} x \cdot f_{x}(x) {{< /katex >}} 

This is also referred to as the mean, average, or center of mass when simply  {{< katex " E[x]" true />}} . Admittedly it looks odd to see an average in this context but the intuition being the equation is that the PMF is the weight for each value your random variable takes. Even though this equation calculates the theoretical mean of this discrete variable, sometimes it can take on decimal values. 


In general, expected value is a function who could take in another function as argument to produce a new function. The mean simply referred to when  {{< katex " g(x) = x" true />}} . Here we see a general form of expected value.

 {{< katex >}}  E[g(x)] = \sum_{x \in X} g(x) \cdot f_{x}(x) {{< /katex >}} 

Another function of random variables is called the variance. It is defined as:

 {{< katex >}}  E[(x - \mu)^2] = Var(x) = \sum_{x \in X} (x - \mu)^2 \cdot f_{x}(x)  {{< /katex >}} 

It describes how spread apart data is from eachother in the random variable distribution. Another way of showing the value of variance can be shown as follows:


 {{< katex >}}
 \begin{aligned}&\hspace{1em}  
    E[(x - \mu)^2] = Var(x)  \\&=
    \sum_{x \in X} (x - \mu)^2 \cdot f_{x}(x)  \\&= \sum_{x \in X} (x^2 - 2x\mu + \mu^2) \cdot f_{x}(x) \\&= \sum_{x \in X} x^2\cdot f_{x}(x) + \sum_{x \in X} -2x\mu \cdot f_{x}(x) + \sum_{x \in X} \mu^2 \cdot f_{x}(x) \\&= \sum_{x \in X} x^2\cdot f_{x}(x) -2\mu \cdot \sum_{x \in X} x \cdot f_{x}(x) + \mu^2 \cdot \sum_{x \in X} 1 \cdot f_{x}(x) \\&= E[x^2] - 2E[x]^2 + E[x]^2 \\&= E[x^2] - E[x]^2 \\&= E[x^2] - \mu^2  
 \end{aligned}
 {{< /katex >}} 

Thus  {{< katex >}}  Var(x) = E[x^2] - \mu^2 {{< /katex >}} 

## Special Types of Distributions


### Bernoulli Distribution

A discrete random variable X is said to follow a Bernoulli distribution if the sample space is binary. We see the PMF is as follows: 

{{< katex >}}  
f_{x}(x) = \begin{cases}
P & \text{if } x = 1,\\
1- P  & \text{if } x = 0\\
\end{cases} 
{{< /katex >}} 

In addition, we can derive expressions for the Expectation Value and Variance. Suppose  {{< katex "X \sim Bern(P)" true />}}  then:

 {{< katex >}}  E[x] = P  {{< /katex >}} 

 {{< katex >}}  Var(x) = P(1 - P)  {{< /katex >}} 

### Binomial Distribution

The result of **n** independent Bernoulli Trials is referred to as a Binomial Distribution. We find: 

 {{< katex >}}  f_{x}(k) = {n \choose k} \cdot P^k \cdot (1-P)^{n - k} {{< /katex >}} 

<p>
    <img src="/assets/images/distributions/bino.gif" alt="Binomial Distribution Figure"/>
    <br>
    <em>Photo Courtesy of 
    <a href="https://www.itl.nist.gov/div898/handbook/eda/section3/eda366i.html">[“Binomial Distribution”]</a>
    </em>
</p>


The intuition underlying this PMF is that we would like to know the probability of **k** occurances of a random variable occur in **n** trials. In the figure shown, there are 100 trials and we observe the likelyhood of k positive experiements, gets shifted to the right as p increases.


In addition, we can derive expressions for the Expectation Value and Variance. Suppose  {{< katex "X \sim Binom(n, P)" true />}}  then:

 {{< katex >}}  E[x] = n \cdot P \\ Var(x) = n \cdot P(1 - P)  {{< /katex >}} 

### Negative Binomial Distribution

Instead of being interested in knowing the probability of *k* occurances of a random variable occur in *n* trials, we instead focus on the probability that it takes **n** trials to achieve **k** occurances of a random variable. If you have n independent bernoulli trials with probability of succcess p and you are interested in the number of trials until success then we say  {{< katex "x \sim NB(k , p)" true />}} , who's probability mass function is:

 {{< katex >}} f_x(n) = P(X = n) = { n - 1 \choose k - 1} \cdot P^k \cdot (1-P)^{n - k} {{< /katex >}} 


Looking at the figure, we consider the likelihood we achieve 20 positive results n trials into an experiment with different probability values p. 


If we choose the occurances of the random variable to be  {{< katex "k = 1" true />}} , we can observe a special case of the Negative Binomial Distribution called the *Geometric Distribution*. Since  {{< katex "{ m \choose 0} = 1 " true />}}  we can reduce this equation to:

 {{< katex >}} f_x(n) = P(X = n) = P \cdot (1-P)^{n - 1} {{< /katex >}} 

We can think of this taking *n* trials in total to achieve a single success, or also z repeated failures if  {{< katex "z = n-1" true />}}  before a success. 

 {{< katex >}} E[x] = \frac{1}{P} {{< /katex >}} 

 {{< katex >}} Var(x) = \frac{1 - P}{P^2} {{< /katex >}} 

### Geometric Distribution

When we repeat an experiment with a binary sample space repeatedly obtaining the same outcome until a different outcome with probability  {{< katex "P" true />}}  occurs, we see that our random variable exhibits this special type of distributions.

We can quickly see it's PMF is:

 {{< katex >}}  f_{x}(k) = P(X = k) = (1 - P)^k \cdot P {{< /katex >}} 

Typically we use this when we would like to know the probability that *k* failures happen in an experiment before a success. It's unique expectation are variance values are as follows:

 {{< katex >}} E[x] = \frac{1 - P}{P} {{< /katex >}} 

 {{< katex >}} Var(x) = \frac{1 - P}{P^2} {{< /katex >}} 

### Uniform Distribution

If a random variable has an equal probability of occuring in a finite range [a,b] then it is said to follow a *Uniform Distribution*.  {{< katex "X \sim Unif(a,b)" true />}}  will be defined as habing a Probability Density Function:

{{< katex >}} 
    f_{x}(x) = \begin{cases}
    \frac{1}{b - a} & \text{if } a \leq x \leq b\\
    0  & \text{otherwise} \\
    \end{cases} 
{{< /katex >}} 


 {{< katex >}} E[x] = \frac{a + b}{2} {{< /katex >}} 

 {{< katex >}} Var(x) = \frac{(a - b)^2}{12} {{< /katex >}} 

<p>
    <img src="/assets/images/distributions/unifPDF.png" alt="Uniform Probability Density Function"/>
    <br>
    <em>Uniform Probability Density Function. Photo Courtesy of 
    <a href="https://probabilityformula.org/uniform-distribution.html">[“Probability Formula”]</a>
    </em>
</p>

<p>
    <img src="/assets/images/distributions/unifCDF.png" alt="Uniform Cumulative Density Function"/>
    <br>
    <em>Uniform Cumulative Density Function. Photo Courtesy of 
    <a href="https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)">[“Wikipedia”]</a>
    </em>
</p>

### Exponential Distribution

Used many times to model the failure of some event occuring as time passes. i.e. the next Covid Pandemic :0 

{{< katex >}} 
f_{x}(x) = \begin{cases}
\lambda e^{- \lambda x} & \text{if } x \geq 0\\
0  & \text{otherwise} \\
\end{cases} 
{{< /katex >}} 

<p>
    <img src="/assets/images/distributions/exponentialPDF.png" alt="Exponential Probability Density Function"/>
    <br>
    <em>Exponential Probability Density Function. Photo Courtesy of 
    <a href="https://en.wikipedia.org/wiki/Exponential_distribution">[“Wikipedia”]</a>
    </em>
</p>

<p>
    <img src="/assets/images/distributions/ExponentialCDF.png" alt="Exponential Cumulative Density Function"/>
    <br>
    <em>Exponential Cumulative Density Function. Photo Courtesy of 
    <a href="https://en.wikipedia.org/wiki/Exponential_distribution">[“Wikipedia”]</a>
    </em>
</p>

## Guassian (Normal) Distribution

Many physical phenomenon are modelled after this distribution. In fact, this distribution deserves it's own blogpost. For now, we say a continuous random variable  {{< katex "X \sim Norm( \mu, \sigma^2)" true />}}  if it satisifies this Probability Density Function:

 {{< katex >}} f_x(x) = \frac{1}{\sigma \sqrt{2\pi}} e^{\frac{-1}{2}\big( \frac{x - \mu}{\sigma} \big)^2} {{< /katex >}} 


 {{< katex >}} E[x] = \mu {{< /katex >}} 

 {{< katex >}} Var(x) = \sigma {{< /katex >}} 

<p>
    <img src="/assets/images/distributions/NormalPDF.png" alt="Gaussian Probability Density Function"/>
    <br>
    <em>Gaussian Probability Density Function. Photo Courtesy of 
    <a href="https://en.wikipedia.org/wiki/Normal_distribution">[“Wikipedia”]</a>
    </em>
</p>


<p>
    <img src="/assets/images/distributions/NormalCDF.png" alt="Gaussian Cumulative Density Function"/>
    <br>
    <em>Gaussian Cumulative Density Function. Photo Courtesy of 
    <a href="https://en.wikipedia.org/wiki/Normal_distribution">[“Wikipedia”]</a>
    </em>
</p>



## References

**Elementary Probability for Applications**, Rick Durret, 1st edition.
