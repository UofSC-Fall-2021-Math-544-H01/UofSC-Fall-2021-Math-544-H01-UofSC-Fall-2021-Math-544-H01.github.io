---
layout: page
title: Vectors
nav_order: 3
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
---

## Vectors 

A *vector* is just a list of numbers. Given a list $b_1,\ldots,b_n$ we usually write a vector vertically 
$$
\begin{pmatrix} 
    b_1 \\
    b_2 \\
    \vdots \\
    b_m 
\end{pmatrix}
$$
as in a single column. We often write $\mathbf{v}$ to denote a vector. The entries of $\mathbf{v}$ are 
called the *components* of $\mathbf{v}$. 

The *length* of the $\mathbf{v}$ is number of entries in $\mathbf{v}$. 

A *scalar* is another name for a vector of length 1. We typically omit the parentheses when writing a scalar. 

We have some basic, but useful, operations we can do with vectors. 

### Vector addition

If $\mathbf{v}$ and $\mathbf{w}$ are vectors of the same length, we can add them. We do this by adding their 
components. More precisely, if 
$$
\mathbf{v} = 
\begin{pmatrix} 
    v_1 \\
    v_2 \\
    \vdots \\
    v_m 
\end{pmatrix} \ , \ 
\mathbf{w} = 
\begin{pmatrix} 
    w_1 \\
    w_2 \\
    \vdots \\
    w_m 
\end{pmatrix}
$$
then 
$$
\mathbf{v} + \mathbf{w} := 
\begin{pmatrix} 
    v_1 + w_1 \\
    v_2 + w_2 \\
    \vdots \\
    v_m + w_m 
\end{pmatrix}
$$

For example, 
$$
\begin{pmatrix} 
    -1 \\
    4 \\
    3 
\end{pmatrix} +
\begin{pmatrix} 
    5 \\
    -6 \\
    0 
\end{pmatrix} = 
\begin{pmatrix} 
    4 \\
    -2 \\
    3
\end{pmatrix} 
$$

**Note**: We cannot add vectors of different lengths. 

## Vectors and multiplication

There are standard ways to multiply vectors but, like with addition, there are some restrictions on the operations. 

### Scalar multiplication 

Given a scalar $a$ and a vector $\mathbf{v}$ we get another vector $a \mathbf{v}$ as 
$$
a 
\begin{pmatrix} 
    v_1 \\
    v_2 \\
    \vdots \\
    v_m 
\end{pmatrix} = 
\begin{pmatrix} 
    av_1 \\
    av_2 \\
    \vdots \\
    av_m 
\end{pmatrix}
$$
In other words, we scale each component of $\mathbf{v}$ by $a$. For example, 
$$ 3 
\begin{pmatrix} 
    -1 \\
    2 \\
    0 
\end{pmatrix} = 
\begin{pmatrix} 
    -3 \\
    -6 \\
    0
\end{pmatrix} 
$$

### Multiplication of vectors

Given two vectors $\mathbf{v}$ and $\mathbf{w}$ of the same length, we can multiply them and return a scalar. 
When we write the formula, we do something a little strange. We turn the first vector into a row, in the 
notation. 

The formula is 
$$
 \begin{pmatrix} v_1 & v_2 & \cdots & v_m \end{pmatrix} 
 \begin{pmatrix} 
    w_1 \\
    w_2 \\
    \vdots \\
    w_m 
 \end{pmatrix} 
  := \sum_{i=1}^m v_i w_i.
$$

For example, 
<center>
$
 \begin{pmatrix} 1 & 2 & 3 & 4 \end{pmatrix} 
 \begin{pmatrix} 
    -1 \\
    0 \\
    1 \\
    2 
 \end{pmatrix} 
  = 1(-1) + 2(0) + 3(1) + 4(2) = 10.
$
</center>

Next, we look at [matrices]({% link notes/solving_linear_systems/matrices.md %}).