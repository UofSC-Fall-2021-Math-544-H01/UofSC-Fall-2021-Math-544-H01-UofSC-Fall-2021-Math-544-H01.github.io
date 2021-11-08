---
layout: page
title: Null Spaces and Ranges
nav_order: 5
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Null spaces and ranges of linear transformation 

The most important concepts we encountered for matrices were 
secretly built from linear transformations. 

For example, the null space and range of a matrix. We have 
the following definitions. 

**Definition**. Let $T: V \to W$ be a linear transformation. 
The _null space_ of $T$ is the set 
$$
    \mathcal Z(T) := \lbrace v \in V \mid T(v) = 0 \rbrace
$$
and the _range_ of $T$ is the set 
$$
    \mathcal R(T) := \lbrace w \in W \mid w = T(v) \rbrace
$$

The _nullity_ of $T$ is $\dim \mathcal Z(T)$ and 
the _rank_ of $T$ is $\dim \mathcal R(T)$. 

**Lemma**. The null space $\mathcal Z(T)$ is a subspace of 
$V$ and the range $\mathcal R(T)$ is a subspace of $W$.

{% include beginproof.html %}
We check that each are closed under linear combinations of 
two vectors. 

Let $v_1,v_2 \in \mathcal Z (T)$. Then, 
$$
    T(c_1v_1 + c_2v_2) = c_1T(v_1) + c_2T(v_2) = 0
$$
so $c_1v_1 + c_2v_2 \in \mathcal Z(T)$. 

Let $w_1,w_2 \in \mathcal R(T)$. We can therefore write 
$w_i = T(v_i)$. Now 
$$
    c_1w_1 + c_2w_2 = c_1T(v_1) + c_2T(v_2) = T(c_1v_1+c_2v_2)
$$
so $c_1w_1+c_2w_2 \in \mathcal R(T)$. 
{% include endproof.html %}

**Proposition**. Assume that $\dim V, \dim W < \infty$ and that 
$A$ is a matrix representation for $T$ in some bases for $V$ 
and $W$. Then, 
$$
    \mathcal Z(T) \cong \mathcal Z(A) 
$$
and 
$$
    \mathcal R(T) \cong \mathcal R(A)
$$

{% include beginproof.html %}
Let's choose bases $v_1,\ldots,v_n$ for $V$ and $w_1,\ldots,w_m$ 
for $W$ and have $A$ be the matrix representation of $T$ in 
these bases. 

Take $v \in \mathcal Z(T)$ and write it in the basis
$$
    v = \sum_{i=1}^n c_i v_i
$$
Denote 
$$
    \mathbf{c} := \begin{pmatrix} c_1 \\ c_2 \\ \vdots \\ c_n \end{pmatrix}
$$
Let's write out $A \mathbf{c}$ 
$$
    (A \mathbf{c})_j = \sum_{j=1}^m A_{ji} c_i
$$
Applying $T$ directly to $v$ gives 
$$
    T(v) = \sum_{i=1}^n c_i T(v_i) = \sum_{i=1}^n c_i \left(\sum_{j=1}^m A_{ji} w_j \right) 
    = \sum_{j=1}^m \left(\sum_{i=1}^n A_{ji} c_i \right) w_j
$$
If $T(v) = 0$, then, as $w_1,\ldots,w_j$ is a basis, we see that 
$$
    \sum_{i=1}^n A_{ji} c_i = 0
$$
for all $1 \leq j \leq m$. In other words, $\mathbf{c} \in \mathcal Z(A)$. 

In the other direction, if $\mathbf{c} \in \mathcal Z(A)$, then $T(v) = 0$. Thus, 
$$
    \begin{aligned}
        \mathcal Z(T) & \to \mathcal Z(A) \\
        v & \mapsto \mathbf{c}
    \end{aligned}
$$
is an isomorphism. 

Next we turn to the ranges. Given $w \in W$, we write it in the vector representation 
for the basis $w_1,\ldots,w_m$ 
$$
    w = \sum_{j=1}^m d_j w_j 
$$
We will check that 
$$
    \begin{aligned}
        \mathcal R(T) & \to \mathcal R(A) \\
        w & \mapsto \mathbf{d}
    \end{aligned}
$$
is an isomorphism. From the computation above, 
$$
    T(v) = \sum_{i=1}^n c_i T(v_i) = \sum_{i=1}^n c_i \left(\sum_{j=1}^m A_{ji} w_j \right) 
    = \sum_{j=1}^m \left(\sum_{i=1}^n A_{ji} c_i \right) w_j
$$
we see that $T(v)$ in vector representation has $A\mathbf{c}$ as coefficients. Thus, 
$w = T(v)$ if and only if $\mathbf{d} = A \mathbf{c}$ so the above map is an isomorphism. 
{% include endproof.html %}

The previous statement tells us that we can use our familiar tools for matrices to 
understand null spaces and ranges for linear transformations _once we choose a basis_. 

As an application of this principle, we can quickly deduce the Rank-Nullity Theorem for 
linear transformations. 

**Theorem**. (Rank-Nullity) Let $T: V \to W$ be a linear transformation with 
$\dim V, \dim W < \infty$.
Then, 
$$
    \operatorname{rank} T + \operatorname{nullity} T = \dim V. 
$$

{% include beginproof.html %}
Since $\mathcal Z(T) \cong \mathcal Z(A)$ and $\mathcal R(T) \cong \mathcal R(A)$, we 
have 
$$
    \operatorname{nullity} T = \dim \mathcal Z(T) = \dim \mathcal Z(A) = 
    \operatorname{nullity} A
$$
and
$$
    \operatorname{rank} T = \dim \mathcal R(T) = \dim \mathcal R(A) = 
    \operatorname{rank} A
$$
The dimension of $V$ is equal to number of columns of $A$ so we know 
$$
    \operatorname{rank} A + \operatorname{nullity} A = \dim V
$$
from the 
[Rank-Nullity Theorem]({% link notes/vector_spaces/rank.md %}#rank-nullity-theorem) 
for $A$. 
{% include endproof.html %}

From a previous [worksheet]({% link worksheets/17.md %}), we have the following. 

**Proposition**. A linear transformation $T: V \to W$ is an isomorphism if and 
only if $\mathcal Z(T) = 0$ and $\mathcal R(T) = W$. 

There is another common adjective for isomorphisms. 

**Definition**. A linear transformation $T: V \to W$ is _nonsingular_ if 
$T$ is an isomorphism. Otherwise, it is called _singular_. 

Computing the null space and range of a linear transformation offers a means 
to check non-singularity. 