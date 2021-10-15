---
layout: page
title: QR factorizations
nav_order: 10
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## QR factorizations

Recall that each elementary row operation in 
[Gaussian Elimination]({% link notes/solving_linear_systems/gaussian_elimination.md %})
could be interpreted as multiplication by a particular matrix. When thinking 
this way, you realize you are actually factoring a matrix when 
running Gaussian Elimination. This realization results in the 
[LU factorizations]({% link notes/solving_linear_systems/lu_factorizations.md %}) 
with pivoting. 

Similarly, we can view 
[Gram Schmidt]({% link notes/vector_spaces/gram_schmidt.md %}) as a factorization, 
called a _QR factorization_. 

First we notice that we can unfold the recursive definition given for Gram-Schmidt 
to write:
$$
    \begin{aligned}
        v_1 & = \langle v_1, w_1 \rangle w_1 \\
        v_2 & = \langle v_2, w_2 \rangle w_2 + \langle v_2, w_1 \rangle w_1 \\
        v_3 & = \langle v_3, w_3 \rangle w_3 + \langle v_3, w_2 \rangle w_2 + \langle v_3,w_1 \rangle w_1 \\
        & \vdots \\
        v_d & = \langle v_d, w_d \rangle w_d + \langle v_d, w_{d-1} \rangle w_{d-1} + \cdots + \langle v_d, w_1 \rangle w_1 
    \end{aligned}
$$

We can combine the $u_i$ as columns of a single matrix $Q$ and we let $R$ be the matrix 
with 
$$
    R_{ij} := \langle v_j, w_i \rangle 
$$

The matrix $R$ from its definition is upper triangular. For this reason, the QR decomposition 
is sometimes called the QU decomposition. 

The matrix $Q$ is an orthogonal matrix. 
Recall from this means the transpose of $Q$ is its inverse:
$$
    Q^T = Q^{-1} 
$$

**Lemma**. A $n \times n$ matrix $A$ is orthogonal if and only if its columns form an orthonormal basis. 

{% include beginproof.html %}
Let's look at $Q^TQ$. The i,j entry of $Q^TQ$ is 
$$
    q_{1j}q_{1i} + q_{2j}q_{2i} + \cdots + q_{nj}q_{ni} = \mathbf{C}_j^T \mathbf{C}_i 
$$
If we want this to be the identity matrix, it is equivalent to requiring that  
$$
     \mathbf{C}_j^T \mathbf{C}_i = \begin{cases} 1 & i = j \\ 0 & i \neq j \end{cases} 
$$
But this is exactly expressing that the vectors $\mathbf{C}\_1,\ldots,\mathbf{C}\_n$ are 
an orthonormal set in $\mathbb{R}^n$. Any orthonormal set is linearly independent and we have 
as many as the dimension of $\mathbf{R}^n$. Thus we have a basis. 
{% include endproof.html %}

Knowing this, we have the following. 

**Theorem**(QR Decomposition). For an invertible $n \times n$ matrix $A$ with entries in $\mathbb{R}$, 
there exists an orthogonal matrix $Q$ and an upper triangular matrix $R$ with
$$
    A = QR
$$

{% include beginproof.html %}
We take $Q$ to have columns given by applying Gram-Schmidt to the columns of $A$ and taking $R$ to 
be the matrix of pairings between columns of $Q$ and those of $A$ as above. 
{% include endproof.html %}

There is another useful characterization of orthogonal matrices. Given an inner product 
$\langle -,- \rangle$ on a vector space $k^n$, we say that an $n \times n$ matrix $A$ 
_preserves the inner product_ if 
$$
    \langle A w, A v \rangle = \langle w, v \rangle 
$$
In other words, applying $A$ to the two inputs and then taking the product returns the same 
number as just applying the product to the two inputs directly. 

**Lemma**. An $n \times n$ matrix $A$ preserves an the standard inner product on $k^n$ 
if and only if $A$ is orthogonal. 

{% include beginproof.html %}
We have 
$$
    \langle Av , Aw \rangle = (Av)^T Aw = v^T A^TA w.
$$
If $A$ is orthogonal, then this is equal to $v^T w = \langle v , w \rangle$. 

If we assume 
$$
    \langle Av, Aw \rangle = \langle v, w \rangle 
$$
for all $v,w \in k^n$, then taking $v = e_i$ and $w = e_j$ we have 
$$
     (A^TA)_{ij} = e_i^T A^TA e_j = e_i^T e_j
$$
Since 
$$
    \langle e_i, e_j \rangle = \begin{cases} 1 & i = j \\ 0 & i \neq j \end{cases} 
$$
we must have 
$$
    A^T A = I. 
$$
{% include endproof.html %}

As mentioned earlier, in Sage there is a method `A.gram_schmidt()` for a matrix $A$. It returns a 
decomposition very close to the QR one. 
- First it consumes a matrix $A$ whose _rows_ are the vectors in the basis. 
- It returns 
$$
    A = \tilde{Q} L 
$$
where $\tilde{Q}$ has orthogonal rows and $L$ is lower triangle. The rows here are the $u_i$'s from 
the [Gram-Schmidt]({% link notes/vector_spaces/gram_schmidt.md %}) as the rows of $\tilde{Q}$. While 
$L$ has $1$'s along the diagonal and 
$$
    L_{i,j} := \frac{\langle v_i, u_j \rangle}{\langle u_j, u_j \rangle}
$$
for the entries below the diagonal. 

There is a function on lists of vectors in Sage that will perform Gram-Schmidt alone. 
```python
sage: B = [vector([1,2,1/5]), vector([1,2,3]), vector([-1,0,0])]
sage: from sage.modules.misc import gram_schmidt
sage: G, mu = gram_schmidt(B)
sage: G
[(1, 2, 1/5), (-1/9, -2/9, 25/9), (-4/5, 2/5, 0)]
```
The example is taken from its [documentation](https://doc.sagemath.org/html/en/reference/modules/sage/modules/misc.html).