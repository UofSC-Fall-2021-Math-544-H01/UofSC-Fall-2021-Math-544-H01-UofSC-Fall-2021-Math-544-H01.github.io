---
layout: page
title: In Bases
nav_order: 3
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Linear Transformations in Bases

Given a linear transformation $T: V \to W$, we can completely capture all of its 
information by just knowing what the image is of a basis set for $V$. 

**Lemma**. Suppose $S,T : V \to W$ are two linear transformation between 
$k$-vector space and that $v_i$ for $i \in B$ is a basis for the vector 
space $V$. If 
$$
    S(v_i) = T(v_i) 
$$
for all $i \in B$, then $S(v) = T(v)$ for any $v \in V$. 

{% include beginproof.html %}
For any $v \in V$, we can write it as a sum 
$$
    v = \sum_{i \in B} c_i v_i 
$$
with only finitely many of the $c_i \neq 0$. Since $S$ is a linear transformation, we 
have 
$$
    S(v) = \sum_{i \in B} c_i S(v_i) 
$$
From our assumption, 
$$
    \sum_{i \in B} c_i S(v_i) = \sum_{i \in B} c_i T(v_i) 
$$
Using the fact tht $T$ is a linear transformation, we get 
$$
    \sum_{i \in B} c_i T(v_i) = T(v) 
$$
So we can conclude that $S(v) = T(v)$. 
{% include endproof.html %}

The previous lemma tells us that two linear transformations which do the same thing 
on a basis are equal as functions. The set of values $T(v_i)$ for $i \in B$ 
completely captures all information about $T$. 

Given a linear transformation $T$, we can ask: how special are the values $T(v_i) \in W$? 
Do they have to some special property to arise as the image a linear transformation 
applied to a basis? Or can they be any possible set of vectors in $W$ indexed by $B$? 

It turns out there is no condition. Given such a collection of vectors in $W$, we 
can build a unique linear transformation from it. 

**Lemma**. Let $V$ and $W$ be $k$-vector spaces and assume we have a basis $v_i$ for 
$i \in B$ of $V$. Given any choice of vectors $w_i \in W$ for $i \in B$, there is a
unique linear transformation $T: V \to W$ with 
$$
    T(v_i) = w_i ~\text{for all } i \in B. 
$$

{% include beginproof.html %}
Remember that with a basis, we can write any $v \in V$ _uniquely_ as a linear 
combination of the $v_i$:
$$
    v = \sum_{i \in B} c_i v_i
$$
for a unique choice of scalars $c_i \in k$ and only finitely many are nonzero. 
We define
$$
    \begin{aligned}
        T : V & \to W \\
        v & \mapsto \sum_{i \in B} c_i w_i 
    \end{aligned}
$$
Since the $c_i$ are uniquely determined by $v$ and the $v_i$, this is a well-defined 
function. 

We need to check it is a linear transformation. First notice that 
$$
    cv = c\left(\sum_{i \in B} c_i v_i \right) = \sum_{i \in B} (cc_i) v_i
$$
Since this is one linear combination expressing $cv$ in terms of $v_i$ 
and there is a unique one, this must be it. By definition, 
$$
    T(cv) = \sum_{i \in B} (cc_i) w_i
$$
Pulling out the $c$ gives 
$$
    \sum_{i \in B} (cc_i) w_i = c\left(\sum_{i \in B} c_i w_i \right) = cT(v)
$$
So $T$ commutes with scalar multiplication. 

Now, we turn to addition. We write 
$$
    v = \sum_{i \in B} c_i v_i \\
    v^\prime = \sum_{i \in B} c_i^\prime v_i
$$
Then
$$
    v + v^\prime = \sum_{i \in B} (c_i+c_i^\prime) v_i
$$
By definition of $T$, we have 
$$
    T(v + v^\prime) = \sum_{i \in B} (c_i + c_i^\prime) w_i 
$$
Expanding this out gives
$$
    \sum_{i \in B} (c_i + c_i^\prime) w_i = \sum_{i \in B} c_i w_i 
    + \sum_{i \in B} c_i^\prime w_i = T(v) + T(v^\prime)
$$
So $T$ also commutes with addition. Thus, $T$ is a linear transformation. 

We have made _one_ linear transformation with $T(v_i) = w_i$ for 
all $i \in B$. The previous lemma tells us it is uniquely determined by 
this property. 
{% include endproof.html %}

So a linear transformation is completely determined by the images of a basis 
and for any choice of images of the basis we can extend the choice to 
a linear transformation with that action on the basis. 

Note that linear transformations make no reference to any basis in their 
definition but introducing a basis in their presence allows us 
great insight. If we take a basis for $W$, we arrive back at a familiar 
friend.

**Definition**. Let $T: V \to W$ be a linear transformation. Given 
bases $v_i, i \in B$ and $w_j, j \in C$, then we can uniquely write 
$$
    T(v_i) = \sum_{j \in C} A_{ji} w_j
$$
for some scalars $A_{ij} \in k$. This is called the _matrix 
representation_ of $T$ in the bases $B$ and $C$. 

If $\dim V = n$ and $\dim W = m$, then we get a familiar $m \times n$ 
matrix $A$. 

**Lemma**. Let $V$ and $W$ be $k$-vector spaces with $\dim V = n$ and 
$\dim W = m$. A linear transformation is completely determined by 
its matrix representation. Moreover, for each $m \times n$ matrix $A$, 
there is unique linear transformation $T: V \to W$ whose matrix 
representation $A$. 

{% include beginproof.html %}
Fix bases $v_1,\ldots,v_n$ for $V$ and $w_1,\ldots,w_m$ for $W$. 
If $S,T : V \to W$ have the same matrix representations, we have 
$$
    S(v_i) = T(v_i)
$$
and thus $S = T$ by a previous lemma. 

For a matrix $A$, we know there is a unique linear transformation 
$T: V \to W$ with 
$$
    T(v_i) = \sum_{j \in C} A_{ji} w_j
$$
from a previous lemma. 
{% include endproof.html %}

So the matrix representation completely determines a linear transformation. 
But, take care because the matrix representation of $T$ depends 
very much on which bases we choose for $V$ and $W$. 

**Example**. Consider the matrix 
$$
    A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix}
$$
As we have seen, this determines a linear transformation 
$$
    \begin{aligned}
        T: \mathbb{R}^3 & \to \mathbb{R}^2 \\
        \mathbf{v} & \mapsto A \mathbf{v}
    \end{aligned}
$$
If we take the standard bases for both $\mathbb{R}^3$ and $\mathbb{R}^2$, 
then matrix representation of $T$ is exactly $A$. 

But what happens if we take different bases? Let's take the basis 
$$
    v_1 := \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}, 
    v_2 := \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix},
    v_3 := \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}
$$
for $\mathbb{R}^3$ and 
$$
    w_1 := \begin{pmatrix} 1 \\ -1 \end{pmatrix},
    w_2 := \begin{pmatrix} 1 \\ 1  \end{pmatrix}
$$
for $\mathbb{R}^2$. 

To determine the matrix representation in our a new bases, we first compute
$$
    Av_1 = \begin{pmatrix} 1 \\ 4 \end{pmatrix} \\
    Av_2 = \begin{pmatrix} 3 \\ 7 \end{pmatrix} \\
    Av_3 = \begin{pmatrix} 6 \\ 15 \end{pmatrix} 
$$

Now, 

We can compute this using our 
[change of basis matrices]({% link notes/vector_spaces/bases.md %}). 
We know that what $T$ looks like in the standard bases $e_1,e_2,e_3$ 
and $e_1,e_2$. If we compute matrix $C$ that changes bases from 
$e_1,e_2,e_3$ to $v_1,v_2,v_3$ and the matrix $D$ that changes 
bases from $w_1,w_2$ to $e_1,e_2$, then the product $DAC$ will be 
the matrix representation for $A$ for $v_1,v_2,v_3$ and $w_1,w_2$. 

The change of basis matrix from $e_1,e_2,e_3$ to $v_1,v_2,v_3$ is 
simply
$$
    \begin{pmatrix} 
        1 & 1 & 1 \\
        0 & 1 & 1 \\
        0 & 0 & 1
    \end{pmatrix}
$$
The matrix that changes from $w_1,w_2$ to $e_1,e_2$ is the _inverse_ to 
$$
    \begin{pmatrix} 
        1 & 1 \\
        -1 & 1 
    \end{pmatrix}
$$
which is 
$$
    \frac{1}{2} \begin{pmatrix} 
        1 & -1 \\
        1 & 1 
    \end{pmatrix}
$$

Thus 
$$
    \frac{1}{2} \begin{pmatrix} 
        1 & -1 \\
        1 & 1 
    \end{pmatrix}
    \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix}
    \begin{pmatrix} 
        1 & 1 & 1 \\
        0 & 1 & 1 \\
        0 & 0 & 1
    \end{pmatrix} =
    \frac{1}{2} \begin{pmatrix} 
        -3 & -6 & -9 \\
        5 & 12 & 21
    \end{pmatrix} 
$$
is the matrix representation of $T$ in the new bases. 

Some words for caution:
- One linear transformation can have many matrix representations! It 
all depends on the bases. 
- One matrix can give many different linear transformations! It all 
depends on the bases. 

Two matrices that differ by changing bases represent the same 
linear transformation and therefore share many features in common. 
In particular, if we have any idea or property we can derive from 
the definition of a linear transformation alone (no bases allowed), 
then these two matrices should share that idea or property. 

We will look at what some of these properties can be 
[soon]({% link notes/linear_transformations/kernels_ranges.md %}). 
But to discuss these relationships properly we need a new notion 
relating vector spaces: 
[isomorphisms]({% link notes/linear_transformations/isomorphisms.md %})
