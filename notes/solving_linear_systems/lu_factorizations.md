---
layout: page
title: LU Factorizations 
nav_order: 12
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
work_in_progress: true 
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## LU Factorizations

One hallmark of good mathematics is that the tools you create to solve the problem end 
up being very useful to handle other issues. 

Gaussian Elimination is very much a good tool. We will see here how to streamline 
the [algorithm for producing row echelon systems]({% link notes/solving_linear_systems/gaussian_elimination.md%}) 
to produce a useful factorization of a general matrix. 

Being able to write a matrix $A$ as a product of two matrices $BC$ where we know 
something about the forms $B$ and $C$ can be a very useful piece of information. 
Such a decomposition is a called a _factorization_ of $A$. 

We are interested in factorizations where $B$ is a square matrix with 
- $1$'s along the diagonal 
- only $0$'s above the diagonal. 

Any matrix satisfying the second condition is called _lower triangular_ and to 
emphasize this notation we will usually write $L$ to mean a lower diagonal 
matrix. 

For $C$, we want to know that 
- all entries below the diagonal are $0$.

This is the tranpose condition of being lower triangular and we call it 
_upper triangular_ and use $U$ to denote matrices that are upper triangular. 

Remember the diagonal of a matrix $A$ are the entries with equal row and column 
indices, i.e. $a_{ii}$ for $1 \leq i \leq \operatorname{min}(m,n)$. The diagonal 
can look a little odd for matrices far from square. For example, 
$$
    A = 
    \begin{pmatrix} 
        5 & -1 & -2 & -3 & -4 
    \end{pmatrix}
$$
only has a single diagonal entry, $5$. This $A$ is trivially upper triangular but 
is very far from lower diagonal. 

<!-- ### Theorem: LUP Factorization 

Given a $m \times n$ matrix $A$, there exists 
- an $m \times m$ lower triangular matrix $L$ with $L_{ii} = 1$ for all $1 \leq i \leq m$ 
- an $m \times n$ upper triangular matrix $U$ such that and 
- an $n \times n$ permutation matrix $P$ such that
$$
    A = LUP.
$$

The best part of this theorem is that we can prove it using an algorithm that is 
a slight modification, in fact a simplication, of 
[Gaussian Elimination]({% link notes/solving_linear_systems/gaussian_elimination.md %}). 

To illustrate the idea, first notice that any matrix in row echelon form is 
automatically upper triangular. Indeed, if $A$ is not $0$, then the first row has to 
be nonzero. Let $a_{1p}$ be the pivot in $\mathbf{R}_1$. From the definition 
row echelon form, we know that $a_{iq} = 0$ for $i > 1$ and $q \leq p$. Thus, the 
pivot for $\mathbf{R}_2$ by at most $a_{2 (p+1)$, the entry down one and to the right one. 
(It doesn't have to be the pivot, of course, but that is smallest column index 
it could possibly have.) 

Continuing down the rows, we see that all entries below the (off-)diagonal starting at 
$a_{1p}$ must vanish so $A$ must be upper triangular. 

### From row operations to factorizations

Recall that each step in Gaussian Elimination can be expressed as multiplication with 
a particular type of $m \times m$ matrix: 
- Scaling via $S(i,c)$ for $c \neq 0$
- Permutations via $P(i,j)$ 
- Linear combination via $L(i,j,c)$ for $i \neq j$

Thus if $A^\prime$ denotes the next step in Gaussian elimination we already know that 
$$
    A^\prime = E A
$$
for $E$ one of these matrices. 

We also know that we can undo multiplication by each of these matrices:
- $S(i,c) S(i,1/c) = I$ from [Homework 2]({% link homework/2.md %})
- $P(i,j) P(j,i) = I$ from [Homework 1]({% link homework/1.md %})
- $L(i,j,c) L(i,j,-c) = I$ from [Worksheet 2]({% link worksheets/2.md %})

Let's introduce a notion to capture "undo-ability". We say a matrix $A$ is _invertible_ 
if there is another matrix $B$ such that 
$$
    A B = I = B A.
$$
It turns out that any such $B$ is automatically unique. Therefore, we use the notation 
$A^{-1}$ to represent the matrix that satisfies 
$$
    A A^{-1} = I = A^{-1} A 
$$  
if it exists. We will delve more deepy into the consequences of 
[invertibility]({% link notes/solving_linear_systems/invertibility.md%}) momentarily. 

Rewriting the previous statements in the new notation says
- $S(1,c)^{-1} = S(1,1/c)$ if $c \neq 0$
- $P(i,j)^{-1} = P(i,j)$ and 
- $L(i,j,c)^{-1} = L(i,j,-c)$ if $i \neq j$

If $A^\prime = EA$, we can multiply by $E^{-1}$ on the left to get 
$$
    E^{-1} A^\prime = E^{-1} E A = I A = A
$$
a factorization of $A$ in terms of $A^\prime$ and $E^{-1}$. 

For what $E$ is $E^{-1}$ lower triangular? 

$S(1,c)$ is diagonal so it is both lower and upper triangular at the same time. 

$P(i,j)$ is never upper or lower triangular for $i \neq j$. 

$L(i,j,c)$ is lower triangular if $i > j$. If $i < j$, it is upper triangular. For example, 
$$
    L(1,3,c) =
    \begin{pmatrix}
        1 & 0 & c \\
        0 & 1 & 0 \\
        0 & 0 & 1
    \end{pmatrix}
$$

We want use just $L(i,j,c)$ with $i < j$ to reduce our matrix $A$ to an upper triangular matrix. 

### An algorithm for LU factorization 

We will keep a running list of matrices starting at the empty list $\ell = []$. We start with a 
$m \times n$ matrix $A_0$. Set $A = A_0$. 

**Step 1**

Reading left to right, find the first column of $A$ with both a pivot $a_{ij}$ with $i < j$ 
and a nonzero entry $a_{sj}$ with $s > i$. 

If there is none, go to step 2. 

Otherwise, multiply $A$ by $L(s,i,-a_{sj}/a_{ij})$ to get 
$$
    A^\prime = L(s,i,-a_{sj}/a_{ij}) A
$$
Add $L(s,i,-a_{sj}/a_{ij})$ to the end of $\ell$. Replace $A$ by $A^\prime$ and return to the start of 
step 1. 

**Step 2** 

The two outputs of step 2 are $A$ and $\ell$. Take the product over all the matrices in our list 
$$
    L := \prod_{l \in \ell} L(i_l,j_l,-c_l)
$$
and set 
$$
    U := A. 
$$

Before trying to reason about the algorithm, let us see it at work in an example. Take 
$$
    A_0 = 
    \begin{pmatrix}
        1 & -2 & 0 \\
        2 & 3 & -1 \\
        0 & -1 & 0 
    \end{pmatrix}
$$
We identify $a_{21}$ as the first element we want to eliminate. Then, we have 
$$
    \begin{pmatrix}
        1 & 0 & 0 \\
        -2 & 1 & 0 \\
        0 & 0 & 1 
    \end{pmatrix} 
    \begin{pmatrix}
        1 & -2 & 0 \\
        2 & 3 & -1 \\
        0 & -1 & 0 
    \end{pmatrix} = 
    \begin{pmatrix}
        1 & -2 & 0 \\
        0 & 7 & -1 \\
        0 & -1 & 0 
    \end{pmatrix}
$$
Now we repeat with  -->
