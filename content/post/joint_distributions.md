+++
title = "Unlocking the Power of Joint Distributions - How to Analyze Multiple Random Variables" 
author = "Alejandro Armas"
tags = ["Probability", "Mathematics"]
date = 2023-04-26
+++



The concept of joint distribution is useful when studying the outcomes and effects of multiple random variables in statistics. Joint distribution allows generalizing probability theory to the multivariate case. Let me paint a story for you.

## Joint Distributions

Today, the weather is nice. Its a fresh summer morning. You're out at a restaurant having breakfast with your in-laws and you want to impress. You're such a nice person, you think to yourself. You offer to pay the tip. You are aware that your wallet contains 3 twenty-dollar bills, 2 fifty-dollar bills, and 5 ten-dollar bills, but it hurts your heart too much to look. You decide on selecting 3 bills, but want to leave it up to the divine spirits of life to dictate which ones exactly.

This is where probability comes into the picture. We are going to formalize this scenario. We could choose to model this problem with a random variable tracking how much money we tip, but we want to be a bit more *fine grained*. We want to track **how many fifty-dollar bills and ten-dollar bills we give up**. Those hold sentimental value, for some reason. So, we use two random variables in our analysis.

This problem is ripe for a joint probability distribution.  

Like we said, we have 2 fifty-dollar, 5 ten-dollar, and 3 twenty-dollar bills. Now we select 3 bills at random and let  {{< katex "X" true />}}  be the number of fifty-dollar and  {{< katex "Y" true />}}  the number of ten-dollar bills that are selected. 

**Definition:**
Joint Discrete Random Variables  
Let  {{< katex "X, Y" true />}}  be discrete random variables. Then their joint probability mass function is  {{< katex "p(x, y) := P(X = x, Y = y)" true />}} . 

We start by determining the joint probability mass function of  {{< katex "(x, y)" true />}} . 


 {{< katex >}} \begin{equation*} \begin{aligned} P(X = x, Y = y) &= \frac{\\{2 \choose x}{5 \choose y}{3 \choose 3 - x - y}}{10 \choose 3} \\ &= \frac{\frac{2}{(2 - x)!x!}\frac{5!}{(5 - y)!y!}\frac{3!}{(x + y)!(3 - x - y)!}}{\frac{10!}{3!7!}} \\ &= \frac{2 \times 5!3!3!7!}{(2 - x)!(5 - y)!(3 - x - y)!x!y!(x + y)!10!} \end{aligned} \end{equation*} {{< /katex >}} 

Sweet! Now we have a function that models our problem! Lets iterate through all the possible values of  {{< katex "X, Y" true />}} . Here they are:

|            |  {{< katex "Y = 0" true />}}                      |  {{< katex "Y = 1" true />}}                      |  {{< katex "Y = 2" true />}}                      |  {{< katex "Y = 3" true />}}                   | 
| ---------- | --------------------------- | --------------------------- | --------------------------- | ------------------------ |
|  {{< katex "X = 0" true />}}     |  {{< katex "\frac{1}{120}" true />}}              |  {{< katex "\frac{15}{120}" true />}}             |  {{< katex "\frac{30}{120}" true />}}             |  {{< katex "\frac{10}{120}" true />}}          | 
|  {{< katex "X = 1" true />}}     |  {{< katex "\frac{6}{120}" true />}}              |  {{< katex "\frac{30}{120}" true />}}             |  {{< katex "\frac{20}{120}" true />}}             |  {{< katex "0" true />}}                       | 
|  {{< katex "X = 2" true />}}     |  {{< katex "\frac{3}{120}" true />}}              |  {{< katex "\frac{5}{120}" true />}}              |  {{< katex "0" true />}}                          |  {{< katex "0" true />}}                       | 

25% chance that you give up a single fifty and ten-dollar bill, respectively. Huh, maybe we should have just been deliberate about choosing the bills...

As we are reaching into our wallet, time slows down to a pause. We think to ourselves, 'Wow, we are doing this huh. Oh no, not the fifty...'. Quickly, our mind thinks of marginal probabilities. Sweat is starting to form. We want to compute the probability of giving up  {{< katex "X" true />}}  fifty-dollar bills. 

**Definition:**
Discrete Random Variables Marginal Density

The marginal probability mass functions of  {{< katex "X, Y" true />}}  are obtained by:

 {{< katex >}} P(X = x) = \sum_y P(X = x, Y = y) = \sum_y p(x , y) {{< /katex >}} 

 {{< katex >}} P(Y = y) = \sum_x P(X = x, Y = y) = \sum_x p(x , y) {{< /katex >}} 


Using the definition of Marginal Density, we can evaluate this probability.

 {{< katex >}} \begin{aligned} P(X = x) &= \sum_{y} \frac{\\{2 \choose x} {5 \choose y} {3 \choose 3 - x - y}}{10 \choose 3} \end{aligned} {{< /katex >}} 

Surely we can handle losing two fifty-dollar bills. We're generous! That's totally possible. In fact, I hope we do. You feel better with yourself. You compute the probability as follows:

 {{< katex >}} \begin{aligned} P(X = 2) &= P(X = 2, Y = 0) + P(X = 2, Y = 1)  \\&= \frac{\\{2 \choose 2}{5 \choose 0}{3 \choose 1}}{10 \choose 3} + \frac{\\{2 \choose 2}{5 \choose 1}{3 \choose 0}}{10 \choose 3} \\&= \frac{3}{120} + \frac{5}{120} \\&= \frac{8}{120} \end{aligned} {{< /katex >}} 

Wait, that's kinda unlikely. If only we were given a chance to be nice, we would. Dang!  

##### Some other cool (and related) calculations

Lets relate the probability of having selected more fifty-dollar bills than ten-dollar bills. So, 

 {{< katex "P(X \geq Y)" true />}} :

 {{< katex >}} \begin{aligned} P(X \geq Y) &= P(X = 0, Y = 0)  + P(X = 1, Y = 1) + P(X = 2, Y = 1) \\& \hspace{7em} + P(X = 1, Y = 0) + P(X = 2, Y = 0) \\&= \frac{1}{120} + \frac{30}{120} + \frac{5}{120} + \frac{6}{120} + \frac{3}{120} \\&= \frac{45}{120} \end{aligned} {{< /katex >}} 

Lastly, what about providing two fifty-dollar bills, provided the condition that we selected more fifty-dollar bills than ten-dollar bills. 

 {{< katex "P(X = 2 \| X \geq Y) " true />}} :

 {{< katex >}} \begin{aligned} P(X = 2 | X \geq Y) &= \frac{P(X = 2, X \geq Y)}{P(X \geq Y)} \\&= \frac{P(Y = 0, Y = 1, X = 2)}{P(X \geq Y)} \\&= \frac{\frac{8}{120}}{\frac{45}{120}} \\&= \frac{8}{45} \end{aligned} {{< /katex >}} 

## Independence of Random Variables

In some cases, the probability distribution of one random variable will not be affected by the distribution of another random variable defined on the same sample space. We refer to those distributions as being independent of eachother.

**Definition:** Discrete and Independent Random Variables 

Random variables  {{< katex "X \subset A, Y\subset B" true />}}  are independent if for all intervals  {{< katex "A, B \subset \mathbb{R}" true />}}  

 {{< katex >}} P(X \in A, Y \in B) = P(X \in A)P(Y \in B) \ \forall A, B \subset \mathbb{R} {{< /katex >}} 

If  {{< katex "X, Y" true />}}  are discrete, then we say that they are independent if:

 {{< katex >}} P(X = x, Y = y) = P(X = x)P(Y = y) \ \forall x \in X, y \in Y {{< /katex >}} 

So in the motivating example earlier, can we say that  {{< katex "X, Y" true />}}  are independent?

Nope. In case you don't believe me, consider the following: 

 {{< katex >}} \begin{aligned} \underbrace{P(X = 2, Y = 2)}_{\text{Evaluates to Zero}} \neq P(X = 2)\underbrace{P(Y = 2)}_{\text{This is not zero}} = \frac{8}{120} \times \frac{50}{120} \end{aligned} {{< /katex >}} 

## Continuous Jointly Distributed Random Variables

This same analysis can be carried over into situations of continuity. 

**Definition:** Jointly Continuous Pair of Random Variables 

 {{< katex "(x, y)" true />}}  is a **jointly continuous** pair of random variables if there exists a joint density  {{< katex "f(x, y) \geq 0" true />}}  so that 

 {{< katex >}} P((x, y) \in S) = \int\int_{S}f(x, y)dxdy \text{ where } S \subset \mathbb{R}^2 {{< /katex >}} 



**Definition:** Continuous Random Variable Marginal Density
If the joint density of (x, y) is  {{< katex "f" true />}} , then the two **marginal densities**, which are densities of  {{< katex "X" true />}}  and  {{< katex "Y" true />}} , are computed by integrating the other variables 

 {{< katex >}} f_X(x) = \int^{\infty}_{-\infty} f(x, y)dx {{< /katex >}} 

 {{< katex >}} f_Y(y) = \int^{\infty}_{-\infty} f(x, y)dy {{< /katex >}} 



**Definition:** Continuous Random Variable Independence 
In the continuous case, independence translates into  {{< katex "\forall A, B \subseteq \mathbb{R}" true />}} , 

 {{< katex >}} P(X \in A, Y \in B) = f_X(x)f_Y(y) \iff \int_{A \times B} f(x, y) dxdy = \underbrace{\int_{A} f_X(x)dx}_{P(X \in A)} \underbrace{\int_{B} f_Y(y)dy}_{P(Y \in B)} {{< /katex >}} 
