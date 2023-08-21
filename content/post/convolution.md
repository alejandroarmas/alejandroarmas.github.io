+++
title = "Mathematics Meets Signal Processing: Exploring the Convolution Integral"
author = "Alejandro Armas"
tags = ["Electrical Engineering", "Mathematics", "Signal Processing"] 
date = 2020-04-22
+++

### Introduction

Since signals are sets of data or information and systems process said data, we are interested in the analysis of systems. When we deal with a special type of system that contains the properties of **linearity** and **time-invariance**, we are able to construct methods of analysis that are extremely useful for Linear Time-invariant (LTI) systems. Fourier analysis, which will be a seperate blog post, and the convolution integral are examples of exploiting system properties to decompose inputs into basic signals which are easy to work with analytically. Let's have a little refresher first with these two properties.
## Linearity and Time Invariance


**Time-invariance** is the property of a system that when an input is shifted in time, then it's subsequent output is shifted by the same amount of time.

  {{< katex >}}  \text{If:} \ \ \ \ \ \ f(t) \implies y(t) \\ \text{then:} \ f(t - t_{0}) \implies y(t - t_{0}) {{< /katex >}} 

**Linearity** implies set of independent outputs can be superimposed into one output.

 {{< katex >}}  \text{If:} \ \ \ c_{1}f_{1}(t) \implies c_{1}y_{1}(t) \ \text{and} \ c_{2}f_{2}(t) \implies c_{2}y_{2}(t) \\ \text{then:} \ \ \ \ \ \ \ \ \ \ c_{1}f_{1}(t) + c_{2}f_{2}(t) \implies c_{1}y_{1}(t) + c_{2}y_{2}(t) {{< /katex >}} 

## Convolution


Before we begin convolution, we must represent any arbitrary signal as a summation over a set of infinitely many weighted impulses  {{< katex " \delta(x) " true />}} . Recall:

{{< katex >}}  
\delta(t) = \begin{cases}
\infty & \text{if } t = 0,\\
0 & \text{if } t \neq 0\\
\end{cases} 
{{< /katex >}} 

Since for all values  {{< katex "t \neq 0, f(t) = 0" true />}}  due to multiplication by  {{< katex "\delta(t)" true />}}  ...

 {{< katex >}}  f(0) = f(t) \cdot \delta(t) {{< /katex >}} 

Equivilantly can be formulated as:

 {{< katex >}}  f(0) = f(0) \cdot \delta(t) {{< /katex >}} 


And with Time-invariance we note...

 {{< katex >}}  f(1) = f(1) \cdot \delta(t - 1) {{< /katex >}} 

Therefore we can construct any arbitrary  {{< katex "f(t)" true />}}  as  {{< katex "f_{n}(t)" true />}}  using this idea. 

 {{< katex >}}  f_{n}(t) = \sum_{k = -\infty}^{\infty} f(k) \cdot \delta(t - k) {{< /katex >}} 

We denote the system response *beginning* at k (unit impulse response) at time to a impulse signal delayed by k as:

 {{< katex >}}  h_{k}(t) = \delta(t - k) {{< /katex >}} 

Due to our good old friend Time-invariance, we can rewrite the unit impulse system response *beginning* at 0 delayed by k as:

 {{< katex >}} h_{k}(t) = h_{0}(t - k)  {{< /katex >}} 


Now if we input this newly constructed arbitrary function into a LTI system we note the response of the linear combination of these inputs  {{< katex " f_{n}(t)" true />}}  is a linear combination of each weighted impulse response  {{< katex "h_{k}(t)" true />}} .

 {{< katex >}}  y(t) = \sum_{k = -\infty}^{\infty} f_{n}(k) \cdot h_{k}(t) {{< /katex >}} 

or


 {{< katex >}}  y(t) = \sum_{k = -\infty}^{\infty} f_{n}(k) \cdot h_{0}(t - k) {{< /katex >}} 

Now with a little big of calculus and replacing our notation and variable k with  {{< katex "\tau" true />}} .

 {{< katex >}}  y(t) = f(t) * h(t) = \int_{-\infty}^{\infty} f(\tau) \cdot h(t - \tau)d\tau {{< /katex >}} 

Intuitively, this integral could be thought of as some infinitesimally thin sample of f(t) we denote as  {{< katex "d\tau" true />}}  input into our system where we obtain a infinitesimely thin system response  {{< katex "h(t - d\tau)" true />}}  repeated over infinity to produce a summation of infinitely thin responses to the system. I highly recommend [this video](https://www.youtube.com/watch?v=acAw5WGtzuk) to give a good visual of what is going on.

## Conclusion

Now the real incredible part is now that we are capable of characterizing the entire system simply by the transmittion of some instantaneous excitation into the system!


## References

[Lecture 4, Convolution by *Alan V. Oppenheim*. MIT RES.6.007 Signals and Systems, Spring 2011](https://www.youtube.com/watch?v=_vyke3vF4Nk)
