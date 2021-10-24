---
layout: page
title: Definitions and examples
nav_order: 2
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Linear Transformations

**Definition**. A function $T: V \to W$ between two $k$-vector spaces 
$V$ and $W$ is a _linear transformation_ if 
- $T$ commutes with scalar multiplication: 
$$
    T(cv) = cT(v) 
$$
for all $c \in k$ and all $v \in V$ and 
- $T$ commutes with addition of vectors:
$$
    T(v_1 + v_2) = T(v_1) + T(v_2)
$$
for all $v_1,v_2 \in V$. 

As indicated by the example below, you have seen many linear transformations 
in your life already and they all do not arise a priori as multiplication 
by a matrix. 

Linear transformations provide the right abstraction for drawing conclusions 
as we would for matrix multiplication but in a broader context. 

### Examples 

- For any vector space $V$, the identity map 
$$
    \begin{aligned}
        \operatorname{Id}_V : V & \to V \\
        v & \mapsto v
    \end{aligned}
$$
is a linear transformation. 

- Multiplication by a matrix is a linear transformation. We know from 
matrix algebra that 
$$
    A(cx) = cAx
$$
and that 
$$
    A(x + y) = Ax + Ay
$$
for vectors $x,y$. But we can also multiply matrices by matrices. 

    Take the vector space $\operatorname{Mat}_{m,n}(k)$ of $m \times n$ 
    matrices with entries in a field $k$ and let $A$ be a $m \times m$ matrix. Then, 
    we get a function
    $$
        \begin{aligned}
            \operatorname{Mat}_{m,n}(k)  & \to \operatorname{Mat}_{m,n}(k)  \\
            B & \mapsto AB
        \end{aligned}
    $$
    This is also a linear transformation. Again, we know that scalar multiplication 
    commutes with matrix multiplication so 
    $$
        A(cB) = cAB
    $$
    and we know that we can distribute multiplication over addition of matrices 
    $$
        A(B+C) = AB + AC
    $$
    Thus, we have a linear transformation. 

- Transpose is a linear transformation. We have 
$$
    (cA)^T = cA^T
$$
and 
$$
    (A+B)^T = A^T + B^T
$$

- Differentiation is a linear transformation. We recall from calculus that 
$$
    \frac{d}{dx} (cf) = c \frac{df}{dx}
$$
and 
$$
    \frac{d}{dx}(f + g) = \frac{df}{dx} + \frac{dg}{dx}
$$

- Integration is a linear transformation. Again from calculus we know that 
$$
    \int cf(x) \ dx = c \int f(x) \ dx 
$$
and 
$$
    \int f(x) + g(x) \ dx = \int f(x) \ dx + \int g(x) \ dx. 
$$

- If we have a bilinear pairing $\langle -,- \rangle$ on a vector space $V$ and 
a vector $v \in V$, we can make a function 
$$
    \begin{aligned}
        V & \to k \\
        w & \mapsto \langle v,w \rangle 
    \end{aligned}
$$
This is a linear transformation since 
$$
    \langle v, c_1w_1 + c_2w_2 \rangle = c_1 \langle v,w_1 \rangle + c_2 \langle v,w_2 \rangle 
$$
Supping this up a little, given a subspace $U \subseteq V$, then the projection 
$$
    \operatorname{proj}_U : V \to U
$$
is a linear transformation. 

- More geometrically, rotations and reflections in the plane are linear transformations. Try 
to visualize this. 

- For something that is not a linear transformation, take a look at 
$$
    \begin{aligned}
    \mathbb{R} & \to \mathbb{R} \\
    x & \mapsto x^{10}
    \end{aligned}
$$  
We don't preserve scaling since 
$$
    (5x)^{10} = 5^{10} x^{10} \neq 5 x^{10}
$$
for $x \neq 0$. 

- Another, more physical, example of a nonlinear transformation is falling. If $h(t)$ is the 
height off the ground after $t$ seconds of falling from a plane, then $h(t)$ is a not linear 
function. For a linear function, the distance you fall from time $t = 0$ to $t=1$ is the same 
as that from $t=1$ to $t=2$. But, due to gravity's acceleration, you speed up and fall faster 
the longer you fall. 


### Properties

**Lemma**. The following statements are equivalent for a function $T: V \to W$ between 
$k$-vector spaces $V$ and $W$.
- $T$ is a linear transformation,
- $T$ preserves linear combinations:
$$
    T\left( \sum c_i v_i \right) = \sum c_iT(v_i)
$$
- $T$ preserves linear combinations of two vectors. 

{% include beginproof.html %}
Assume that $T$ is a linear transformation. Then using induction we can show that 
$$
    T(\sum v_i) = \sum T(v_i)
$$
So 
$$
    T(\sum c_i v_i) = \sum T(c_iv_i) = \sum c_iT(v_i)
$$

If $T$ preserves linear combinations, then it certainly preserves linear combinations 
of two vectors. 

Finally, assume that $T$ preserves linear combinations of two vectors. Then, 
taking $v_2 = 0$ we see that 
$$
    T(c_1v_1) = c_1T(v_1)
$$
so $T$ preserves scalar multiplication. Taking $c_1,c_2 = 1$, we have 
$$
    T(v_1 + v_2) = T(v_1) + T(v_2)
$$
and $T$ preserves addition of vectors. 
{% include endproof.html %}

The next lemma can provide a quick sanity check for whether a functor could possibly be a
linear transformation. 

**Lemma**. If $T$ is a linear transformation, the $T(0) = 0$. In particular, functions 
that do not take the zero vector to the zero vector cannot be linear transformations. 

{% include beginproof.html %}
We have 
$$
    T(0) = T(0\cdot v) = 0 T(v) = 0. 
$$
{% include endproof.html %}