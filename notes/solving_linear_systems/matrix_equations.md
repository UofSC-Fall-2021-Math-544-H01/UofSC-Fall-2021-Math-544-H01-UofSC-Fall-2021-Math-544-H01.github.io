---
layout: page
title: Matrix Equations
nav_order: 5
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
---

## From systems of linear equations to matrix equations 

Let's start with a system of linear equations 
$$
    a_{11} x_1 + a_{12}x_2 + \cdots a_{1m} x_m = b_1 \\
    a_{21} x_1 + a_{22}x_2 + \cdots a_{2m} x_m = b_2 \\
    \vdots \\
    a_{n1} x_1 + a_{n2}x_2 + \cdots a_{nm} x_m = b_n \\
$$

If we set 
$$
    A = 
    \begin{pmatrix} 
    a_{11} & a_{12} & \cdots & a_{1m} \\
    a_{21} & a_{22} & \cdots & a_{2m} \\
    \vdots & \vdots & \ddots & \vdots \\
    a_{n1} & a_{n2} & \cdots & a_{nm}
    \end{pmatrix} \ , \ 
    \mathbf{x} = 
    \begin{pmatrix} 
    x_1 \\ 
    x_2 \\
    \vdots \\ 
    x_m 
    \end{pmatrix} \ , \
    \mathbf{b} = 
    \begin{pmatrix} 
    b_1 \\ 
    b_2 \\
    \vdots \\ 
    b_n 
    \end{pmatrix}
$$
then the system of can be captured using the simple matrix equation 
$$
    A \mathbf{x} = \mathbf{b}. 
$$

Similarly, we can reverse the direction. Writing out $A \mathbf{x} = \mathbf{b}$ explicitly 
will yield the original system of linear equations. Thus, we lose no information when using 
the matrix language. 

### Augmented matrices 

An extended notation for matrix equations will be useful, particularly for solving linear systems. Given 
a matrix equation $A \mathbf{x} = \mathbf{b}$, the *augmented matrix* is denoted 
$$
\begin{pmatrix}
    a_{11} & a_{12} & \cdots & a_{1m} &\bigg| & b_1 \\
    a_{21} & a_{22} & \cdots & a_{2m} &\bigg| & b_2 \\
    \vdots & \vdots & \ddots & \vdots &\bigg| & \vdots \\
    a_{n1} & a_{n2} & \cdots & a_{nm} &\bigg| & b_n 
\end{pmatrix}
$$

Our next task is to understand how we can enhance our understanding of solutions of linear systems 
by using matrices. We will study which [operations]({% link notes/solving_linear_systems/row_operations.md %}) on (augmented) matrices can simplify the 
matrix into a [canonical form]({% link notes/solving_linear_systems/row_echelon_form.md %})
without losing information about the solution set of the linear system. 