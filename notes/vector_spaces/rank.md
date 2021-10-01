---
layout: page
title: Rank and nullity
nav_order: 7
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Rank and Nullity 

The dimension of a vector space is its most important characteristic. Given two matrices, we have two 
subspaces of great interest: the null space $\mathcal Z(A)$ and the range $\mathcal R(A)$. So 
we create some language to speak about their dimensions. 

**Definition**. The _rank_ of $A$ is the dimension of $\mathcal R(A)$.

The _nullity_ of $A$ is the dimension of $\mathcal Z(A)$. 

Sometimes the dimension of $\mathcal R(A)$ is called the _column rank_ of $A$ since the range 
is the span of the column vectors. There is also the _row rank_ which is the dimension of the 
span of the rows of $A$. 

We can restate previous results using this new language. 

**Proposition**. The rank of $A$ is the number of pivots of $A^T$ in row echelon form. 

This is just the 
[second example]({% link notes/vector_spaces/bases.md %}#examples)
from the previous section.

**Proposition**. The nullity of $A$ is the number free variables of $A$ in row echelon form. 

This is just the 
[first example]({% link notes/vector_spaces/bases.md %}#examples)
from the previous section.

### Facts about ranks and nullity

The rank and nullity of a matrix are not independent numbers. In fact, if you know one, 
you can quickly determine the other.

Before we give a the Rank Nullity Theorem, we want to discuss the effect of row 
operations on the range of $A$. 

We 
[know]({% link notes/vector_spaces/linear_independence.md %}#linear-dependence-and-matrices)
that row operations don't change the the row space, ie $\mathcal R(A^T)$. 

This is definitely not the case for the columns. Take the simple example of 
$$
    \begin{pmatrix}
        1 \\ 0 
    \end{pmatrix}
$$
whose span is 
$$
    \left\lbrace \begin{pmatrix} x \\ 0 \end{pmatrix} \mid x \in k \right\rbrace
$$
If we swap the first and second row, then we have the matrix 
$$
    \begin{pmatrix}
        0 \\ 1 
    \end{pmatrix}
$$
whose span is 
$$
    \left\lbrace \begin{pmatrix} 0 \\ x \end{pmatrix} \mid x \in k \right\rbrace
$$
These are not the same. But _they do have the same dimension_. More generally, 
we have the following statement. 

**Proposition**. Let $W \subseteq k^m$ be a subspace and let $A$ be an 
$m \times m$ matrix. Then,
$$
    \dim A(W) \leq \dim W
$$
where
$$
    A(W) := \lbrace v \in k^m \mid v = Aw \text{ for } w \in W \rbrace.
$$

{% include beginproof.html %}
Pick a basis $w_1,\ldots,w_d$. Let $v \in A(W)$. Then by definition, we know that there is 
some $w \in W$ with $v = Aw$. Since we have a basis, we can write 
$$
    w = c_1w_1 + c_2w_2 + \cdots + c_dw_d
$$
If we apply $A$ to each side, we get 
$$
    v = Aw = A\left( \sum c_i w_i \right) = \sum c_i A(w_i)
$$
This says that $v$ lies in the span of $Aw_1,\ldots,Aw_d$. From the 
[final proposition]({% link notes/vector_spaces/linear_independence.md %}#consequences), we 
know that a subset of $\lbrace Aw_1,\ldots,Aw_d \rbrace$ forms a basis of $A(W)$. 
Thus, 
$$
    \dim A(W) \leq \dim W
$$
{% include endproof.html %}

**Corollary**. If $A$ and $B$ are related by a sequence of elementary row operations, then 
$$
    \operatorname{rank} A = \operatorname{rank} B
$$
In particular, the rank of $A$ and the rank of any row echelon form of $A$ are equal. 

{% include beginproof.html %}
If $A$ and $B$ are related by a sequence of row operations, then $CA = B$ for an 
invertible matrix $C$ where $C$ is a product of $S(i,c), P(i,j),$ and $L(i,j,c)$ 
corresponding to the row operations performed. 

Thus, applying the previous proposition, we know that 
$$
    \dim \mathcal R(B) \leq \dim \mathcal R(A)
$$

Since $C$ is invertible, we also know that $A = C^{-1}B$ so 
$$
    \dim \mathcal R(A) \leq \dim \mathcal R(B)
$$
Combining these we get 
$$
    \dim \mathcal R(A) = \dim \mathcal R(B)
$$
as desired. 
{% include endproof.html %}

**Proposition**. For any matrix $A$, 
$$
    \operatorname{rank} A = \operatorname{rank} A^T
$$

{% include beginproof.html %}
From the previous corollary, we know that both $\operatorname{rank} A$ does 
not change under Gaussian Elimination. We also already know that 
$\operatorname{rank} A^T$ does not change under Gaussian elimination. 

Thus, we can assume that $A$ is in reduced row echelon form. We have 
[seen]({% link notes/vector_spaces/linear_independence.md %}#linear-dependence-and-matrices) 
that the rows of any matrix in row echelon form are linearly independent. Thus, 
the rank of $A^T$ is just the number of nonzero rows of $A$. 

Let's call the number of nonzero rows $r$. 

The columns containing the pivots form a basis the range of $A$. Notice that 
the sub-matrix of $A$ consisting of the rows and the columns is a copy 
of the identity of size $r \times r$. 

To have a relation amongst the columns, we need a relation amongst the columns of 
this submatrix which must be the trivial relation. 

And, we can write any other column as a linear combination of the columns of 
the identity matrix. Hence, these columns span and they form a basis. 

Thus the rank of $A$ equals the number of pivots. 

Since the number pivots is equal to the number of nonzero rows, we have
$$
    \operatorname{rank} A = \operatorname{rank} A^T
$$
{% include endproof.html %}

### Rank Nullity Theorem 

**Theorem**. Let $A$ be a $m \times n$ matrix. Then, 
$$
    \operatorname{rank}(A) + \operatorname{nullity}(A) = n. 
$$

{% include beginproof.html %}
An rather obvious observation is that 
$$
    n = \# \text{ free variables } + \# \text{ bound variables }
$$
and we know that 
$$
    \operatorname{nullity} A = \# \text{ free variables }
$$
The number of bound variables is the number of pivots in row echelon form of $A$. 

Now, the number of pivots in the row echelon form of $A$ is the rank of $A^T$. 
And we just saw that the rank of $A$ is equal to the rank of $A^T$. 
{% include endproof.html %}

### Examples

As an application of the Rank Nullity Theorem, we just need to convert 
$A$ to row echelon form and count the number of free variables and 
the number of pivots. 

For example, if we take 
$$
    A =
    \begin{pmatrix}
        7 & 5 & 12 & 0 & 3 \\
        9 & 34 & -13 & 1 & 4 \\
        3 & -3 & 2 & 10 & 5 \\
        1 & 4 & 3 & -1 & 2 
    \end{pmatrix}
$$
its reduced row echelon form is 
$$
    A = 
    \begin{pmatrix}
        1 & 0&  0&  0 & -221/263 \\
        0&  1&  0&  0 & 136/263 \\
        0&  0&  1&  0 & 138/263 \\
        0&  0&  0&  1  & 211/263
    \end{pmatrix} 
$$
so we see that its rank is $4$ and its nullity is $1$. Their sum is $5$. 