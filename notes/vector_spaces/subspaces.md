---
layout: page
title: Subspaces
nav_order: 3
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: true
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Subspaces



**Lemma**. Suppose that $V$ is a $k$-vector space and $W$ is a subset of $V$. Then $W$ (with its addition and scalar 
multiplication inherited from $V$) is also a $k$-vector space if and only if $W$ is closed under addition and 
scalar multiplication, ie for any $w_1,w_2 \in W$, we have $w_1 + w_2 \in W$ and for any $c \in k$ and $w \in W$, we 
have $cw \in W$. 

**Proof**. Part of being a vector space is that $+ : W \times W \to W$ and $\cdot: k \times W \to W$ are well 
defined functions. We can add two elements of $W$ and output of will still be an element of $W$. Similarly, we 
can scale an element of $W$ and still have an element of $W$. So being closed under addition has to hold if $W$ 
is a $k$-vector space. 

In the other direction, since $V$ is a vector space itself, we know the 
[list]({% link notes/vector_spaces/def_egs.md %}#Definition) of conditions has to be satisfied already. For example, 
for $w_1,w_2 \in W$, since $W \subseteq V$ we know that $w_1 + w_2 = w_2 + w_1$ will hold. 

If for any $w_1,w_2 \in W$, we have $w_1 + w_2 \in W$ and for any $c \in k$ and $w \in W$, we 
have $cw \in W$, the functions
$$
    \begin{aligned}
        + : W \times W & \to W \\
        \cdot : k \times W & \to W
    \end{aligned}
$$
land back in $W$. Now, we check the conditions for $W$ to be a vector space itself. 
- $+$ is a associative: $(w_1+w_2)+w_3 = w_1+(w_2+w_3)$. 

    Since each $w_i \in V$ and this holds for all elements of $V$ by assumption, we are good. 

- $+$ is commutative: $v_1 + v_2 = v_2 + v_1$. 

    Similarly, since $w_i \in V$ and $V$ is a vector space we know this already true. 

- There is an element $0 \in W$ with $0 + w = w + 0 = 0$ for any $w \in W$. 

    Here we have something to check. Is $0$ from $V$ actually an element of the subset $W$? 
    There is a trick here. Notice that in a vector space we have 
    $$
        0 \cdot v = (0+0)\cdot v = 0 \cdot v + 0 \cdot v
    $$
    Subtracting $0 \cdot v$ from both sides leaves 
    $$
        0 = 0 \cdot v
    $$
    Then, 
    $$
        0 = (1-1)\cdot v = v + (-1) \cdot v
    $$
    Thus, $(-1) \cdot v$ is the additive inverse $-v$. 

    Since $W$ is closed under the scalar action $\cdot$, we know that $(-1) \cdot w \in W$. 
    Since $W$ is closed under addition and $w, -w \in W$, we have 
    $$
        0 = w + (-w) \in W
    $$
    also.

- For any element $w \in W$, there is another $-w$ with $w + (-w) = (-w) + w = 0$. 

    We established that $-w \in W$ if $w \in W$ in the previous step. 

- $\cdot$ distributes over $+$: 
$$
    c \cdot (w_1 + w_2) = c\cdot w_1 + c \cdot w_2
$$

    Since this is true for all elements of $V$ and $W \subseteq V$, it is true for all elements of $W$. 

- $1 \cdot$ is the identity: 
$$
    1 \cdot w = w 
$$
for all $w \in W$.

    Since this is true for all elements of $V$ and $W \subseteq V$, it is true for all elements of $W$. 

- Finally, $\times$ in $k$ and $\cdot$ have the following relation 
$$
    (c_1 \times c_2) \cdot w = c_1 \cdot (c_2 \cdot w)
$$

    Again, since this is true for all elements of $V$ and $W \subseteq V$, it is true for all elements of $W$. 
    $\blacksquare$