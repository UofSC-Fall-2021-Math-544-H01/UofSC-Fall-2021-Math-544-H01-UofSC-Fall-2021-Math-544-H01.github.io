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

A *matrix* $A$ of size $n \times m$ is a list of numbers $a_{ij}$ indexed by pairs $(i,j)$ for $1 \leq i \leq n$ 
and $1 \leq j \leq m$. We write a $A$ as 
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

A matrix is *square* if $n = m$. 

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
[scalar multiplication of vectors]({% link notes/solving_linear_systems/vectors.md %}/#multiplication-of-vectors) 
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
Similar to [scalar multiplication of vectors]({% link notes/solving_linear_systems/vectors.md %}/#scalar-multiplication) 
we scale each entry of $B$ by $a$. 
