---
layout: article
title: Understanding the Fourier Transform
tags: signal-processing math electrical-engineering
aside:
    toc: true
  
---

# Motivation

For a long time now, the piece of mathematics that is the fourier transform has mistified me. It remains to be one of the most useful equations in engineering, spanning applications from medical imaging to geology (maybe?). In my personal opinion, it is one of the most beautiful equations to exist, so lets get to demistifying it's elagence. 

Before we begin, the reader should know that there is an amazing analogy between vectors and sinusoids. So we will begin with explaining vectors and extend that definition to sines and cosines (sinusoids). We will use that information to then build up to the fourier series, and naturally extend that definition to the fourier transform. 

# Extending the Dot Product Beyond Vectors 

 Just as any vector is superimposed by constituient vectors, any arbitrary signal is composed of constituient sinusoidal waveforms. Consider the dot product, which provides a geometric meaning of being perpendicular (orthogonality) in vector space. We can readily observe that our vector $ \mathbf{V} = a_{1} \hat{x} + a_{2} \hat{y} + a_{3} \hat{z}$ is a superposition of the 3 basis vectors $ \hat{x} , \hat{y} , \hat{z} $, each orthogonal to one another and scaled by some factor $a_{1} , a_{2}, a_{3} $. In general we observe the dot between any two basis vectors to be $$ \hat{x}_{i} \cdot \hat{x}_{j} = \left\{
        \begin{array}{ll}
            0 & \quad i = j\\
            1 & \quad i \neq j
        \end{array}
    \right. $$

<p>
    <img src="/assets/images/Fourier/VectorComponents.png" alt="Vector V superimposed"/>
    <br>
    <em>
    <a href="https://www.mathsisfun.com/algebra/vectors-dot-product.html">[“Fourier Transforms & Applications in Imaging” by Brian H. Kolner]</a>
    </em>
</p>

Now if we wanted some procedure to extract these scaling factors $ a_{1} , a_{2}, a_{3} $, we simply perform $ \mathbf{V} \cdot a_{1}\hat{x}_{1} = a_{1}$ . This is called the projection of the component in the $\hat{x}_{1}$ direction, similarily called the coefficient decomposition.

The dot product typically is used for finding the degree of correlation (similarity metric) or angle between two vectors. Two vectors pointing in the same direction when dotted evaluate to 1. Building upon these ideas, you can view the inner product as a generalization of what we remember for the dot product for vectors, but to abstract vector spaces so that geometric concepts can be applied to describe abstract vectors such as sinusoidal waveforms [3](http://linear.ups.edu/download/fcla-3.50-tablet.pdf). The prerequisites for defining an inner product are the properties of commutativity, linearity and the inner product of a function with itself should be positive definite [1](https://www.math.ust.hk/~mabfchen/Math111/Week13-14.pdf).

The vector space $C[a, b]$ of all real-valued continuous functions on a closed interval $[a, b]$ is an inner product space, whose inner product is defined by:

$$ \langle \mathbf{f} , \mathbf{g} \rangle = \int_a^b f(x)g(x)dx \ \ \ f, g \in C[a, b]$$

When you let $f(x)=cos(x)$ and $g(x)=sin(x)$ for a single period, the result will be 0: they are orthogonal. However if you instead choose $f(x)=cos(x)$ and $g(x)=cos(x)$ the result is 1. These signals are identical! As similarity reduces the inner product becomes lesser. So when the inner product is 0 we can say that the signals/ vectors are maximally dissimilar.



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