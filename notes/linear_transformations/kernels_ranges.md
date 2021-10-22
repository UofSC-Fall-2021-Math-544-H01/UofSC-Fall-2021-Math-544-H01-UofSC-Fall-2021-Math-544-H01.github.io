---
layout: page
title: Kernel, Range, Nullity, Rank
nav_order: 5
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: true
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Kernels and ranges of linear transformation 

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
    \mathcal R(T) := \lbrace w \in W \mid w = T(v) \text
$$

The _nullity_ of $T$ is $\dim \mathcal Z(T)$ and 
the _rank_ of $T$ is $\dim \mathcal R(T)$. 

**Lemma**. The null space $\mathcal Z(T)$ is a subspace of $V$. 
The range $\mathcal R(T)$ 

**Proposition**. Assume that $\dim V, \dim W < \infty$ and that 
$A$ is a matrix representation for $T$ in some bases for $V$ 
and $W$. Then, 
$$
    \mathcal Z(T) = \mathcal Z(A) 
$$
and 
$$
    \mathcal R(T) = \mathcal R(A)
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
$4
Let's write out $A \mathbf{c}$ 
$$
    (A \mathbf{c})_j = \sum_{j=1}^m A_{ji} c_i
$$
Applying $T$ directly to $v$ gives 
$$
    T(v) = \sum_{i=1}^n c_i T(v_i) = \sum_{i=1}^n c_i \left(\sum_{j=1}^m A_{ji} w_j \right)
$$


Let's denote $\dim V = n$ and $\dim W = m$. Then $A$ is a 
$m \times n$ matrix 
{% include endproof.html %}