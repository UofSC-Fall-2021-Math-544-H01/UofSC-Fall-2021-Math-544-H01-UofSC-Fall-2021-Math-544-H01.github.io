---
layout: page
title: Spans
nav_order: 4
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: false
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

**Definition**. Given a vector space $V$, a subset $U$ _spans_ $V$ if 
$$
    \operatorname{Span}(U) = V.
$$
If $U$ spans $V$, we call it a _spanning set_ for $V$.

A common question in linear algebra is: given a vector space, identify a spanning set for it.  

### Consequences

The following is a simple observation but useful to keep in mind. 

**Lemma**. $U \subseteq \operatorname{Span}(U)$. 

{% include beginproof.html %}
    Note that $U \subseteq \operatorname{Span}(U)$ since we can take the linear combination $1 \cdot u = u$.
{% include endproof.html %}

As mentioned, taking the span is a way to "close up" a general subset under linear combinations. But if 
that subset is already a subspace it does nothing. 

**Lemma**. The span $\operatorname{Span}(U)$ is the smallest subspace of $V$ containing $U$. More precisely, 
if a $W \subseteq V$ is a subspace with $U \subseteq W$, then 
$$
    \operatorname{Span}(U) \subseteq W
$$
also. In particular, if $U$ is already a subspace then $\operatorname{Span}(U) = U$. 

{% include beginproof.html %}
    Assume that $W$ is a subspace and $U \subseteq W$. Since $W$ is closed under linear combinations 
    $$
        c_1 u_1 + \cdots + c_r u_r \in W
    $$
    as each $u_i \in W$. Thus, $\operatorname{Span}(U) \subseteq W$. 

    If $U$ were already a subspace, then applying the previous statement shows that $\operatorname{Span}(U) 
    \subseteq U$. Since we just saw that $U \subseteq \operatorname{Span}(U)$, we have 
    $$
        U = \operatorname{Span}(U).
    $$
{% include endproof.html %}

### Examples 

- The vector space $k^n$ is the span of the vectors: 
$$
    \mathbf{e}_i := \begin{pmatrix} 0 \\ \vdots \\ 0 \\ 1 \\ 0 \\ \vdots \\ 0 \end{pmatrix} \leftarrow i^{th},   \text{ for } 1 \leq i \leq n 
$$
Indeed, any vector can be expressed as a linear combination 
$$
    \begin{pmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{pmatrix} = v_1 \mathbf{e}_1 + v_2 \mathbf{e}_2 + \cdots + v_n \mathbf{e}_n
$$

- Perhaps the inspiration for the general notion of the span is the range of a matrix. Let $A$ be a 
$m \times n$ matrix then $\mathcal R(A)$ is the span of the column vectors $\mathbf{C}_1^A, \ldots, 
\mathbf{C}_n^A$. 

    Remember that the range of $A$ is set of vectors of the form $A \mathbf{x}$ for all $\mathbf{x} \in k^n$. 
    We can rewrite the multiplication as 
    $$
        A \mathbf{x} = x_1 \mathbf{C}_1^A + x_2 \mathbf{C}_2^A + \cdots + x_n \mathbf{C}_n^A.
    $$
    The scalars we use for the linear combination are the components of the vector $\mathbf{x}$. 

- Polynomials of degree $\leq d$. The vector space $\operatorname{Poly}_d(\mathbb{R})$ is spanned by the polynomials 
$$
    1, x, x^2, \ldots, x^d
$$
since, by definition, we can write any polynomial $p(x)$ in $\operatorname{Poly}(\mathbb{R})$
$$
    p(x) = a_d x^d + a_{d-1}x^{d-1} + \cdots a_1x + a_0. 
$$


- In the examples above, each subspace had a _finite_ spanning set. In general this is not the case. Consider the set of 
all polynomials $\operatorname{Poly}(\mathbb{R})$. Take any finite set of polynomials $p_1,\ldots,p_s$. For each $p_i$, 
let $d_i$ be the degree of $p_i$ and let $d = \max d_i$. 

    We claim that $x^{d+1} \not \in \operatorname{Span}(\lbrace p_1, \ldots, p_s \rbrace )$. Why? In any linear combination 
    $$
        c_1p_1 + \cdots c_sp_s,
    $$
    $x^{d+1}$ never appears as a term. The largest $x^r$ possible is $x^d$. 

    Thus, $\operatorname{Poly}(\mathbb{R})$ does not have a finite spanning set. 

    It does have an infinite spanning set consisting of _all_ monomials
    $$
        1, x, x^2, \ldots, x^m, \ldots.
    $$

### Spanning sets for null spaces 

We have seen that null spaces can be written as ranges. Therefore they have spanning sets. But, how do 
we compute one? Let's take the example of 
$$
    A = 
    \begin{pmatrix}
        1 & 2 & -1 & 0 \\
        1 & -1 & 1 & 2 \\
        2 & 1 & 0 & 2 
    \end{pmatrix}
$$
We first convert it to reduced row echelon form. 
$$
    B = 
    \begin{pmatrix}
        1 & 0 & 1/3 & 4/3 \\
        0 & 1 & -2/3 & -2/3 \\
        0 & 0 & 0 & 0 
    \end{pmatrix}
$$ 
Our free variables are $x_3$ and $x_4$. We can write the general parametrized solution in terms of these as 
$$
    \mathbf{x} = 
    \begin{pmatrix}
        -x_3/3 - 4x_4/3 \\
        2x_3/3 + 2x_4/3 \\
        x_3 \\
        x_4 
    \end{pmatrix}
$$
and break that up into a linear combination of the two vectors where we set $x_3=1,x_4=0$ and $x_3=0,x_4=0$
$$
    \begin{pmatrix}
        -x_3/3 - 4x_4/3 \\
        2x_3/3 + 2x_4/3 \\
        x_3 \\
        x_4 
    \end{pmatrix} = 
    x_3 \begin{pmatrix} 
        -1/3 \\
        2/3 \\
        1 \\
        0 
    \end{pmatrix} + 
    x_4 \begin{pmatrix} 
        -4/3 \\
        2/3 \\
        0 \\
        1 
    \end{pmatrix}
$$
Thus, $\mathcal Z(A)$ is the span of 
$$
    \begin{pmatrix} 
        -1/3 \\
        2/3 \\
        1 \\
        0 
    \end{pmatrix}, \
    \begin{pmatrix} 
        -4/3 \\
        2/3 \\
        0 \\
        1 
    \end{pmatrix}
$$

In general, we have the following.

**Proposition**. The null space will be spanned by $d$ vectors where $d$ is the number of free 
variables in row echelon form. To get a spanning set, we can write the general parametric solution 
for system and evaluate $d$ times by setting each free variable to $1$ and all the others to $0$. 
