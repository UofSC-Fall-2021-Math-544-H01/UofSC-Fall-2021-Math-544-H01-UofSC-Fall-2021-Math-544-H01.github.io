---
layout: page
title: LU Factorizations 
nav_order: 13
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

### Definitions

An _LU factorization_ of a $m \times n$ matrix $A$ is a lower triangular $m \times m$ 
matrix $L$ with $L_{ii} = 1$ for each $i$ and an upper triangular $m \times n$ matrix 
$U$ where 
$$
    A = LU. 
$$  

_If it exists_, an LU factorization is very useful information about the matrix $A$.

### LU factorizations = Gaussian Elimination without permutations

To see why, we revisit the 
[Gaussian Elimination algorithm]({% link notes/solving_linear_systems/gaussian_elimination.md %}) 
with an assumption about how it works on an $A$. 

Assume that each time we pass through Step 1 in the Gaussian Elimination Algorithm, we 
actually don't need to perform any row exchanges. 

Each iteration of Step 2 is multiplication by $L(i,j,c)$ for $i > j$ since we are always taking the 
smallest row index, with pivots in a fixed column, and using multiples of it to eliminate the 
other entries in rows below it. 

Thus, if $A^\prime$ is obtained from $A$ in Step, we have 
$$
    A^\prime = L(i,j,c)A 
$$
for $i > j$. 

At the end of Gaussian Elimination, $A^\prime$ is upper triangular since it is in row echelon form. 

Taking all the steps together, we get 
$$
    U = \prod_{t=1}^N L(i_t,j_t,c_t) A
$$
We can cancel off the product by using its inverse. We remember the inverse of product reverses it ordering
$$
    \left(\prod_{t=1}^N L(i_t,j_t,c_t) \right)^{-1} = \prod_{t=N}^1 L(i_t,j_t,c_t)^{-1} = \prod_{t=N}^1 L(i_t,j_t,-c_t)
$$
The product of lower triangular matrices with $1$'s on the diagonal is another lower triangular matrix with $1$'s 
on the diagonal.

Thus, if we set 
$$
    L = \prod_{t=N}^1 L(i_t,j_t,c_t)^{-1}
$$
we get a LU factorization of $A$
$$
    LU = A. 
$$  

Let's do an example. 
$$
    A = \begin{pmatrix}
            1 & 2 & 3 & 1 \\ 
            2 & 2 & 2 & 2 \\
            2 & 0 & -1 & 3 
        \end{pmatrix}
$$
<details>
<summary>
Expand for computations. 
</summary>
We need to keep track of each row subtraction as we do Gaussian elimination. 

First we take $\mathbf{R}_2 - 2\mathbf{R}_1$ and then $\mathbf{R}_3 - 2\mathbf{R}_1$ to get 
$$
    \begin{pmatrix}
        1 & 2 & 3 & 1 \\ 
        0 & -2 & -4 & 0 \\
        0 & -4 & -7 & 1 
    \end{pmatrix}
$$
and our list of row operations so far is 
$$
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        0 & 1 & 0 \\
        -2 & 0 & 1  
    \end{pmatrix} \ , \ 
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        -2 & 1 & 0 \\
        0 & 0 & 1  
    \end{pmatrix}
$$

Next we take $\mathbf{R}_3 - 2\mathbf{R}_2$ to get 
$$
    \begin{pmatrix}
        1 & 2 & 3 & 1 \\ 
        0 & -2 & -4 & 0 \\
        0 & 0 & 1 & 1 
    \end{pmatrix}
$$
which is in row echelon form. Our list of matrices now reads 
$$
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        0 & 1 & 0 \\
        0 & -2 & 1  
    \end{pmatrix} \ , \ 
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        0 & 1 & 0 \\
        -2 & 0 & 1  
    \end{pmatrix} \ , \ 
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        -2 & 1 & 0 \\
        0 & 0 & 1  
    \end{pmatrix}
$$

To get our $L$ we take the product of the inverses in the inverted order
$$
    L = \begin{pmatrix}
        1 & 0 & 0 \\ 
        -2 & 1 & 0 \\
        0 & 0 & 1  
    \end{pmatrix}^{-1} 
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        0 & 1 & 0 \\
        -2 & 0 & 1  
    \end{pmatrix}^{-1}
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        0 & 1 & 0 \\
        0 & -2 & 1  
    \end{pmatrix}^{-1} = \\
    {} \\
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        2 & 1 & 0 \\
        0 & 0 & 1  
    \end{pmatrix} 
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        0 & 1 & 0 \\
        2 & 0 & 1  
    \end{pmatrix}
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        0 & 1 & 0 \\
        0 & 2 & 1  
    \end{pmatrix} = 
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        2 & 1 & 0 \\
        2 & 2 & 1  
    \end{pmatrix}
$$
</details>

Our LU factorization is 
$$
    \begin{pmatrix}
        1 & 2 & 3 & 1 \\ 
        2 & 2 & 2 & 2 \\
        2 & 0 & -1 & 3 
    \end{pmatrix}
    =
    \begin{pmatrix}
        1 & 0 & 0 \\ 
        2 & 1 & 0 \\
        2 & 2 & 1  
    \end{pmatrix}
    \begin{pmatrix}
        1 & 2 & 3 & 1 \\ 
        0 & -2 & -4 & 0 \\
        0 & 0 & 1 & 1 
    \end{pmatrix}
$$

### LU factorization with partial pivoting

The assumption that we don't need to use any row exchanges is not a vacuous one. Take for example
$$
    \begin{pmatrix}
        0 & 1 \\
        1 & 0 
    \end{pmatrix}
$$
There is no way to write it as a product $LU$. 

We will need row exchanges at some point for this example and in general. 

A more general factorization always exists. Recall that we call matrices $P(i,j)$ 
permutation matrices. In fact, they are special examples of a more general notion of 
a permutation matrix. 

A _permutation matrix_ is a square matrix with exactly one nonzero entry in each row 
and in each column. That one nonzero entry is required to be a $1$. Note $P(i,j)$ is 
indeed an example of such matrix. 

Such matrices are called permutation matrices because you can obtain them from $I$ by 
shuffling the rows vectors (or shuffling the column vectors). 

An _LU factorization with partial pivoting_ of 
a $m \times n$ matrix $A$ is a $m \times m$ permutation matrix $P$, 
a lower triangular $m \times m$ matrix $L$ with $1$'s along the diagonal, and an $m \times n$
upper triangular matrix $U$ such that 
$$
    PA = LU.
$$

**Theorem**. Any matrix has an LU factorization with partial pivoting. 

**Proof (Sketch)**. We won't provide the full details at the moment. 

The essential idea is that, instead of the existing flow in the 
[Gaussian Elimination algorithm]({% link notes/solving_linear_systems/gaussian_elimination.md %}) 
where we return to Step 1 to permute rows after each step 2, we perform a well-chosen 
permutation $P$ on the rows of $A$ to start. 

After this permutation, we are able to run Gaussian Elimination without any more 
row permutations to get $PA = LU$. 