---
layout: page
title: QR factorizations
nav_order: 10
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: true
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

**Lemma**. A square matrix $A$ is orthogonal if and only if its columns form an orthonormal basis. 

{% include begin_proof.html %}
Let's look at $Q^TQ$. The i,j entry of $Q^TQ$ is 
$$
    q_{1j}q_{1i} + q_{2j}q_{2i} + \cdots + q_{nj}{ni} = \mathbf{C}_j^T \mathbf{C}_i 
$$
If we want this to be the identity, then we need 
$$
     \mathbf{C}_j^T \mathbf{C}_i = \begin{cases} 1 & i = j \\ 0 & i \neq j \end{cases} 
$$
But this is exactly expressing that the vectors $\mathbf{C}\_1,\ldots,\mathbf{C}\_n$ are 
an orthonormal set in $\mathbb{R}^n$. Any orthonormal set is linearly independent and we have 
as many as the dimension of $\mathbf{R}^n$. Thus we have a basis. 
{% include end_proof.html %}