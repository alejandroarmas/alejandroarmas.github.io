---
layout: article
title: Understanding the Fourier Transform
tags: research interning bees machine-learning
aside:
    toc: true
  
---

# Motivation

For a long time now, the piece of mathematics that is the fourier transform has mistified me. It remains to be one of the most useful equations in engineering, spanning applications from medical imaging to geology (maybe?). In my personal opinion, it is one of the most beautiful equations to exist, so lets get to demistifying it's elagence. 

Before we begin, the reader should know that there is an amazing analogy between vectors and sinusoids. So we will begin with explaining vectors and extend that definition to sines and cosines (sinusoids). We will use that information to then build up to the fourier series, and naturally extend that definition to the fourier transform. 

# Extending the Dot Product Beyond Vectors 

Assume for analogy that a signal is composed of constituient sinusoidal waveforms, which you will soon find to be true. Likewise, any vector is collectively comprised of constituient vectors, which sum to give a resultant vector defined by it's magnititude and phase. Given the geometric definition of the dot product, it is intuitive to see that two two-dimesional vectors are perpendicular if the dot product between them is zero. 

$$ \langle \mathbf{u} , \mathbf{v} \rangle =\|\mathbf{u}\|\ \|\mathbf{v}\|\cos\theta $$

<p>
    <img src="/assets/images/FourierTransform/dot-product-1.gif" alt="Dot Product"/>
    <br>
    <em>
    <a href="https://www.mathsisfun.com/algebra/vectors-dot-product.html">[“Magnitude of two Vectors and the angle between them”]</a>
    </em>
</p>

Consider a $n-$dimensional linear vector euclidean space, with othonormal basis vectors $u_k$, so $ u_i \cdot u_i = 1$ and $ u_i \cdot u_j = 0$ for $ i \neq
 j$. 



This operation typically is used for finding the degree of correlation (similarity metric) or angle between two vectors. Building upon these ideas, you can view the inner product as a generalization of what we remember for the dot product for vectors, but to abstract vector spaces so that geometric concepts can be applied to describe abstract vectors such as sinusoidal waveforms [3](http://linear.ups.edu/download/fcla-3.50-tablet.pdf). The prerequisites for defining an inner product are the properties of commutativity, linearity and the inner product of a function with itself should be positive definite [1](https://www.math.ust.hk/~mabfchen/Math111/Week13-14.pdf).

The vector space $C[a, b]$ of all real-valued continuous functions on a closed interval $[a, b]$ is an inner product space, whose inner product is defined by:

$$ \langle \mathbf{f} , \mathbf{g} \rangle = \int_a^b f(x)g(x)dx \ \ \ f, g \in C[a, b]$$

When you let $f(x)=cos(x)$ and $g(x)=sin(x)$ for a single period, the result will be 0: they are orthogonal.



It is when the signals (vectors) are exactly the same! As similarity reduces the inner product becomes lesser(Note that inner product between 2 vectors gives a single number). So when the inner product is 0 we can say that the signals/ vectors are maximally dissimilar



# Fourier Series 

In general, a complicated signal can be represented in an infinite amount of ways.  In orthogonal sets, whole families of signals can be orthogonal to all other members in the family and they collectively would provide the basis for creating signals [2]. 


Make mistakes so that you learn from them and never make them again.

References

[1] [Beifang Chen, “Inner Product Spaces and Orthogonality week 13-14 Fall 2006”, Department of Mathematics Hong Kong University of Science and Technology, Oct. 2006.](https://www.math.ust.hk/~mabfchen/Math111/Week13-14.pdf)




[2] [John Semmlow. "Signals and Systems for Bioengineers (Second Edition)
A MATLAB-Based Introduction Biomedical Engineering" Elsevier,
2012, Pages 35-80](https://doi.org/10.1016/B978-0-12-384982-3.00002-X)

[3] [Robert A. Beezer, "A First Course in Linear Algebra", Congruent Press
Gig Harbor, Washington, USA, 2015](http://linear.ups.edu/download/fcla-3.50-tablet.pdf)