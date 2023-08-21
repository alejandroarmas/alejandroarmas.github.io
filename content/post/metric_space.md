+++
title = "Quick Primer on Metric Spaces"
author = "Alejandro Armas"
tags = ["Mathematics"] 
date = 2020-06-18
+++

### Vector Space

A vector space is set of mathemetical objects that can be multiplied and added together to produce objects of the same kind. This notion of vector spaces proves to be a very useful framework for extending methods and structures to very different types of problems. A few special types of vector spaces you may be already be familiar with:


##### Function Spaces

We can add functions together and scale them as well. 


{{< figure src="/posts/vector_space/images/Function.png" alt="Function Graphed" caption="Figure 1: Additive Property of Functions" class="figure-container">}}



In Figure 1 we can see there exists:
1. A function in blue  {{< katex "f(x) = x" true />}} 
2. A function in red  {{< katex "g(x) = \sin(x)" true />}} 

Taking the summation of these two functions produces a third function in green  {{< katex "(f + g)(x) = \sin(x) + x " true />}} 

##### Euclidean Spaces 

We can add  {{< katex "i, j, k" true />}} together and scale them as well to produce a vector {{< katex "a" true />}} . 

{{< figure src="/posts/vector_space/images/Vector.png" alt="Function Graphed" caption="Figure 2: Vector Space Visualized. " class="figure-container">}}



Typically this is the vector space you learn in linear algebra because it is intuitive to understand and very helpful for extending additional structure into spaces. 

### More Formally

**Definition**: A *field* is a set  {{< katex "\mathbb{F}" true />}}  of numbers, such that  {{< katex "a, b \in \mathbb{F} \implies a+ b, a - b, ab, \frac{a}{b} \in \mathbb{F}." true />}}  Some examples of sets that would count as fields are the real numbers  {{< katex "\mathbb{R}" true />}}  and the complex numbers  {{< katex "\mathbb{C}" true />}} .

**Definition**: A *Vector Space* consists of a set  {{< katex "\textbf{V}" true />}} , a field  {{< katex "\mathbb{F}" true />}}  and two operations:

*  Vector Addition:  {{< katex "\textbf{a}, \textbf{b} \in \textbf{V} \implies \textbf{a} + \textbf{b} \in \textbf{V}" true />}} 
*  Scalar Multiplication:  {{< katex "c \in \mathbb{F}, \textbf{v} \in \textbf{V} \implies c\textbf{v} \in \textbf{V}" true />}} 


### Metric Space 

Essentially a metric is a measurement to see how similar two vectors are to one another. In geometrical terms, this similarity could be interpreted as distance. 

**Definition**: A *Metric Space* consists of a set  {{< katex "\textbf{V}" true />}} , and has a notion of distance  {{< katex "d(x,y) \ \forall x, y \in \textbf{V}" true />}} . That is  {{< katex "d : \textbf{V} \times \textbf{V} \to [0;\infty)" true />}}  and satisfies these following properties  {{< katex "\forall x,y,z \in \textbf{V}" true />}} :

*  Identification:  {{< katex "d(x,y) = 0 \implies x = y" true />}} 
*  Symmetry:  {{< katex "d(x,y) = d(y,x)" true />}} 
*  Triangle Inequality:  {{< katex "d(x,y) \leq d(x,z) + d(z,y)" true />}} 

As long as these axioms hold true for a particular vector space with a function d, then it can be categorized as a metric space. A few examples you may be familiar with are the euclidean distance metric, or L2. 

{{< katex >}} 
d(x,y) = \sqrt{\sum_{i = 0}^n \mid x_i - y_i\mid^2}  
{{< /katex >}} 
