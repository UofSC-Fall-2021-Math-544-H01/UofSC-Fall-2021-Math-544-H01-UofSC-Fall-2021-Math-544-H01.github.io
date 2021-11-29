---
layout: page
title: Jordan Canonical Form
nav_order: 13
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: true
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Jordan Canonical Form 

We have seen that not all matrices can be diagonalized, or 
equivalently there is not always a basis for $k^n$ consisting of 
eigenvectors of the matrix. 

So, how far off are we from diagonalization? Can any $n \times n$ 
matrix $A$ be brought to a related form by replacing $A$ with 
$S^{-1} A S$? 

The answer is yes, over $\mathbb{C}$. 

**Definition**. A _Jordan block_ matrix J_n(\lambda) is a 
$n \times n$ matrix with 
a single value, $\lambda$, along the diagonal and with $1$'s just above 
the diagonal. Precisely, 
$$
	J_n(\lambda)_{ij} = 
		\begin{cases} 
			\lambda & i = j \\
			1 & i + 1 = j \\
			0 & \text{otherwise} 
		\end{cases}
$$

For example, you saw a $3 \times 3$ Jordan block on [Problem 2 from 
Worksheet 27]({% link worksheets/27.md %}) and here is another 
example
$$
J_4(0) = 
\begin{pmatrix}
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 0 & 0 
\end{pmatrix}
$$
which has $\lambda = 0$. 

We say that $A$ and $B$ are _similar_ if there is some invertible $S$ 
with $S^{-1} A S = B$. 

**Theorem** (Jordan Canonical Form). Let $A$ be a $n \times n$ matrix 
over $\mathbb{C}$. Then $A$ is similar to unique a block diagonal matrix 
where all the blocks are Jordan blocks. 

The Jordan block matrix in the theorem is called the _Jordan 
canonical form_ of $A$. 

It is important to know that this result is not true over $\mathbb{R}$. 

Note that a matrix in Jordan Canonical Form is in particular 
upper triangular - thus it is simple to read off the eigenvalues. 

One can also read off the eigenspaces. 

**Lemma**. Each $J_n(\lambda)$ has a one-dimensional $\lambda$-
eigenspace. 

{% include beginproof.html %}
If 
$$
J_n(\lambda) v = \lambda v 
$$
then we have 
$$
\begin{pmatrix}
0 & 1 & 0 & \cdots & 0 \\
0 & 0 & 1 & \cdots & 0 \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
0 & 0 & 0 & \cdots & 1 \\
0 & 0 & 0 & \cdots & 0 
\end{pmatrix}
\begin{pmatrix} 
v_1 \\ v_2 \\ \vdots \\ v_{n-1} \\ v_n 
\end{pmatrix} = 
\begin{pmatrix}
v_2 \\ v_3 \\ \vdots \\ v_n \\ 0
\end{pmatrix} = 
\begin{pmatrix}
0 \\ 0 \\ \vdots \\ 0 \\ 0 
\end{pmatrix}
$$
Thus, the eigenspace is 
$$
\left\lbrace \begin{pmatrix} x \\ 0 \\ \cdots \\ 0 \\ 0 \end{pmatrix} 
\mid x \in k \right\rbrace 
$$
which is one-dimensional. 
{% include endproof.html %}

**Corollary**. The sum of the dimensions of the eigenspaces is 
equal to the number of Jordan blocks in Jordan Canonical Form. 
Consequently, the $A$ is diagonalizable over $\mathbb{C}$ if 
and only if all Jordan blocks are $1 \times 1$ in size. 

In the other direction, the dimensions of the eigenspaces is 
not enough to recover the Jordan Canonical Form, though it does 
limit the possibility strongly. 

**Example**. Note that both 
$$
\begin{pmatrix}
-1 & 0 & 0 & 0 \\
0 & -1 & 1 & 0 \\
0 & 0 & -1 & 1 \\
0 & 0 & 0 & -1
\end{pmatrix} 
$$
and 
$$
\begin{pmatrix}
-1 & 1 & 0 & 0 \\
0 & -1 & 0 & 0 \\
0 & 0 & -1 & 1 \\
0 & 0 & 0 & -1 
\end{pmatrix}
$$
have a two-dimensional $(-1)$-eigenspaces and in Jordan Canonical 
Form but are not equal. 