---
layout: page
title: Eigenvectors
nav_order: 6
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Eigenvectors and Eigenvalues

We have seen a few notions we can attach to a linear tranformation 
built from the kernel and range. Here we introduce a different 
but very important one. 

**Definition**. Let $T: V \to V$ be a linear transformation. A 
vector $v \in V$ is called an _eigenvector_ for $T$ if $v \neq 0$
and 
$$
    T(v) = \lambda v
$$
for some scalar $\lambda \in k$. The scalar $\lambda$ is called 
the _eigenvalue_ of the eigenvector $v$. 

Given a scalar $\lambda \in k$, the $\lambda$-_eigenspace_ is 
$$
    E_{\lambda}(T) := \lbrace v \in V \mid T(v) = \lambda v \rbrace 
$$

**Lemma**. Eigenspaces are subspaces. 

{% include beginproof.html %}
We check $E_\lambda$ is closed under linear combinations of 
two vectors. If $T(v_1) = \lambda v_1$ and $T(v_2) = 
\lambda v_2$, then 
$$
    T(c_1v_1+c_2v_2) = c_1T(v_1) + c_2T(v_2) c_1 \lambda v_1 
    + c_2 \lambda v_2 = \lambda(c_1v_1 + c_2v_2)
$$
So $c_1v_1 + c_2v_2 \in E_\lambda$. 
{% include endproof.html %}

Eigenvectors are important because they allow use to understand  
the structure of the linear transformation. 

**Example**. Let 
$$
    D = \begin{pmatrix}
    \lambda_1 & 0 & \cdots & 0 \\
    0 & \lambda_2 & \cdots & 0 \\
    \vdots & \vdots & \ddots & \vdots \\
    0 & \cdots & 0 & \lambda_n 
    \end{pmatrix}
$$
be a diagonal matrix. Then, each standard basis vector 
$\mathbf{e}_i$ is eigenvector for $D$ with eigenvalue 
$\lambda_i$. 

**Proposition**. Suppose that $T : V \to V$ is a linear 
transformation with $\dim V < \infty$. 
If $V$ has a basis of eigenvectors of 
$T$, $T$ has a matrix representation which is a 
diagonal matrix. 

{% include beginproof.html %}
Let $v_1,\ldots,v_d$ be a basis of $V$ with 
$$
    T(v_i) = \lambda_i v_i
$$
for each $i$. Then the matrix representation of 
$T$ using the basis $v_1,\ldots,v_d$ in both the domain 
and codomain is 
$$
    D = \begin{pmatrix}
    \lambda_1 & 0 & \cdots & 0 \\
    0 & \lambda_2 & \cdots & 0 \\
    \vdots & \vdots & \ddots & \vdots \\
    0 & \cdots & 0 & \lambda_n 
    \end{pmatrix}
$$
{% include endproof.html %}

If we are allowed to choose two different bases for $V$, 
one to use in the domain and one for the codomain, then 
we can find diagonal matrix representation for any 
$T : V \to V$. However, this will not guarantee that 
we have found any eigenvectors. We need the matrix 
representation of $T$ to be diagonal for _the same_ 
basis on each side. 

After choosing a basis, we get a matrix representation 
$A$ for $T$. Changing to a different basis, the same in 
the source and target, replaces $A$ with 
$$
    S^{-1}AS
$$
where $S$ is the change of basis matrix. 

**Definition**. A $n\times n$ matrix $A$ is _diagonalizable_ if 
there exists an invertible $n \times n$ matrix $S$ with 
$S^{-1} A S$ diagonal. 

**Proposition**. Let $T: V \to V$ be a linear transformation 
with $\dim V < \infty$. Then $V$ has a basis of 
eigenvectors if and only a(ny) matrix representation in the 
same basis for both domain and codomain for 
$T$ is diagonalizable. 

{% include beginproof.html %}
As before, we can take the matrix representation of $T$ 
using our basis of eigenvectors in $V$ for both the domain and 
codomain to get a diagonal matrix representation. 

Assume $A$ is some matrix representation of $T$ with the basis 
$v_1,\ldots,v_d$ used for the domain and codomain 
and we know that $S^{-1}AS$ is diagonal. Then 
$$
    w_i := \sum_{j=1}^d S_{ij}v_j
$$
is a new basis for $V$. The change of basis matrix 
from $v_1, \ldots, v_d$ to $w_1,\ldots,w_d$ is the matrix $S$ 
and $T$ in the new basis is $S^{-1}AS$ which is diagonal. 
Thus $w_1,\ldots,w_d$ is a basis for eigenvectors for $V$. 
{% include endproof.html %}

If we can find eigenvectors with different eigenvalues, we 
get linear independence automatically. 

**Lemma**. Let $v_1,\ldots,v_s$ be eigenvectors for 
$T: V \to V$ with $\lambda_i \neq \lambda_j$ if $i \neq j$. 
Then, $v_1,\ldots,v_s$ is linearly independent. 

{% include beginproof.html %}
If $v_1,\ldots,v_s$ are linearly dependent, we can write
at least one as a linear combination of the other vectors. 
Up to relabeling we have, 
$$
    v_{t+1} = \sum_{j=1}^t c_i v_i
$$
with $v_1,\ldots,v_t$ linearly independent. 
Now applying $T$ we get 
$$
    \lambda_{t+1} v_{t+1} = \sum_{j=1}^t \lambda_i c_i v_i 
$$

If $\lambda_{t+1} = 0$, then we have relation so at least one 
$\lambda_i = 0$ since $v_1,\ldots,v_t$ is linearly independent 
and not all $c_i = 0$. This is a contradiction. 

If $\lambda_{t+1} \neq 0$, then we can divide by $\lambda_{t+1}$ 
to get 
$$
    v_{t+1} = \sum_{j=1}^t \frac{\lambda_i}{\lambda_{t+1}} c_i v_i 
$$
which gives another way to write $v_{t+1}$ as linear combination of 
$v_1,\ldots,v_t$. So 
$$
    c_i = \frac{\lambda_i}{\lambda_{t+1}} c_i 
$$
for all $i$. If $\lambda_i \neq \lambda_{t+1}$, then $c_i = 0$ 
which contradicts $v_{t+1} \neq 0$.
{% include endproof.html %}

Our next goal will be to understand the eigenspaces and the 
set of eigenvalues of a linear transformation. We will need a 
helpful tool: 
[determinants]({% link notes/linear_transformations/determinants.md %}).
