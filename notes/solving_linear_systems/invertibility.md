---
layout: page
title: Invertibility
nav_order: 11
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
work_in_progress: false 
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Invertibility

**Definition** We say a matrix $A$ is _invertible_ if there is another matrix $B$ such that 
$$
    A B = I = B A.
$$

Invertible matrices are special. 

### Invertible matrices are square

Assume that $AB = BA = I$. 

From $AB = I$ the number of rows of $A$ equals the number of rows of $I$. 

From $BA = I$, 
the number of columns of $A$ equals the number of columns of $I$. 

Since $I$ is a square matrix, 
the number of rows of $A$ and the number of columns of $B$ are equal, ie $A$ is square. 

### Inverses are unique 

In other words, there is at most one $B$ satisfying $AB = I = BA$ for a given $A$. 

Assume that $B,C$ satisfy 
$$
    BA = I = AB \\
    CA = I = AC
$$

Then, we have 
$$
    C = IC = BAC = BI = B. 
$$

We call the unique $B$ such that $BA = I = AB$ the _inverse_ to $A$. 

Since the inverse of $A$ (if it exists!) is unique, we introduce notation that only 
depends on $A$: we write $A^{-1}$ for the inverse of $A$. 

### Inverses don't always exist, even if square

Of course, if $A$ is not square, then $A$ cannot be invertible. 

Let's assume that $A$ is square and 
let us assume we have a vector $\mathbf{v}$ of length $n$ such that 
$$
    A \mathbf{v} = \mathbf{0}.
$$

If $A^{-1}$ exists, then we have 
$$
    \mathbf{v} = I \mathbf{v} = A^{-1} A \mathbf{v} = A^{-1} \mathbf{0} = \mathbf{0}
$$
which is a contradiction. 

For a simple example of a nonzero square matrix that does not have an inverse, take 
$$
    \begin{pmatrix} 
        1 & 0 \\
        0 & 0 
    \end{pmatrix}
$$
Since 
$$
    \begin{pmatrix}
        1 & 0 \\
        0 & 0 
    \end{pmatrix} 
    \begin{pmatrix} 
        0 \\
        1  
    \end{pmatrix} = 
    \begin{pmatrix} 
        0 \\
        0  
    \end{pmatrix} 
$$
this matrix cannot be invertible. 

### If possible inverting twice does nothing  

Assume that $A^{-1}$ exists. What is $\left( A^{-1} \right)^{-1}$? 

Since $A A^{-1} = I = A^{-1} A$, we already know by definition that 
$A$ is the inverse of $A^{-1}$! Thus, 
$$
    \left( A^{-1} \right)^{-1} = A
$$
if $A^{-1}$ exists. 

### Products of invertible matrices are invertible

Assume that $A^{-1}$ and $B^{-1}$ both exist and we want to figure out an 
inverse for $AB$. 

We might first guess that $A^{-1} B^{-1}$ should work? But when we write out 
$$
    A^{-1} B^{-1} AB 
$$
there is no way to simplify the expressions since a matrix isn't touching its 
own inverse. 

However, if we try the opposite order $B^{-1} A^{-1}$ we see that 
$$
    B^{-1} A^{-1} A B = B^{-1} I B = B^{-1} B = I
$$
and 
$$
    A^{-1} B^{-1} B A = A^{-1} I A = A^{-1} A = I
$$
and it works!

We can capture this fact with the notation
$$
    (AB)^{-1} = B^{-1} A^{-1}.
$$

### Sums of invertible matrices are not invertible in general

For example, 
$$
    A + (-A) = 0. 
$$

We will see later that _generically_ this is indeed the case though. 

### Examples 

We have already seen some examples of invertible matrices in our pursuit 
of Gaussian Elimination: $S(i,c), P(i,j), L(i,j,c)$.

We also know that we can undo multiplication by each of these matrices:
- $S(i,c) S(i,1/c) = I$ from [Homework 2]({% link homework/02.md %})
- $P(i,j) P(j,i) = I$ from [Homework 1]({% link homework/01.md %})
- $L(i,j,c) L(i,j,-c) = I$ from [Worksheet 2]({% link worksheets/02.md %})

Rewriting the previous statements in the new notation says
- $S(1,c)^{-1} = S(1,1/c)$ if $c \neq 0$
- $P(i,j)^{-1} = P(i,j)$ and 
- $L(i,j,c)^{-1} = L(i,j,-c)$ if $i \neq j$

### Detecting invertibility?

If we are handed a matrix, how do we efficiently figure out if an matrix is invertible?

It turns out Gaussian elimination allows us to do this. 

Start with a square matrix $A$. We interested in solving $AB = I$. We can break this into 
a list of matrix equations. Before we do so, it useful to introduce some notation. Let 
$$
    \mathbf{e}_j := C_{I_m}^j
$$
denote the column vector that is the j-th column of the $m \times m$ identity matrix $I_m$.

Then solving $AB = I$ is the same as solving the following $m$ systems:
$$
    A C_1^B = \mathbf{e_1} \\
    A C_2^B = \mathbf{e_2} \\
    \vdots \\
    A C_m^B = \mathbf{e_m}
$$
Gaussian elimination certainly helps us here. In fact, we can run Gaussian Elimination _all at once_! 

Let us introduce the notation for the extended augmented matrix: $(A \mid I)$. 

### Gaussian elimination can produce an inverse 

We apply Gaussian Elimination to the extended augmented matrix $(A \mid I)$ to convert 
$A$ to reduced row echelon form. 

**Theorem**. The reduced row echelon form of $A$ is $I$ if and only if $A$ is invertible. 

Moreover, if the result of reducing $(A \mid I)$ is $(I \mid B)$, then $B = A^{-1}$. 

**Proof**. The first statement becomes clearer when we make a useful observation.
Assume $A$ and $A^\prime$ are related by a row operation. 

If either $A$ or $A^\prime$ is invertible, so is the other one. Why? We know that 
$$
    A^\prime = E A
$$
where $E = S(i,c)$ for $c \neq 0$, $P(i,j)$, or  $L(i,j,c)$ for $i \neq j$. We have seen that 
in each of these cases $E^{-1}$ exists. 

Assume that $A$ is invertible. As $E$ is also invertible, the product 
$A^\prime = EA$ is invertible. 

Assume that $A^\prime$ is invertible, we can use $E^{-1}$ and write 
$$
    E^{-1} A^\prime = A 
$$
with both $E^{-1}$ and $A^\prime$ invertible. Thus $A$ is invertible. 

Now assume we can reduce $A$ to $I$. Then, 
$$
    I = E_t E_{t-1} \cdots E_1 A 
$$
for some list of row operation matrices. Rewriting this using the inverses gives 
$$
    E_1^{-1} \cdots E_t^{-1} I = A
$$
Since $A$ is a product of invertible matrices, it is also invertible. This fact is 
part of your [homework]({% link homework/02.md%}).

Now, assume $A$ is invertible and let $A^\prime$ be the result of using Gaussian 
Elimination to produce a matrix in reduced row echelon form. As above, we know 
that 
$$
    A^\prime = E_t E_{t-1} \cdots E_1 A 
$$
and so that $A^\prime$ must also be invertible. Also part of your 
[homework]({% link homework/02.md%}) is to prove that the only invertible matrix 
in reduced row echelon form is $I$. 

Let's turn to proving the second statement. Assume that we can reduce 
$(A \mid I)$ to $(I \mid B)$. Then, we know that 
$$
    (I \mid B) = E_t E_{t-1} \cdots E_1 (A \mid I) = 
    (E_t E_{t-1} \cdots E_1 A \mid E_t E_{t-1} \cdots E_1)
$$
so $B = E\_t E\_{t-1} \cdots E\_1$ and we see that $BA = I$. Since we can reduce 
$A$ to $I$, we know that $A^{-1}$ exists. Multiplying by $A^{-1}$ on the right we 
have 
$$
    A^{-1} = I A^{-1} = (BA)A^{-1} = B(AA^{-1}) = B I
$$
So $B = A^{-1}$. 