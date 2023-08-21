+++
title = "What is the Difference Between Covariance and Correlation?" 
author = "Alejandro Armas"
tags = ["Probability", "Mathematics"]
date = 2023-05-05
+++


Working with data will almost always begin with a data exploration phase. We listen to its heartbeat and ask lots of questions. As we begin this phase, one might ask themselves 'what are the tools we can leverage?'. What do we do to define a linear measure of a relationship between two random variables? In other words, how do we measure the amount of 'increasing X increases Y'-ness, or '- decreasing Y'-ness and vice versa in a joint probability distribution? How do we bake that into an equation?

### Covariance

Recall that data is sampled from distributions. Different random variables might or might not be related.

Covariance is a statistical measure that:
1. indicates the extent to which two or more variables are related. 
2. determining the strength of the relationship between variables.

In probability and statistics one such formula is defined as the following:

**Definition**: Covariance

 {{< katex >}} \begin{aligned}&\hspace{1em} cov(X, Y) := \mathbb{E}[(X - \mathbb{E}(X))(Y - \mathbb{E}(Y))] \\&= \mathbb{E}[XY - \mathbb{E}(X)Y - \mathbb{E}(Y)X + \mathbb{E}(X)\mathbb{E}(Y)] \\&= \mathbb{E}(XY) - \mathbb{E}(\mathbb{E}(X)Y) - \mathbb{E}[\mathbb{E}(Y)X] + \mathbb{E}[\mathbb{E}(X)\mathbb{E}(Y)] \\&= \mathbb{E}(XY) - \mathbb{E}(X)\mathbb{E}(Y) - \underbrace{\mathbb{E}(Y)\mathbb{E}(X)}_{\text{Linearaity of expectations}} + \mathbb{E}(X)\mathbb{E}(Y) \\&= \mathbb{E}(XY) - \mathbb{E}(X)\mathbb{E}(Y) \end{aligned} {{< /katex >}} 

If  {{< katex "X, Y" true />}}  **are independent, then their covariance is zero**. In fact, this statistic is designed precisely to have this properly. It is very useful. See the [Appendix section](#appendix) for a proof of why this is.

##### What is this equation tracking?

The equation is tracking the average product between two **signed distances**. Furthermore, each distance is measuring how far a random variable lies from its mean. 

Let me repeat that again, we are understanding: on average, how far the product between two variables are measured from their averages. 

The values can take anything from negative infinity to positive infinity under the following cases:
- The case when both  {{< katex "\mathbb{E}[(X - \mathbb{E}(X))] > 0 \text{ and } \mathbb{E}[(Y - \mathbb{E}(Y))] > 0" true />}}  or  {{< katex "\mathbb{E}[(X - \mathbb{E}(X))] < 0 \text{ and } \mathbb{E}[(Y - \mathbb{E}(Y))] < 0" true />}}  then there is a positive correlation and covariance.
- The case when both  {{< katex "\mathbb{E}[(X - \mathbb{E}(X))] < 0 \text{ and } \mathbb{E}[(Y - \mathbb{E}(Y))] > 0" true />}}  or  {{< katex "\mathbb{E}[(X - \mathbb{E}(X))] > 0 \text{ and } \mathbb{E}[(Y - \mathbb{E}(Y))] < 0" true />}}  then there is a negative correlation. 

### Correlation

In programming, we are working with data sampled from distributions. So, we denote  {{< katex "\bar{x}" true />}}  as an estimator of the mean  {{< katex "\mu" true />}}  of our random variables. Lets formulate our definition of covariance differently:  

{{< katex >}} 
\begin{aligned}&\hspace{1em} Cov(X, Y) := \mathbb{E}[(X - \mu_x) (Y - \mu_y)] \\&= \frac{\sum^n_{i = 0}(x_i - \bar{x}) (y_i - \bar{y})}{n} \\&= \frac{\sum^n_{i = 0}x_iy_i - \bar{x}\sum^n_{i = 0}y_i - \bar{y}\sum^n_{i = 0}x_i + n\bar{x}\bar{y}}{n}  \\&= \frac{\sum^n_{i = 0}x_iy_i - \bar{x}\sum^n_{i = 0}y_i }{n} \\&= \frac{n\sum^n_{i = 0}x_iy_i - (\sum^n_{i = 0}x_i)(\sum^n_{i = 0}y_i)}{n^2} \end{aligned} 
{{< /katex >}} 

##### Normalizing Covariance

By normalizing covariance, we have a unitless statistic, that ranges between  {{< katex "-1" true />}}  and  {{< katex "1" true />}} . Lets do that: 

{{< katex >}} 
\begin{aligned}&\hspace{1em} Corr(x, y) 
= \frac{Cov(x, y)}{\sqrt{Var(x)Var(y)}} 
\\&= \frac{Cov(x, y)}{\sqrt{\left[\frac{\sum_{i = 1}^{n}x_i^2}{n} - \bar{x}^2 \right]\left[\frac{\sum_{i = 1}^{n}y_i^2}{n} - \bar{y}^2 \right]}} 
\\&=  
\frac{n\sum^n_{i = 0}x_iy_i - (\sum^n_{i = 0}x_i)(\sum^n_{i = 0}y_i)}{n^2\sqrt{\left[\frac{\sum_{i = 1}^{n}x_i^2}{n} - \bar{x}^2 \right]\left[\frac{\sum_{i = 1}^{n}y_i^2}{n} - \bar{y}^2 \right]}}
\\&=  
\frac{n\sum^n_{i = 0}x_iy_i - (\sum^n_{i = 0}x_i)(\sum^n_{i = 0}y_i)}{\sqrt{\left[\frac{n^2\sum_{i = 1}^{n}x_i^2}{n} - n^2\bar{x}^2 \right]\left[\frac{n^2\sum_{i = 1}^{n}y_i^2}{n} - n^2\bar{y}^2 \right]}}
\\&=  
\frac{n\sum^n_{i = 0}x_iy_i - (\sum^n_{i = 0}x_i)(\sum^n_{i = 0}y_i)}{\sqrt{\left[n\sum_{i = 1}^{n}x_i^2 - (\sum_{i = 1}^{n}x_i)^2 \right]\left[n\sum_{i = 1}^{n}y_i^2 - (\sum_{i = 1}^{n}y_i)^2 \right]}}
\end{aligned} 
{{< /katex >}} 


### Algorithm for Correlation in Python

The coefficient for correlation is sometimes referred to as the Pearson correlation coefficient. In the previous formulation, we rearranged a lot of terms, in order to work with more efficient numpy operations.

```python
import numpy as np

def pearson_corr_coef(x, y):
	n = len(x)
	assert n == len(y)
	numerator = n * np.sum(x * y) - np.sum(x) * np.sum(y)
	denominator = np.sqrt((n * np.sum(x ** 2) - np.sum(x) ** 2) * (n * np.sum(y ** 2) - np.sum(y) ** 2))
	return numerator / denominator
```



# appendix

Suppose we are working with two independent random variables from a joint distribution, then the following holds true. This derivation shows that the average of two random variables, nested in a function, is equivalent to the product of the average of two random variables, nested in a function.

**Claim**:

If  {{< katex "X, Y" true />}}  are independent, then  {{< katex "h, t: \mathbb{R} \to \mathbb{R}" true />}}  

 {{< katex >}} \mathbb{E}(t(x)h(y)) = \mathbb{E}(h(x))\mathbb{E}(t(y)) {{< /katex >}} 

**Proof**:

{{< katex >}} 
\begin{equation*} 
\begin{split} \mathbb{E}(t(x)h(y)) 
&= \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} t(x)h(y)f_{X,Y}(x,y)dxdy 
\\&= \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} t(x)h(y)\underbrace{f_X(x)f_Y(y)}_{\text{Def of Independence}}dxdy 
\\&= \int_{-\infty}^{\infty} t(x)f_X(x)dx \int_{-\infty}^{\infty} h(y)f_Y(y)dy \\&= \mathbb{E}(t(x)) \mathbb{E}(h(y))

\end{split} 
\end{equation*}
{{< /katex >}}