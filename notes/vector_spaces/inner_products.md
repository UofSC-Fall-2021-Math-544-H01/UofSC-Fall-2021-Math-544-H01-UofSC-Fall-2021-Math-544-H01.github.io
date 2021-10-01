---
layout: page
title: Inner products
nav_order: 8
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Inner products

One aspect of vector algebra that we mentioned initially but have not revisited is the
[scalar product of vectors]({% link notes/solving_linear_systems/vectors.md %}#multiplication-of-vectors).

We want to abstract the properties of scalar product into a structure that we can study. 

**Definition**. Let $V$ be a $k$-vector space. Then an _inner product_ on $V$ is a function
$$
    \langle - , - \rangle : V \times V \to k 
$$
satisfying the following three conditions. 
- $\langle - , - \rangle$ is _bilinear_, ie linear in each entry. In other words
$$
    \begin{aligned}
        \langle c_1v_1+c_2v_2 , w \rangle & = c_1\langle v_1 , w \rangle + c_2\langle v_2 , w \rangle \\
        \langle v , c_1w_1+c_2w_2 \rangle & = c_1\langle v , w_1 \rangle + c_2\langle v , w_2 \rangle
    \end{aligned}
$$
- $\langle - , - \rangle$ is _symmetric_: 
$$
    \langle v , w \rangle = \langle w , v \rangle
$$
- And $\langle - , - \rangle$ is _non-degenerate_: for any $v \in V$ with $v \neq 0$ there is some $w$ 
for which 
$$
    \langle v , w \rangle \neq 0. 
$$

Two vectors $v,w$ are said to be _orthogonal_ if 
$$
    \langle v, w \rangle = 0 
$$

A set of vectors $v_1,\ldots,v_s$ is called _orthonormal_ if each $v_i$ and $v_j$ are orthogonal for $i \neq j$ 
and $\langle v_i, v_i \rangle = 1$. 

### Examples

- The scalar product in $\mathbb{R}^m$ or on $\mathbb{Q}^m$ satisfies all three properties. Recall that 
the formula is 
    $$
    \begin{pmatrix} v_1 & v_2 & \cdots & v_m \end{pmatrix} 
    \begin{pmatrix} 
        w_1 \\
        w_2 \\
        \vdots \\
        w_m 
    \end{pmatrix} 
    := \sum_{i=1}^m v_i w_i.
    $$
    If we write $v$ and $w$ as column vectors, this can be succinctly expressed using matrix multiplication: $v^T w$. 

    This is linear thanks to the properties of matrix algebra:
    $$
        (c_1v_1+c_2v_2)^T w = (c_1v_1^T + c_2v_2^T)w = c_1v_1^Tw + c_2v_2^T w \\
        v^T (c_1w_1+c_2w_2) = c_1v^Tw_1 + c_2v^T w_2
    $$  

    This is symmetric as 
    $$
        \sum_{i=1}^m v_i w_i = \sum_{i=1}^m w_i v_i
    $$

    Finally, it is non-degenerate. If 
    $$
        v^Tv = v_1^2 + v_2^2 + \cdots + v_m^2 = 0
    $$
    then since $v_i^2 \geq 0$ we know that each $v_i = 0$. Thus $v$ is its own witness, through the product, that 
    it is nonzero. 

- Let's consider the vector space of continuous real-valued functions $[0,1] \to \mathbb{R}$ with 
    $$
        \langle f(x), g(x) \rangle = \int_0^1 f(t)g(t) \ dt. 
    $$
    Thanks to the properties we remember from calculus we know this is linear. It is also clearly symmetric. 

    For non-degeneracy, we again consider 
    $$
        \langle f(x), f(x) \rangle = \int_0^1 f(t)^2 \ dt.
    $$
    If $f(x) \neq 0$ for all $x$, then, due to continuity of $f$, there is a $x_0 \in [0,1]$ and 
    an $\epsilon > 0$ with $f(x) \neq 0$ for all $x_0 - \epsilon < x < x_0 + \epsilon$. We can break up 
    $$
        \int_0^1 f(t)^2 \ dt =  \int_0^{x_0-\epsilon } f(t)^2 \ dt  + \int_{x_0-\epsilon }^{x_0+\epsilon } f(t)^2 \ dt +
        \int_{x_0+\epsilon }^1 f(t)^2 \ dt
    $$
    Since $f(x) > 0$ on $[x_0-\epsilon,x_0+\epsilon]$, 
    $$
        \int_{x_0-\epsilon }^{x_0+\epsilon } f(t)^2  > 0
    $$
    The other two terms in the sum are $\geq 0$ always. Thus, 
    $$
        \int_{0}^{1} f(t)^2  > 0.
    $$

- Let $M_n(\mathbb{R})$ be the vector space of $n \times n$ matrices with entries in $\mathbb{R}$. We use 
    $$
        \langle A, B \rangle = \operatorname{tr}(A^TB)
    $$
    where the _trace_ of $A$ is the sum of its diagonal entries
    $$
        \operatorname{tr}(A) = \sum_{i=1}^n a_{ii}
    $$

    An explicit formula for $ \operatorname{tr}(A^TB)$ is 
    $$
        \operatorname{tr}(A^TB) = \sum_{i,j=1}^n a_{ij}b_{ij}
    $$

    Thus, if we identify $M_n(\mathbb{R})$ with $\mathbb{R}^{n^2}$ by listing out all the entries of $A$, we see this is 
    just a special way to write the scalar product of the corresponding vectors in $\mathbb{R}^{n^2}$.

    This also works to give $M_n(\mathbb{Q})$ an inner product. 

- For the general fields $k$, we still have inner product on $k^m$ given by scalar multiplication. 
    It is straightforward to see it is linear and symmetric. Non-degeneracy is a little different. 

    Let's see how for $\mathbb{C}^2$. Note that we can have nonzero vectors $w \in \mathbb{C}^2$ with $w^T w = 0$. For example, 
    $$
        \begin{pmatrix} 1 & \imath \end{pmatrix}  \begin{pmatrix} 1 \\ \imath \end{pmatrix} = 1^2 + \imath^2 = 1-1 =0
    $$
    We can instead use the _complex conjugate_ $$\overline{a + b \imath} := a - b \imath$$. For vector $w$ we can take the complex 
    conjugate of all the components. We write this as $\overline{w}$. Then, one can check that if
    $$
        \overline{w}^T w = 0 
    $$
    we must have $w = 0$. Sometimes when we work over the complex numbers one uses a _Hermitian inner product_ which satisfies 
    the same conditions except
    $$
        \langle v, c w \rangle = \overline{c} \langle v, w \rangle 
    $$
    instead of 
    $$
        \langle v, c w \rangle = c \langle v, w \rangle
    $$
    The product $w^T \overline{w}$ is a Hermitian inner product. 

    Now let's see how it works in $\mathbb{F}_2^2$. We only have four vectors 
    $$
        \begin{pmatrix} 0 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 0 \\ 1 \end{pmatrix},
        \begin{pmatrix} 1 \\ 1 \end{pmatrix}
    $$
    For each of the nonzero vectors, we can find another one whose pairing with it is nonzero. For 
    $$
        \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 0 \\ 1 \end{pmatrix}
    $$
    we can use the vectors themselves. For 
    $$
        \begin{pmatrix} 1 \\ 1 \end{pmatrix}
    $$
    we can use either 
    $$
        \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 0 \\ 1 \end{pmatrix}
    $$

- One can have multiple inner products on a single vector space. Let's take $\mathbb{R}^n$ and an $n \times n$ 
    invertible symmetric matrix $A$. Recall that symmetric means $A^T = A$. 

    Then, 
    $$
        \langle v, w \rangle := v^T A w 
    $$
    is also an inner product. Linearity follows from the properties of matrix algebra as before. 

    For symmetry, we compute 
    $$
        \langle w, v \rangle = w^T A v = w^T A^T v = (Aw)^T v = v^T A w
    $$
    where we use the symmetry $u^T v = v^T u$ from before. 

    Finally, for non-degeneracy, we have 
    $$
        \langle v, A^{-1} v \rangle = v^T A A^{-1} v = v^T v
    $$ 
    which saw only vanished if $v = 0$. 

### Facts 

Given a finite dimensional vectors space $V$ with a bilinear function 
$$
\langle -,- \rangle : V \times V \to k 
$$
we can choose a basis 
$v_1,\ldots,v_d$ and get a $d \times d$ matrix
$$
    A_{ij} := \langle v_i, v_j \rangle 
$$

If we write $v,w  \in V$ in terms of the 
basis 
$$
    v = x_1 v_1 + \cdots + x_d v_d \\
    w = y_1 v_1 + \cdots + y_d v_d
$$
then we have 
$$
    \langle v, w \rangle = \begin{pmatrix} x_1 & \cdots & x_d \end{pmatrix} A \begin{pmatrix} y_1 \\ \vdots \\ y_d \end{pmatrix} = x^T A y
$$

For example, the standard scalar product on $k^m$ would just output the identity matrix $I_d$.

**Lemma**. $\langle -,- \rangle$ is symmetric if and only $A = A^T$. 

{% include beginproof.html %}
Since 
$$
    \langle v_i, v_j \rangle = \langle v_j, v_i \rangle 
$$
we have $A_{ij} = A_{ji}$ or $A^T = A$.
{% include endproof.html %}

Next, we can check that if we have special type of basis, one that is orthonormal, we know our pairing is 
actually non-degenerate. 

**Lemma**. Let $V$ be a vector space with a symmetric and bilinear pairing
$$
    \langle - , - \rangle : V \times V \to k.
$$
If we have an orthonormal basis for $V$, then $\langle -, - \rangle$ is 
non-degenerate, and hence a inner product. 

{% include beginproof.html %}
Lets write $v \in V$ as 
$$
    v = a_1 v_1 + \cdots a_d v_d
$$
in terms of the orthogonal basis. If $v \neq 0$, then some $a_i \neq  0$. 
We have 
$$
    \langle v , v_i \rangle = \sum_{j=1}^d a_j\langle v_j, v_i \rangle = a_i
$$
from orthonormality. 
{% include endproof.html %}

**Corollary**. Scalar multiplication of vectors in $k^m$ is a inner product 
for any field $k$.

{% include beginproof.html %}
The standard basis for $k^m$ is an orthonormal basis for scalar multiplication of 
vectors. 
{% include endproof.html %}