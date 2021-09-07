---
layout: page
title: Sage
nav_order: 3
has_children: false
has_toc: false
parent: Notes
work_in_progress: false 
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Sage Basics 

[Sage](https://www.sagemath.org/) is a robust mathematical-software system built upon Python.  
It provides a solid back-up tool for checking your computations. Its extensibility allows you write 
programs in Sage to create new tools for your particular problem. 

Use of Sage will not be required for any assignments but you will definitely find it helpful.

### Installation

There are three ways to use it: 
- [Install Sage on your own computer](https://doc.sagemath.org/html/en/installation/). 
- Use a [CoCalc instant Sage worksheet](https://cocalc.com/app?anonymous=sagews&utm_source=sagemath.org&utm_medium=landingpage) online.
- Use [Sage Math Cell](https://sagecell.sagemath.org/) online.

If you want to use Sage occasionally, online use might be sufficient for you. If you are using it online, a CoCalc instant worksheet is 
your best option. Sage installs are superior for ease of access and storing your work. 

### Linear algebra basics

Sage has a multitude of libraries for different branches of math. We will focus on linear algebra in 
Sage. You can find a [cheat sheet](https://wiki.sagemath.org/quickref?action=AttachFile&do=view&target=quickref-linalg.pdf) 
which includes all the examples we cover here and more. 

Let's start with the basics. Comments are written after a # symbol. It is a good idea to mess around and try mathematical 
operations that are not defined, like adding vectors of different length. The output you get out is helpful.

How to make vectors and matrices:

```python
v = vector([1,2]) # defines a vector (1,2) 
A = matrix([[1,2],[3,4],[5,6]]) # gives a 3x2 matrix with rows (1,2), (3,4), (5,6)
I = identity_matrix(3) # 3x3 identity matrix
```

How to add and multiply vectors and matrices:

```python
v = vector([1,2])
w = vector([0,1])
5*v - w # a linear combination of v and w
A = matrix([[1,2],[3,4]]) 
B = matrix([[0,1],[1,0]])
2*A - 3*B # a linear combination of matrices 
A*B # multiplication of matrices
```

We can check if a matrix is invertible or square or check its size.

```python
A = matrix([[1,2,3],[4,5,6],[7,8,9]])
A.is_invertible() # returns False
A.is_square() # returns True
A.nrows() # 3 rows 
A.ncolumns() # 3 columns
```

We also have access to all row operations - but remember that indexing begins as $0$.

```python 
A.rescale_row(i,a) # scales row i 
A.add_multiple_of_row(i,j,a) # replaces row i with row i + a(row j)
A.swap_rows(i,j) # exchanges row i and row j
```

With this we can perform Gaussian elimination step by step. But Sage also has built in functions 
for computing reduced row echelon form. 

```python
B = matrix([[1,-1,0,0],[0,2,1,-1],[1,1,1,0]]) 
B.rref() # outputs
# [  1   0 1/2   0]
# [  0   1 1/2   0]
# [  0   0   0   1]
```

We can create augmented matrices. The setting `subdivide=true` puts the bars in the augmented matrix. 

```python
A = matrix([[1,0,0],[0,1,0],[0,0,0]]) 
B = A.augment(matrix([[1],[2],[3]]),subdivide=true) # the augmented matrix A | b. 
# output 
# [1 0 0|1]
# [0 1 0|2]
# [0 0 0|3]
```

### Examples

Let's solve the system 
$$
    \begin{aligned}
        5x - 2y + 3z + w & = 1 \\
        x + y + z + w & = -1 \\
        x - 3y - 2z - w & = 0 
    \end{aligned}
$$

We can create the augmented matrix 

```python
A = matrix([[5,-2,3,1],[1,1,1,1],[1,-3,-2,-1]])
v = vector([1,-1,0])
B = A.augment(v, subdivide=true)
B.rref() 
# outputs 
# [     1      0      0   7/13|-14/13]
# [     0      1      0   8/13|-16/13]
# [     0      0      1  -2/13| 17/13]
```
So $x_4$ is the only free variable and we can present the general solution as 
$$
    \begin{aligned}
        x_1 & = -\frac{14}{13} - \frac{7}{13} x_4 \\
        x_2 & = -\frac{16}{13} - \frac{8}{13} x_4 \\
        x_3 & = \frac{17}{13} + \frac{2}{13} x_4
    \end{aligned}
$$

Next let's figure out if $A$ is invertible where 
$$
    A = 
    \begin{pmatrix}
        1 & -1 & 0 \\
        0 & 1 & -1 \\
        1 & 0 & -1
    \end{pmatrix} 
$$

There is a direct function for this `A.inverse()`. Try running 

```python
A = matrix([[1,-1,0],[0,1,-1],[1,0,-1]])
A.inverse()
```

and the output will be a string of text which starts with `ZeroDivisionError` and 
ends with `ZeroDivisionError: matrix must be nonsingular`. Nonsingular is a synonym for 
invertible. It is telling us that $A$ is not invertible. 

If we wanted to see this another way, we could try the following.

```python 
B = A.augment(identity_matrix(3), subdivide=true)
B.rref()
# output 
# [ 1  0 -1| 0  0  1]
# [ 0  1 -1| 0  1  0]
# [ 0  0  0| 1  1 -1]
```

Since the left hand side is not $I$, we know that $A$ is not invertible. 

If you did this by hand, then you might end up with 
$$
    \begin{pmatrix}
        1 & 0 & -1 & \bigg| & 1 & 1 & 0 \\
        0 & 1 & -1 & \bigg| & 0 & 1 & 0 \\
        0 & 0 & 0 & \bigg| & -1 & -1 & 1
    \end{pmatrix} 
$$

It is important to note that Sage performs Gaussian Elimination on the whole, ie both sides, of an augmented matrix. 
This is harmless in terms of correctness but more work for humans. 

Lets compute the range of the previous matrix. First we want to add variables into the system and then we will try 
to reduce the result. 

```python
var('b1 b2 b3') # declares symbolic variables b1, b2, b3 
v = vector([b_1,b_2,b_3])
A.augment(v) # doesn't work 
B = matrix([[1,-1,0,b1],[0,1,-1,b2],[1,0,-1,b3]]) # by hand 
B.rref() 
# output is clearly not correct 
# [ 1  0 -1  0]
# [ 0  1 -1  0]
# [ 0  0  0  1] 
```

Sage is assuming that the symbolic variables will not evaluate to $0$ and using row operations to eliminate. If we want to keep 
them around, then we proceed step by step using row operations.

```python
B.add_multiple_of_row(2,0,-1) # subtract the first row from the third 
B.add_multiple_of_row(2,1,-1) # subtract row 2 from row 3
B 
# output 
# [            1            -1             0            b1]
# [            0             1            -1            b2]
# [            0             0             0 -b1 - b2 + b3]
```

So the range is given by the equation $-b_1 - b_2 + b_3 = 0$. 