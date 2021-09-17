---
layout: page
title: Spans
nav_order: 4
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: true
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Spanning sets and spans

In general, if we take a random subset $U \subseteq V$ of a vector space, we 
are usually not going to get a subspace. 

A particularly good example of this phenomenon is: a finite subset of 
a $\mathbb{R}$-vector space $V$
$$
    \lbrace v_1, \ldots, v_r \rbrace \subset V 
$$
is a subspace over $\mathbb{R}$ if and only if 
$$
    v_1 = v_2 = \cdots = v_r = 0. 
$$

Why? If $v_i \neq 0$, then we will need to have a whole line 
$$
    \lbrace c \cdot v_i \mid c \in \mathbb{R} \rbrace
$$
inside a finite set. 

However, there is a way to correct, or close up, $U$ into a subspace. 

**Definition**. Let $V$ be a vector space and $U \subseteq V$. The 
_span_ of $U$ is the set 
$$
    \operatorname{Span}(U) := \lbrace c_1 u_1 + \cdots + c_r u_r \mid u_i \in U, 
    c_i \in k, r \in \mathbb{N} \rbrace.
$$
In other words, the $\operatorname{Span}(U)$ is the set of all possible linear 
combinations of vectors in $U$. 

The key fact about the span of $U$ is the following.

**Lemma**. The span of $U$ is a subspace of $V$. 

<details markdown="block">
<summary>
<b>Proof</b>. (Expand to view)
</summary> 

We use the [criteria]({% link notes/vector_spaces/subspaces.md%}#consequences-of-the-definition) of checking that 
any linear combination of two vectors from $\operatorname{Span}(U)$ is also an element of $\operatorname{Span}(U)$.

Let's take two vectors from $\operatorname{Span}(U)$. By definition, we can write them as 
$$
    \begin{aligned}
        w_1 & = a_1 u_1 + \cdots + a_r u_r \\
        w_2 & = b_1 u^\prime_1 + \cdots b_s u^\prime_s
    \end{aligned}
$$
for $a_i,b_i \in k$ and $u_i, u^\prime_i \in U$. Pick $c_1,c_2 \in k$, then we expand 
the linear combination 
$$
    \begin{aligned}
        c_1 w_1 + c_2 w_2 & = c_1(a_1 u_1 + \cdots + a_r u_r) + c_2(b_1 u^\prime_1 + \cdots b_s u^\prime_s)\\
        & = (c_1a_1) u_1 + \cdots (c_1a_r) u_r + (c_2b_1) u^\prime_1 + \cdots + (c_2b_s) u^\prime_s
    \end{aligned}
$$
We see that this is also a linear combination of elements of $U$. Hence $c_1 w_1 + c_2 w_2 \in \operatorname{Span}(U)$.
<span style="float:right;"> &#9632; </span>

</details>