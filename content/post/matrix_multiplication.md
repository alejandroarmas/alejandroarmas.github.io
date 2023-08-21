+++
title = "Primer on Matrix Multiplication" 
author = "Alejandro Armas"
tags = ["Mathematics"]
date = 2020-05-27
+++


### Introduction

Remember the good ol days when 6 x 5 easily made sense as adding 6 together with itself 5 times and whala you ended up with 30. Now you're in college and things are hard 😭 Hopefully running through an example can give you a bit of a glimpse as to how and why we do matrix multiplication.

  

### How to Compute Matrix Multiplication

  

Consider two Matricies **A** and **B**. We denote the dimensions by *row* and *columns*, in that order. **A** is of dimensions 2 x 3. **B** is 3x2.

  

{{< katex >}} 

\bf{A} =

\begin{bmatrix}

1 & 2 & 3\\

4 & 5 & 6

\end{bmatrix}

{{< /katex >}} 

  

{{< katex >}} 

\bf{B} =

\begin{bmatrix}

5 & 4\\

3 & 2\\

1 & 0

\end{bmatrix}

{{< /katex >}} 

  
  

Matrix Multiplication is defined as the dot product between each row within the first matrix **A** and each column of the second matrix **B**:

  

{{< katex >}} 
\begin{aligned}

\bf{A} \times \bf{B} &= \bf{C}

\\&=

\begin{bmatrix}

1 & 2 & 3\\

4 & 5 & 6

\end{bmatrix}


\begin{bmatrix}

5 & 4\\

3 & 2\\

1 & 0

\end{bmatrix}

\\&=

\begin{bmatrix}

5(1) + 3(2) + 1(3) & 4(1) + 2(2) + 0(3)\\

5(4) + 3(5) + 1(6) & 4(4) + 2(5) + 0(6)

\end{bmatrix}

\\&=

\begin{bmatrix}

5 + 6 + 3 & 4 + 4 + 0\\

10 + 15 + 6 & 16 + 10 + 0

\end{bmatrix}  

\\&=

\begin{bmatrix}

14 & 8\\

41 & 26

\end{bmatrix}

\end{aligned} 
{{< /katex >}} 

  


Recall the dimensions of matricies **A** and **B** are two by three (2 x 3) and three by two (3 x 2) respectively and notice how the 2 rows in **A** multiplied with the 2 columns in **B**.

  

We can conclude that for matrix multiplication between any two matricies requires the number of columns in your first matrix be identical to the number of rows in your second matrix being multiplied.

  

Formally we define a matrix **A** of size n x b and the second matrix **B** to be of  {{< katex "b \times m" true />}} :

 {{< katex >}} 
 \bf{A} =

\begin{bmatrix}

a_{11} & a_{12} & \dots & a_{1b}\\

a_{21} & a_{22} & \dots & a_{2b}\\

\dots & \dots & \dots & \dots \\

a_{n1} & a_{n2} & \dots & a_{nb}

\end{bmatrix} 
{{< /katex >}} 

  

{{< katex >}} 
\bf{B} =
  

\begin{bmatrix}

b_{11} & b_{12} & \dots & b_{1m}\\

b_{21} & b_{22} & \dots & b_{2m}\\

\dots & \dots & \dots & \dots \\

b_{b1} & b_{b2} & \dots & b_{bm}

\end{bmatrix} 
{{< /katex >}} 

  

In general the multiplication of two matricies:

  

{{< katex >}} \bf{A} \bf{B} = \bf{C} {{< /katex >}} 

  

 {{< katex >}} \begin{aligned}
\begin{bmatrix}

a_{11} & a_{12} & \dots & a_{1b}\\

a_{21} & a_{22} & \dots & a_{2b}\\

\dots & \dots & \dots & \dots \\

a_{n1} & a_{n2} & \dots & a_{nb}

\end{bmatrix}

  

\begin{bmatrix}

b_{11} & b_{12} & \dots & b_{1m}\\

b_{21} & b_{22} & \dots & b_{2m}\\

\dots & \dots & \dots & \dots \\

b_{b1} & b_{b2} & \dots & b_{bm}

\end{bmatrix}

  

&=

  

\begin{bmatrix}

c_{11} & c_{12} & \dots & c_{1m}\\

c_{21} & c_{22} & \dots & c_{2m}\\

\dots & \dots & \dots & \dots \\

c_{n1} & c_{n2} & \dots & c_{nm}

\end{bmatrix}

\end{aligned}

 {{< /katex >}} 

  

Multiplication **A** x **B** results in a final matrix that is of dimension n x m. Origininally we took the dot product from the first row of matrix **A** with the first column Primer on of matrix **B** and that gave us the first index, which formally is said to be  {{< katex "c_{11} = \sum_{k=0}^{b}a_{1k} \cdot b_{k1}" true />}} .

  
In general, each index is computed with the formula:

 {{< katex >}} 

### Introduction

c_{ij} = \sum_{k=0}^{b}a_{ik} \cdot b_{kj}

 {{< /katex >}} 

  
### Intuition behind Matrix Multiplication.

  

Now consider a system of equations.

  

 {{< katex >}} 

a = 1x + 2y + 3z

 {{< /katex >}} 

  

 {{< katex >}} 

b = 4x + 5y + 6z

 {{< /katex >}} 

  

We can formulate some matrix **A** to represent the linear transformation of (x,y,z) space into (a,b) coordinate space. Formally we define a matrix which represents a linear transformation:

  

 {{< katex >}} 

\bf{A} =

  

\begin{bmatrix}

1 & 2 & 3\\

4 & 5 & 6

\end{bmatrix}

  
  

 {{< /katex >}} 

  

We can see now that any vector **v** = (x, y , z) can be transformed into vector **v'** = (a, b) by this matrix **A**.

  

 {{< katex >}} 

\begin{bmatrix}

a \\

b

\end{bmatrix}

  

=

  

\begin{bmatrix}

1 & 2 & 3\\

4 & 5 & 6

\end{bmatrix}

  

\begin{bmatrix}

x \\

y \\

z

\end{bmatrix}

  

 {{< /katex >}} 

  
  

Written more compactly as:

  

 {{< katex >}} 

\bf{v'} = \bf{A} \bf{v}

 {{< /katex >}} 

  

Now let us define another matrix **B** representing the following set of linear equations:

  

 {{< katex >}} 

i = 5a + 4b

 {{< /katex >}} 

  

 {{< katex >}} 

j = 3a + 2b

 {{< /katex >}} 

  

 {{< katex >}} 

k = 1a + 0b

 {{< /katex >}} 

  

Then,

  

 {{< katex >}} 

\bf{B} =

  

\begin{bmatrix}

5 & 4\\

3 & 2\\

1 & 0

\end{bmatrix}

 {{< /katex >}} 

  

Is the matrix which is used in the transformation of any vector **v'** = (a,b) to a vector **w** = (i, j, k). We see the transformation is written as:

  

 {{< katex >}} 

  

\begin{bmatrix}

i \\

j \\

k

\end{bmatrix}

  

=

  

\begin{bmatrix}

5 & 4\\

3 & 2\\

1 & 0

\end{bmatrix}

  
  

\begin{bmatrix}

a \\

b

\end{bmatrix}

  

 {{< /katex >}} 

  

Written more compactly as:

  

 {{< katex >}} 

\bf{w} = \bf{B} \bf{v'}

 {{< /katex >}} 

  

Now if we wanted to transform any vector **v** = (x, y, z) into the vector space of **w** = (i, j , k), we would use:

  

 {{< katex >}} 

\begin{bmatrix}

i \\

j \\

k

\end{bmatrix}

  

=

  

\begin{bmatrix}

5 & 4\\

3 & 2\\

1 & 0

\end{bmatrix}

  

\begin{bmatrix}

1 & 2 & 3\\

4 & 5 & 6

\end{bmatrix}

  

\begin{bmatrix}

x \\

y \\

z

\end{bmatrix}

  

 {{< /katex >}} 

  

Written more compactly as:

  

 {{< katex >}} 

\bf{w} = \bf{B} \bf{A} \bf{v}

 {{< /katex >}} 

  

This is where matrix multiplication comes into place, you can think of **B** x **A** as the composition of these two linear functions into one matrix transformation. Notice we used the same matricies **A**, **B** in the first section. Well multiplication is not communitive and we shall notice that we get a different result for the matrix multiplication when they are ordered differently.

  

 {{< katex >}} 
\begin{aligned}
\bf{D} &= \bf{B} \times \bf{A} 

\\&=

\begin{bmatrix}

5 & 4\\

3 & 2\\

1 & 0

\end{bmatrix}

\begin{bmatrix}

1 & 2 & 3\\

4 & 5 & 6

\end{bmatrix}

  

\\&=



\begin{bmatrix}

1(5) + 4(4) & 2(5) + 5(4) & 3(5) + 6(4)\\

1(3) + 4(2) & 2(3) + 5(2) & 3(3) + 6(2)\\

1(1) + 4(0) & 2(1) + 5(0) & 3(1) + 6(0)

\end{bmatrix}

\\&=

\begin{bmatrix}

5 + 16 & 10 + 20 & 15 + 24\\

3 + 8 & 6 + 10 & 9 + 12\\

1 + 0 & 2 + 0 & 3 + 0

\end{bmatrix}

  

\\&=

\begin{bmatrix}

21 & 30 & 39\\

11 & 16 & 21\\

1 & 2 & 3

\end{bmatrix}

\end{aligned}
 {{< /katex >}} 

  

  

And we can write our transformation from vector space **v** = (x, y, z) to vector space **w** = (i, j , k) as

  

 {{< katex >}} 

  

\begin{bmatrix}

i \\

j \\

k

\end{bmatrix}

  

=

  

\begin{bmatrix}

21 & 30 & 39\\

11 & 16 & 21\\

1 & 2 & 3

\end{bmatrix}

  
  

\begin{bmatrix}

x \\

y \\

z

\end{bmatrix}

  

 {{< /katex >}} 

  

Written more compactly as:

  

 {{< katex >}} 

\bf{w} = \bf{D} \bf{v}

 {{< /katex >}} 
