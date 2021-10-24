---
layout: page
title: Isomorphisms
nav_order: 4
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Isomorphisms

**Definition**. A linear transformation $T: V \to W$ is an 
_isomorphism_ if there is a linear transformation, usually 
denoted by $T^{-1}: W \to V$, satisfying 
$$
    T^{-1}(T(v)) = v ~\text{for all}~ v \in V
$$
and 
$$
    T(T^{-1}(w)) = w ~\text{for all}~ w \in W
$$
In other words, 
$$
    T^{-1} \circ T = \operatorname{Id}_V 
$$
and
$$
    T \circ T^{-1} = \operatorname{Id}_W
$$

**Proposition**. A linear transformation $T: V \to W$ is an 
isomorphism if and only if $T$ is a bijection. 

{% include beginproof.html %}
If $T$ is an isomorphism, then $T^{-1}$ is the inverse function 
to $T$. So $T$ is a bijection. 

Assume that $T$ is a linear transformation and also a bijection. 
Since it is a bijection, there is an inverse _function_ 
$S : W \to V$ of sets. We want to see that $S$ is also a 
natural transformation. 

Pick $w \in W$. Since $T$ is surjective, we can write it as 
$w = T(v)$. Then,  
$$
    S(cw) = S(cT(v)) = S(T(cv)) = cv = cS(w)
$$
Similarly, if we have $w,w^\prime \in W$, we can write 
$w = T(v)$ and $w^\prime = T(v^\prime)$. Then, 
$$
    S(w + w^\prime) = S(T(v) + T(v^\prime)) = ST(v+v^\prime) = v + v^\prime = S(w) + S(w^\prime)
$$
Thus, $S$ is a linear transformation and $T$ is an isomorphism. 
{% include endproof.html %}

Two vector spaces that are related by an isomorphism are called 
_isomorphic_ and we write 
$$
    V \cong W. 
$$
Isomorphic vector spaces are not the same, ie equal. 
But, since they differ by a linear relabeling, they are the same 
by any measure of linear algebra. 

**Example**. For a field $k$, the vector spaces of $m\times n$ matrices, 
$\operatorname{Mat}_{m,n}(k)$, and $k^{mn}$ are isomorphic. 

We consider the function
$$
    \begin{aligned}
        T : \operatorname{Mat}_{m,n}(k) & \to k^{mn} \\
        (A_{ij}) & \mapsto \begin{pmatrix} A_{11} & \cdots & A_{mn} \end{pmatrix}^T
    \end{aligned}
$$
which just lists the entries of the matrix reading left to right and then moving down 
to the next row. 

This is a bijection since we can take the length $mn$ list and break it up into 
$m$ intervals of length $n$ to get the rows of the matrix. 

Since $c(A_{ij})= (cA_{ij})$ and $(A_{ij}) + (B_{ij}) = (A_{ij}+B_{ij})$ are just 
componentwise scaling and addition, we see the result is the same whether we scale or 
add before or after applying $T$. Thus, we have an isomorphism.

**Example**. Let $A$ be an $n \times n$ matrix and take 
$$
    \begin{aligned}
        T : k^n & \to k^n \\
        \mathbf{v} & \mapsto A \mathbf{v}
    \end{aligned}
$$
Then, $T$ is an isomorphism if and only if $A$ is an invertible matrix. 

Indeed, if we have an inverse matrix $A^{-1}$, multiplication by $A^{-1}$ 
gives the inverse function $T^{-1}(\mathbf{v}) := A^{-1}\mathbf{v}$.
$$
    A(A^{-1}\mathbf{v}) = I \mathbf{v} = \mathbf{v} \\
    A^{-1}(A\mathbf{v}) = I \mathbf{v} = \mathbf{v} \\
$$

In the other direction, assume we have an inverse linear transformation 
$T^{-1} : k^n \to k^n$. Using the standard basis for both copies of 
$k^n$ we get a matrix representation $B$ of $T^{-1}$. This satisfies 
$$
    \mathbf{v} = T(T^{-1}(\mathbf{v})) = AB\mathbf{v}
$$
for all $\mathbf{v}$ and 
$$
    \mathbf{v} = T^{-1}(T(\mathbf{v}) = BA\mathbf{v}
$$
Plugging in $\mathbf{e}_i$, $AB\mathbf{e}_i$ is the i-th column of $AB$. 
Since $AB\mathbf{e}_i = \mathbf{e}_i$ for all $i$, we see that $AB = I$. 
Similarly, $BA = I$. 

**Proposition**. Isomorphic vector spaces have equal dimensions. 

{% include beginproof.html %}
Let $T: V \to W$ be an isomorphism of vector spaces. And let $v_i, i \in B$ 
be a basis for $V$. We claim that $T(v_i), i \in B$ is a basis for $W$. 
Assuming this claim for a moment, since 
$$
    T : \lbrace v_i \mid i \in B \rbrace \to \lbrace T(v_i) \mid i \in B \rbrace 
$$
is a bijection, then number of $v_i$ equals the number of $T(v_i)$. Thus, the 
dimensions of $V$ and $W$ coincide. 

Now let's check that $T(v_i), i \in B$ forms a basis for $W$. Assume we have 
a linear relation 
$$
    0 = \sum_{i \in B} c_i T(v_i)
$$
Then, since 
$$
    0=\sum_{i \in B} c_i T(v_i) = T\left( \sum_{i \in B} c_iv_i \right)
$$
$T(0) = 0$ and $T$ is injective, we have
$$
    0 = \sum_{i \in B} c_iv_i
$$
This is a linear relation amongst elements of a basis. Thus $c_i = 0$ for all $i$. 
So $T(v_i), i \in $ is a linearly independent set. 

Now pick $w \in W$. Since $T$ is surjective, we know there is some $v \in V$ with 
$T(v) = w$. Since $v_i$ span, we can write 
$$
    v = \sum_{i \in B} c_i v_i 
$$
Applying $T$ we have 
$$
    w = T(v) = T\left( \sum_{i \in B} c_i v_i \right) = \sum_{i \in B} c_i T(v_i)
$$
So $w$ is in the span of the $T(v_i)$. 
{% include endproof.html %}

The converse statement also holds. 

**Proposition**. If two $k$-vector spaces have the same dimension, then they are 
isomorphic. 

{% include beginproof.html %}
Let $V$ and $W$ be $k$-vector spaces with $\dim V = \dim W$. Pick bases 
$v_1,\ldots,v_d$ and $w_1,\ldots,w_d$ for $V$ and for $W$. Then we have seen that 
there exists unique linear transformation $T: V \to W$ with 
$$
    T(v_i) = w_i
$$
Similarly, there exists a unique line $S:W \to V$ with 
$$
    S(w_i) = v_i 
$$
Note that for each $i$
$$
    ST(v_i) = v_i 
$$
Thus, since they both act the same on a basis, we have $ST = \operatorname{Id}_V$. 
Similarly we have $$TS = \operatorname{Id}_W$. So we see that $T$ is an 
isomorphism. 
{% include endproof.html %}

Combining the two statements, we have the following. 

**Theorem**. Two vector spaces are isomorphic if and only if they have 
the same dimension. 

This theorem says that the dimension of $V$ captures all the information 
about it. 