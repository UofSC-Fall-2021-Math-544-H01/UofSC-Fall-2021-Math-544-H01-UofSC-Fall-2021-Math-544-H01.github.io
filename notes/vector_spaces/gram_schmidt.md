---
layout: page
title: Gram Schmidt
nav_order: 9
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: true
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Orthogonalization

<!-- The following lemma is useful to help check when a candidate inner product is actually 
an inner product. 

**Lemma**. Let $V$ be a vector space and $v_1,\ldots,v_d$ be a basis for $V$. Assume 
we have a linear and symmetric pairing 
$$
    \langle - , - \rangle : V \times V \to k.
$$
Let $A$ be the matrix $A_{ij} = \langle v_i, v_j \rangle$. Then $\langle -,- \rangle$ is 
nondegenerate if and only if $A$ is invertible. 

{% include beginproof.html %}
We saw above that computing $\langle v, w \rangle$ is the same as computing the $y^T A x$ 
where $y$ and $x$ are the representations of $v$ and $w$ in the basis. 

From our example above, we know that if $A$ is invertible $y^T A x$ is an inner product. 

Assume that $A$ is not invertible. Then, its row echelon form must have a zero row and so 
$\ker A \neq 0$. Pick a nonzero $u \in \ker A$. Then, 
$$
    y^T A u = 0 
$$
for all $y$. Thus, $\langle -,- \rangle$ is degenerate. 
{% include endproof.html %}

**Corollary**.  -->

<!-- 
**Lemma**. Let $V$ be a vector space and $v_1,\ldots,v_d$ be a basis for $V$. Assume 
we have a linear and symmetric pairing 
$$
    \langle - , - \rangle : V \times V \to k.
$$
The pairing is an inner product if and only if for each $v_i$ there some $w_i \in V$ with 
$$
    \langle v_i , w_i \rangle \neq 0
$$

{% include beginproof.html %}
If $\langle - , - \rangle$ is non-degenerate, then we already know for any nonzero $v \in V$ 
we must have a $w$ with $\langle v, w \rangle \neq 0$. In particular, this is true for 
each $v_i$.

Now assume that for each $v_i$ there some $w_i \in V$ with 
$$
    \langle v_i , w_i \rangle \neq 0
$$
and let $
{% include endproof.html %} -->