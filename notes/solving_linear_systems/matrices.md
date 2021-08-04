---
layout: page
title: Matrices
nav_order: 4
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
---

## Matrices 

Conceptually, a matrix is a list of vectors. But, as we will see, how that is done precisely depends 
on some convention and we will want to appeal to both conventions. 

A *matrix* $A$ of size $n \times m$ is a list of numbers $a_{ij}$ (we will also sometimes write $A_{ij}$)
indexed by pairs $(i,j)$ for $1 \leq i \leq n$ and $1 \leq j \leq m$. We write a $A$ as 
$$
\begin{pmatrix} 
    a_{11} & a_{12} & \cdots & a_{1m} \\
    a_{21} & a_{22} & \cdots & a_{2m} \\
    \vdots & \vdots & \ddots & \vdots \\
    a_{n1} & a_{n2} & \cdots & a_{nm}
\end{pmatrix}
$$

Our convention is that reading left-to-right increases the second index while reading up-to-down increase the 
first index. (Other conventions are fine but we all need to pick one and stick to it. This is it.)

A matrix is *square* if $n = m$. The *diagonal* of $A$ is the set of where the two indices are equal, i.e. 
$a_{11}, a_{22}, \ldots, a_{dd}$ where $d = \operatorname{min}(m,n)$. 

We can extract lists of vectors from a matrix $A$ in (at least) two ways:
- The *set of columns vectors* of $A$ is the collection 
$$
\begin{pmatrix} 
    a_{11} \\
    a_{21} \\
    \vdots \\
    a_{n1}
\end{pmatrix} \ , \ 
\begin{pmatrix} 
    a_{12} \\
    a_{22} \\
    \vdots \\
    a_{n2}
\end{pmatrix} \ , \ \cdots \ , \ 
\begin{pmatrix} 
    a_{1m} \\
    a_{2m} \\
    \vdots \\
    a_{nm}
\end{pmatrix}
$$
Note that we get $m$ vectors of length $n$ in this fashion. Each vector comes from reading down a single 
column.

- The *set of row vectors* of $A$ is the collection 
$$
\begin{pmatrix} 
    a_{11} \\
    a_{12} \\
    \vdots \\
    a_{1m}
\end{pmatrix} \ , \ 
\begin{pmatrix} 
    a_{21} \\
    a_{22} \\
    \vdots \\
    a_{2m}
\end{pmatrix} \ , \ \cdots \ , \ 
\begin{pmatrix} 
    a_{n1} \\
    a_{n2} \\
    \vdots \\
    a_{nm}
\end{pmatrix}
$$
Note that we get $n$ vectors of length $m$ in this fashion. Each vector comes from reading across a single 
row of $A$. 

Here you might notice that the strange notational choice for 
[scalar multiplication of vectors]({% link notes/solving_linear_systems/vectors.md %}#multiplication-of-vectors) 
would yield a more natural 
way of extracting the rows 
$$
\begin{pmatrix} 
    a_{11} &
    a_{12} &
    \cdots &
    a_{1m}
\end{pmatrix} \ , \ 
\begin{pmatrix} 
    a_{21} &
    a_{22} &
    \cdots &
    a_{2m}
\end{pmatrix} \ , \ \cdots \ , \ 
\begin{pmatrix} 
    a_{n1} &
    a_{n2} &
    \cdots &
    a_{nm}
\end{pmatrix}
$$
It is natural to therefore think of both $n \times 1$ and $1 \times m$ matrices as being vectors since are both 
lists with a single index. 

In fact, there is a natural operation on matrices which exchanges row and column vectors. Given a matrix $A = (a_{ij})$, its 
*transpose* $A^t$ flips the two indices. More precisely, 
$$
A^t := 
\begin{pmatrix} 
    a_{11} & a_{21} & \cdots & a_{n1} \\
    a_{12} & a_{22} & \cdots & a_{n2} \\
    \vdots & \vdots & \ddots & \vdots \\
    a_{1m} & a_{2m} & \cdots & a_{mn}
\end{pmatrix}
$$

The notation might be seem subtle to you so let's see an example. Suppose 
$$
A = 
\begin{pmatrix}
    1 & 2 \\
    3 & 4 \\
    5 & 6
\end{pmatrix}
$$
Then the column vectors of $A$ are 
$$
\begin{pmatrix}
    1 \\
    3 \\ 
    5
\end{pmatrix} \ , \
\begin{pmatrix}
    2 \\
    4 \\ 
    6
\end{pmatrix}
$$
while the row vectors of $A$ are 
$$
\begin{pmatrix}
    1 \\
    2
\end{pmatrix} \ , \
\begin{pmatrix}
    3 \\
    4 
\end{pmatrix} \ , \
\begin{pmatrix}
    5 \\
    6 
\end{pmatrix}
$$

We can compute the transpose 
$$
\begin{pmatrix}
    1 & 2 \\
    3 & 4 \\
    5 & 6
\end{pmatrix}^t = 
\begin{pmatrix}
    1 & 3 & 5 \\
    2 & 4 & 6 
\end{pmatrix}
$$
The entries $1$ and $4$ on the diagonal don't move and everything else is reflected over it. 

## Addition of matrices

Addition of matrices works in the same way as for vectors: you add the entries (or components) individually with 
the **big caveat** that you can only add matrices of the same size. 
$$
\begin{pmatrix} 
    a_{11} & a_{12} & \cdots & a_{1m} \\
    a_{21} & a_{22} & \cdots & a_{2m} \\
    \vdots & \vdots & \ddots & \vdots \\
    a_{n1} & a_{n2} & \cdots & a_{nm}
\end{pmatrix} + 
\begin{pmatrix} 
    b_{11} & b_{12} & \cdots & b_{1m} \\
    b_{21} & b_{22} & \cdots & b_{2m} \\
    \vdots & \vdots & \ddots & \vdots \\
    b_{n1} & b_{n2} & \cdots & b_{nm} 
\end{pmatrix} = 
\begin{pmatrix} 
    a_{11} + b_{11} & a_{12} + b_{12} & \cdots & a_{1m} + b_{1m} \\
    a_{21} + b_{21} & a_{22} + b_{22} & \cdots & a_{2m} + b_{2m} \\
    \vdots & \vdots & \ddots & \vdots \\
    a_{n1} + b_{n1} & a_{n2} + b_{n2} & \cdots & a_{nm} + b_{nm}
\end{pmatrix}
$$

## Multiplication of matrices 

### Scalar multiplication 

Given a scalar $a$ and a matrix $B$, we can multiply them to yield a new matrix $aB$
$$ a 
\begin{pmatrix} 
    b_{11} & b_{12} & \cdots & b_{1m} \\
    b_{21} & b_{22} & \cdots & b_{2m} \\
    \vdots & \vdots & \ddots & \vdots \\
    b_{n1} & b_{n2} & \cdots & b_{nm}
\end{pmatrix} = 
\begin{pmatrix} 
    ab_{11} & ab_{12} & \cdots & ab_{1m} \\
    ab_{21} & ab_{22} & \cdots & ab_{2m} \\
    \vdots & \vdots & \ddots & \vdots \\
    ab_{n1} & ab_{n2} & \cdots & ab_{nm}
\end{pmatrix}
$$
Similar to [multiplication of a scalar and a vector]({% link notes/solving_linear_systems/vectors.md %}#scalar-multiplication) 
we scale each entry of $B$ by $a$. 

### Matrix multiplication 

We now arrive at a type of multiplication that might seem new and strange to some. Given an $A$ an $n \times m$ matrix 
and $B$ an $m \times k$ matrix, we can multiply them to yield $AB$ an $n \times k$ matrix. 

Let me repeat: **you can only multiply $A$ and $B$ if the number of columns of $A$ equals the number of rows of $B$**. 
An observant reader will notice that this is not a symmetric condition in general. A $2 \times 3$ multiplied by 
a $3 \times 1$ matrix is fine. But $3 \times 1$ times $2 \times 3$ is not.  

The formula for the $(i,j)$ entry in the product $AB$ is 
$$
    (AB)_{ij} := \sum_{s = 1}^m A_{is}B_{sj}
$$

You might recognize a similarity to the formula for 
[multiplication of vectors]({% link notes/solving_linear_systems/vectors.md %}#multiplication-of-vectors). 

Indeed, if $A$ is a $1 \times m$ matrix and $B$ is a $m \times 1$ matrix, then $AB$ is **exactly** the product of 
$A$ and $B$ considered as vectors. 

The general formula can be understand this way: the $(i,j)$ entry of $AB$ is the product of the $i$-th row vector of $A$ 
and the $j$-th column vector of $B$. 

Let us see this in an example. Take 
$$
A = 
\begin{pmatrix}
    1 & 2 \\
    3 & 4 \\
    5 & 6
\end{pmatrix} \ , \
B = 
\begin{pmatrix} 
    0 & -1 & -2 & -3 \\
    -4 & -5 & -6 & -7 
\end{pmatrix} 
$$
Then $AB$ is well-defined but $BA$ is not. We break $A$ into its row vectors 
$$
 \begin{pmatrix}
    1 & 2 
 \end{pmatrix} \ , \ 
 \begin{pmatrix}
    3 & 4
 \end{pmatrix} \ , \
 \begin{pmatrix}
    5 & 6
\end{pmatrix}
$$
and $B$ into its column vectors 
$$
\begin{pmatrix} 
    0 \\
    -4 
\end{pmatrix} \ , \
\begin{pmatrix} 
    -1 \\
    -5 
\end{pmatrix} \ , \
\begin{pmatrix} 
    -2 \\
    -6 
\end{pmatrix} \ , \
\begin{pmatrix} 
    -3 \\
    -7 
\end{pmatrix}
$$
Now we compute each product of a row vector of $A$ with a column vector of $B$. There are 12. 
<details>
	<summary>Click to see the calculations</summary>
	$$ 
\begin{pmatrix}
    1 & 2 
\end{pmatrix} 
\begin{pmatrix} 
    0 \\
    -4 
\end{pmatrix} = -8 \\
 {} \\
\begin{pmatrix}
    1 & 2 
\end{pmatrix} 
\begin{pmatrix} 
    -1 \\
    -5 
\end{pmatrix} = -11 \\
 {} \\
\begin{pmatrix}
    1 & 2 
\end{pmatrix} 
\begin{pmatrix} 
    -2 \\
    -6 
\end{pmatrix} = -14 \\
 {} \\
\begin{pmatrix}
    1 & 2 
\end{pmatrix} 
\begin{pmatrix} 
    -3 \\
    -7 
\end{pmatrix} = -17 \\
 {} \\
\begin{pmatrix}
    3 & 4 
\end{pmatrix} 
\begin{pmatrix} 
    0 \\
    -4 
\end{pmatrix} = -16 \\
 {} \\
\begin{pmatrix}
    3 & 4 
\end{pmatrix} 
\begin{pmatrix} 
    -1 \\
    -5 
\end{pmatrix} = -23 \\
 {} \\
\begin{pmatrix}
    3 & 4 
\end{pmatrix} 
\begin{pmatrix} 
    -2 \\
    -6 
\end{pmatrix} = -30 \\
 {} \\
\begin{pmatrix}
    3 & 4 
\end{pmatrix} 
\begin{pmatrix} 
    -3 \\
    -7 
\end{pmatrix} = -27 \\
 {} \\
 \begin{pmatrix}
    5 & 6 
\end{pmatrix} 
\begin{pmatrix} 
    0 \\
    -4 
\end{pmatrix} = -24 \\
 {} \\
\begin{pmatrix}
    5 & 6 
\end{pmatrix} 
\begin{pmatrix} 
    -1 \\
    -5 
\end{pmatrix} = -35 \\
 {} \\
\begin{pmatrix}
    5 & 6 
\end{pmatrix} 
\begin{pmatrix} 
    -2 \\
    -6 
\end{pmatrix} = -46 \\
 {} \\
\begin{pmatrix}
    5 & 6 
\end{pmatrix} 
\begin{pmatrix} 
    -3 \\
    -7 
\end{pmatrix} = -57
$$
</details>
The product is 
$$
    AB =
    \begin{pmatrix}
        -8 & -11 & -14 & -17 \\
        -16 & -23 & -30 & -37 \\
        -24 & -35 & -46 & -47
    \end{pmatrix} 
$$

Next we turn to [translating systems of linear equations into matrix equations]({% link notes/solving_linear_systems/matrix_equations.md %})