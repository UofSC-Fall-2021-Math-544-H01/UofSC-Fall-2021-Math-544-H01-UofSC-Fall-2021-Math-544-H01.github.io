---
layout: page
title: Definitions and examples
nav_order: 2
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: true
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Vector spaces 

We [previously]({% link notes/vector_spaces/fields.md %}) described scalars and now we turn to 
vectors. 

### Definition

A _$k$-vector space_, or a _vector space over $k$_, is a set $V$ equipped two operations:
$$
    \begin{aligned}
        + : V \times V & \to V \\
        \cdot : k \times V & \to V
    \end{aligned}
$$
satisfying the following conditions:
- $+$ is a associative: $(v_1+v_2)+v_3 = v_1+(v_2+v_3)$. 
- $+$ is commutative: $v_1 + v_2 = v_2 + v_1$. 
- There is an element $0 \in V$ with $0 + v = v + 0 = 0$ for any $v \in V$. 
- For any element $v \in V$, there is another $-v$ with $v + (-v) = (-v) + v = 0$. 
- $\cdot$ distributes over (both) $+$: 
$$
    c \cdot (v_1 + v_2) = c\cdot v_1 + c \cdot v_2
$$
and 
$$
    (c_1 + c_2) \cdot v = c_1 \cdot v + c_2 \cdot v
$$
- $1 \cdot$ is the identity: 
$$
    1 \cdot v = v 
$$
for all $v \in V$. 
- Finally, $\times$ in $k$ and $\cdot$ have the following relation 
$$
    (c_1 \times c_2) \cdot v = c_1 \cdot (c_2 \cdot v)
$$

Elements of a vector space $V$ are called _vectors_. 

The conditions on $+$ for $V$ are reminiscent of what we saw for fields. 

However, $\cdot$ is a bit different. It takes two different inputs: one a scalar from $k$ 
and the other a vector from $V$. We can translate the identity 
$$
    (c_1 \times c_2) \cdot v = c_1 \cdot (c_2 \cdot v)
$$
as saying: scaling by the product of $c_1$ and $c_2$ is the same as scaling by $c_2$ 
and then scaling the result by $c_1$. 

### Examples 

- Any field is a vector space over itself. Indeed, we can take $\cdot = \times$. For the case 
of $k = \mathbb{R}$, 

- For any field $k$, the set consisting of a single point is a vector space over $k$. Let's 
suggestively call that point $0$. Then we set $0+0 = 0$

- For $k = \mathbb{R}$, the Euclidean spaces $\mathbb{R}^n$ are vector spaces. In general, for a 
field $k$, we have a vector space $k^n$ consisting of length $n$ lists of elements of $k$. 
Addition is 
$$
    \begin{pmatrix} 
        v_1 \\
        v_2 \\
        \vdots \\
        v_n 
    \end{pmatrix} + 
    \begin{pmatrix} 
        w_1 \\
        w_2 \\
        \vdots \\
        w_n 
    \end{pmatrix} = 
    \begin{pmatrix} 
        v_1+w_1 \\
        v_2+w_2 \\
        \vdots \\
        v_n+w_n 
    \end{pmatrix}
$$
and scalar multiplication is given by 
$$
    c \begin{pmatrix} 
        v_1 \\
        v_2 \\
        \vdots \\
        v_n 
    \end{pmatrix} = 
    \begin{pmatrix} 
        cv_1 \\
        cv_2 \\
        \vdots \\
        cv_n 
    \end{pmatrix}
$$
analogously to the case $k = \mathbb{R}$. 

- Given an $m \times n$ matrix $A$ and vector $\mathbf{b} \in k^m$, the null space $\mathcal Z(A)$ 
is a $k$-vector space. We will use vector addition and scalar multiplication. To verify we 
indeed have a vector space, we need to check that:
    - if $\mathbf{v}, \mathbf{w} \in \mathcal Z(A)$ then $\mathbf{v} + \mathbf{w} \in \mathcal Z(A)$ and
    - if $\mathbf{v} \in \mathcal Z(A)$, then $c \mathbf{v} \in \mathcal Z(A)$ 

    We remember that $\mathbf{v} \in \mathcal Z(A)$ is another way to state that $A \mathbf{v} = \mathbf{0}$. 
    So we can translate the previous statements into 
    - if $A \mathbf{v} = \mathbf{0}$  $A\mathbf{w} = \mathbf{0}$ then $A(\mathbf{v} + \mathbf{w}) = \mathbf{0}$ and
    - if $A \mathbf{v} = \mathbf{0}$, then $A(c \mathbf{v}) = \mathbf{0}$ 

    Since matrix multiplication is distributive over addition, we have 
    $$
        A(\mathbf{v} + \mathbf{w}) = A \mathbf{v} + A \mathbf{w} = \mathbf{0}
    $$
    if $A \mathbf{v}, A \mathbf{w} = \mathbf{0}$. 

    Similarly, since $Ac = cA$ for a scalar $c$ and a matrix $A$, we have
    $$
        A(c\mathbf{v}) = c A(\mathbf{v}) = \mathbf{0}
    $$
    if $A \mathbf{v} = \mathbf{0}$. 

    This example is a case of [more general statement]({% link notes/vector_spaces/subspaces.md %}). 

- We can contrast the previous example with the case of $\mathcal Z(A \mid \mathbf{b})$ for 
$\mathbf{b} \neq \mathbf{0}$. Consider $x+y = 1$. Then, $(1 \ 0)^T$ is a solution but 
$2 (1 \ 0)^T = (2 \ 0)$ is not! 

    Solutions to the homogeneous system $A \mathbf{x} = \mathbf{0}$, ie null spaces, are vector spaces but 
    solutions to an inhomogeneous system are never vector spaces. 

- We know that $\mathcal R(A)$ is a vector space since we 
[know]({% link notes/solving_linear_systems/equations_for_solvable_systems.md %}) there is another 
matrix $B$ with $\mathcal R(A) = \mathcal Z(B)$. 

- Let $\operatorname{Mat}_{m,n}(k)$ be the set of $m \times n$ matrices with entries in the field $k$. 
This is a $k$-vector space with matrix addition and scalar multiplication. 

- There are also more exotic examples. Let 
$$
    \operatorname{Fun}(\mathbb{R},\mathbb{R}) = \lbrace f: \mathbb{R} \to \mathbb{R} \rbrace
$$
be the set of all real-valued functions of one variable with domain all of $x$. Some examples of elements 
include 
$$
    e^x, \ 5x^5 + 4x^4 + 3x^3 + 2x^2 + x + 1, \ \frac{1}{1+x^2}, \sin(x),\ldots
$$
This is a $\mathbf{R}$-vector space with 
$$
    (f+g)(x) := f(x) + g(x) 
$$
and scalar multiplication 
$$
    (cf)(x) := cf(x)
$$
The element $0$ is the constant function with value $0$. 
