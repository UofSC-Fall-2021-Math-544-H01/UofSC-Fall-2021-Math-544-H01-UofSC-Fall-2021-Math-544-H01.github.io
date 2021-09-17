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

One of most common ways to make new vector spaces out of old ones is take a known vector 
space $V$ and find a subset $W$ that inherits the vector space structure from $V$. 

**Definition**. A _subspace_ $W$ of a $k$-vector space $V$ is a subset $W \subseteq V$ satisfying 
the conditions that
- $W$ is _closed under addition_: for any two vectors, their sum is in $W$, ie
$$
    w_1,w_2 \in W \Rightarrow w_1 + w_2 \in W
$$ 
- $W$ is _closed under scaling_: for any scalar $c \in k$ and any vector $w \in W$, scaling $w$ by 
$c$ is also in $W$, ie
$$
    c \in k, \ w \in W \Rightarrow c \cdot w \in W.
$$

Notice that the definition of a subspace did not say it is a vector space! That is a consequence of 
the definition.

**Proposition**. Suppose that $V$ is a $k$-vector space and $W$ is a subset of $V$. If $W$ is a 
subspace, then $W$ with addition and scaling inherited from $V$ is also a vector space. 



<details>
<summary>
Expand for the proof. 
</summary>

**Proof**. Let's try to spell out what "addition and scaling inherited from $V$" is precisely. 

Recall that the condition that $W$ is closed under $+$ means that for any pair of vectors 
$w_1, w_2 \in W$, their sum $w_1 + w_2 \in W$. We say vectors here because we are implicitly viewing 
$w_1, w_2 \in V$ via the inclusion $W \subseteq V$. This is the only way to make sense of the 
expression $w_1 + w_2$. The content of being closed under $+$ is the statement that the element 
$w_1 + w_2 \in V$ actually lies back in the subset $W$. 

We can succinctly capture this by saying that 
$$
    + : W \times W \to W 
$$
is a well-defined function. In particular, its codomain is actually what we claim it to be: $W$. This 
is the addition inherited from $V$. 

Similarly, if we take $w \in W$ view it as an element of $V$ and scale it, then the result actually 
still lies in $W$. 
$$
    \cdot : k \times W \to W
$$
is also a well-defined function. This is the scalar multiplication inherited from $V$. 

With that exposition out of the way, let's check that $W$ satisfies the 
[conditions]({% link notes/vector_spaces/def_egs.md %}#Definition) for being a 
vector space one by one. 
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

</details>