---
layout: article
title: Matrix Multiplication
tags:  Mathematics
aside:
    toc: true
  
---

Remember the good ol days when 6 x 5 easily made sense as adding 6 together with itself 5 times and whala you ended up with 30. Now you're in college and things are hard :( Hopefully running through an example can give you a bit of a glimpse as to how and why we do matrix multiplication.

## How to Compute Matrix Multiplication

Consider two Matricies **A** and **B**. We denote the dimensions by *row* and *columns*, in that order. **A** is of dimensions 2 x 3. **B** is 3x2. 

$$
\boldsymbol{A} = 

\begin{pmatrix}
1 & 2 & 3\\
4 & 5 & 6
\end{pmatrix}
$$

$$
\boldsymbol{B} = 
\begin{pmatrix}
5 & 4\\
3 & 2\\
1 & 0
\end{pmatrix}
$$


Matrix Multiplication is defined as the dot product between each row within the first matrix **A** and each column of the second matrix **B**.

$$
\boldsymbol{A} \times \boldsymbol{B} = \boldsymbol{C} = 

\begin{pmatrix}
1 & 2 & 3\\
4 & 5 & 6
\end{pmatrix}

\begin{pmatrix}
5 & 4\\
3 & 2\\
1 & 0
\end{pmatrix}
$$

When we compute this, we arrive at:

$$
\boldsymbol{A} \times \boldsymbol{B} = 

\begin{pmatrix}
5(1) + 3(2) + 1(3) & 4(1) + 2(2) + 0(3)\\
5(4) + 3(5) + 1(6) & 4(4) + 2(5) + 0(6) 
\end{pmatrix}\

= 

\begin{pmatrix}
5 + 6 + 3 & 4 + 4 + 0\\
10 + 15 + 6 & 16 + 10 + 0 
\end{pmatrix}\

=

\begin{pmatrix}
14 & 8\\
41 & 26 
\end{pmatrix}\
$$

Thus we know,

$$
\boldsymbol{C} = 

\begin{pmatrix}
14 & 8\\
41 & 26 
\end{pmatrix}\

$$

Recall the dimensions of matricies **A** and **B** are 2 x 3 and 3 x 2 respectively and notice how the 2 rows in **A** multiplied with the 2 columns in **B**. 

We can conclude that for matrix multiplication between any two matricies requires the dimension of the first to be of m x b and the second to be of b x n, resulting in a final matrix that is m x n. 

## Intuition behind Matrix Multiplication.

Now consider a system of equations. 

$$
a = 1x + 2y + 3z
$$

$$
b = 4x + 5y + 6z 
$$

We can formulate some matrix **A** to represent the linear transformation of (x,y,z) space into (a,b) coordinate space. Formally we define a matrix which represents a linear transformation:

$$
\boldsymbol{A} = 

\begin{pmatrix}
1 & 2 & 3\\
4 & 5 & 6
\end{pmatrix}


$$

We can see now that any vector **v** = (x, y , z) can be transformed into vector **v'** = (a, b) by this matrix **A**.

$$
\begin{pmatrix}
a \\
b 
\end{pmatrix}

=

\begin{pmatrix}
1 & 2 & 3\\
4 & 5 & 6
\end{pmatrix}

\begin{pmatrix}
x \\
y \\
z 
\end{pmatrix}

$$


Written more compactly as:

$$
\boldsymbol{v'} = \boldsymbol{A} \boldsymbol{v} 
$$

Now let us define another matrix **B** representing the following set of linear equations:

$$
i = 5a + 4b
$$

$$
j = 3a + 2b
$$

$$
k = 1a + 0b
$$

Then, 

$$
\boldsymbol{B} = 

\begin{pmatrix}
5 & 4\\
3 & 2\\
1 & 0
\end{pmatrix}
$$

Is the matrix which is used in the transformation of any vector **v'** = (a,b) to a vector **w** = (i, j, k). We see the transformation is written as:

$$

\begin{pmatrix}
i \\
j \\
k
\end{pmatrix}

= 

\begin{pmatrix}
5 & 4\\
3 & 2\\
1 & 0
\end{pmatrix}


\begin{pmatrix}
a \\
b 
\end{pmatrix}

$$

Written more compactly as:

$$
\boldsymbol{w} = \boldsymbol{B} \boldsymbol{v'} 
$$

Now if we wanted to transform any vector **v** = (x, y, z) into the vector space of **w** = (i, j , k), we would use:

$$
\begin{pmatrix}
i \\
j \\
k
\end{pmatrix}

= 

\begin{pmatrix}
5 & 4\\
3 & 2\\
1 & 0
\end{pmatrix}

\begin{pmatrix}
1 & 2 & 3\\
4 & 5 & 6
\end{pmatrix}

\begin{pmatrix}
x \\
y \\
z 
\end{pmatrix}

$$

Written more compactly as:

$$
\boldsymbol{w} = \boldsymbol{B} \boldsymbol{A} \boldsymbol{v} 
$$

This is where matrix multiplication comes into place, you can think of **B** x **A** as the composition of these two linear functions into one matrix transformation. Notice we used the same matricies **A**, **B** in the first section. Well multiplication is not communitive and we shall notice that we get a different result for the matrix multiplication when they are ordered differently.

$$
\boldsymbol{B} \times \boldsymbol{A} = \boldsymbol{D} = 

\begin{pmatrix}
5 & 4\\
3 & 2\\
1 & 0
\end{pmatrix}


\begin{pmatrix}
1 & 2 & 3\\
4 & 5 & 6
\end{pmatrix}

=

$$

$$

\boldsymbol{D} = 

\begin{pmatrix}
1(5) + 4(4) & 2(5) + 5(4) & 3(5) + 6(4)\\
1(3) + 4(2) & 2(3) + 5(2) & 3(3) + 6(2)\\
1(1) + 4(0) & 2(1) + 5(0) & 3(1) + 6(0)
\end{pmatrix}

=

\begin{pmatrix}
5 + 16 & 10 + 20 & 15 + 24\\
3 + 8 & 6 + 10 & 9 + 12\\
1 + 0 & 2 + 0 & 3 + 0
\end{pmatrix}

=

\begin{pmatrix}
21 & 30 & 39\\
11 & 16 & 21\\
1 & 2 & 3
\end{pmatrix}
$$

Compactly.

$$
\boldsymbol{D} = 

\begin{pmatrix}
21 & 30 & 39\\
11 & 16 & 21\\
1 & 2 & 3
\end{pmatrix}

$$

And we can write our transformation from vector space **v** = (x, y, z) to vector space **w** = (i, j , k) as 

$$

\begin{pmatrix}
i \\
j \\
k
\end{pmatrix}

= 

\begin{pmatrix}
21 & 30 & 39\\
11 & 16 & 21\\
1 & 2 & 3
\end{pmatrix}


\begin{pmatrix}
x \\
y \\
z 
\end{pmatrix}

$$

Written more compactly as:

$$
\boldsymbol{w} = \boldsymbol{D} \boldsymbol{v} 
$$
