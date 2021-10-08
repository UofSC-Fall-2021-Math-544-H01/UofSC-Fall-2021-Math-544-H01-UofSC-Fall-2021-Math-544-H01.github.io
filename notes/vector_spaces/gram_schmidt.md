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

## Making orthonormal bases

If we have a inner product $\langle - , - \rangle$ on a vector space $V$ and we locate a 
basis $v_1,\ldots,v_d$, then generally it will not be orthonormal. 

For example, take $V = k^3$ for a field $k$. The collection 
$$
    \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}
$$
is a basis but none of the pairs of vectors in it is orthogonal for the standard inner product 
$\langle v,w \rangle = v^T w$. 

Moreover, starting from a basis $v_1,\ldots,v_d$, we know that we can 
- swap any pair,
- scaled any vector by a nonzero scalar, or 
- add a multiple of one vector to a different one 

and still have a basis in the end. 

If we started with an orthonormal basis, then, of these three classes of operations, only 
swapping a pair and scaling a vector by $\pm 1$ will output a new orthonormal basis. This is 
pretty constraining. Said another way, orthonormal bases are _very special_.

Orthonormal bases can be very useful, however, especially computationally. So figuring 
out a way to product an orthonormal basis from a general basis is useful. 

The most well-known way is the _Gram-Schmidt algorithm_. Before we state, we want to recall 
one condition on inner product. The following only makes sense if we have some ordering 
on the field $k$. Therefore, we will restrict attention to $k = \mathbb{R}$.

**Definition**. An inner product $\langle -, - \rangle$ on a vector space over $\mathbb{R}$ 
is called _positive definite_ if 
$ \langle v, v \rangle > 0$ for any $v \in V$ with $v \neq 0$. 

**Example**. Let $A$ be an invertible $n \times n$ matrix with $\mathbb{R}$ entries. 
Then, the inner product 
$$
    \langle v, w \rangle := (Av)^T (Aw) = v^T A^TA w
$$
is a positive definite inner product on $\mathbb{R}^n$. Since 
$$
    \langle v, v \rangle = (Av)^T Av \geq 0
$$
from the standard inner product on $\mathbb{R}^m$.

### The Gram-Schmidt Algorithm 

The inputs to Gram-Schmidt are a vector space $V$ with a positive definite inner product 
$\langle -, - \rangle$ and a basis for $V$. The output is an 
orthonormal basis $w_1,\ldots,w_d$. 

1. Establish an ordering for your basis $v_1,\ldots,v_d$.

2. Define 
$$
    u_i := v_i - \sum_{j=1}^{i-1} \frac{\langle v_i, v_j \rangle}{\langle v_j, v_j \rangle} v_j 
$$

3. Set  
$$
    w_i := \frac{1}{\sqrt{\langle u_i, u_i \rangle}} u_i
$$

Note that 
$$
    w_1 := \frac{1}{\sqrt{\langle v_1, v_1 \rangle}} v_1
$$
by definition. 

**Lemma**. Step 2 is well-defined. In other words, we are not dividing by anywhere. 

{% include beginproof.html %}
Since $\langle -,- \rangle$ is positive definite, to know that $\langle v_i, v_i \rangle \neq 0$ 
we only need to check that $v_i \neq 0$. But, the zero vector can never be part of basis since 
$1 \cdot 0 = 0$ is a nontrivial linear relation. 
{% include endproof.html %}

**Lemma**. Step 3 is well-defined. 
{% include beginproof.html %}
If $u_i = 0$, then 
$$
    v_i - \sum_{j=1}^{i-1} \frac{\langle v_i, v_j \rangle}{\langle v_j, v_j \rangle} v_j = 0
$$
is a nontrivial linear relation amongst elements of a basis. This is a contradiction so 
we conclude $u_i \neq 0$. Thus, $\langle u_i, u_i \rangle \neq 0$ by positive definiteness. 
{% include endproof.html %}

Next, let's check that we actually still have a spanning set for $V$. It helps to 
establish a more general statement. 

**Proposition**. For any $1 \leq i \leq d$, we have 
$$
   \operatorname{Span}(v_1,\ldots,v_i) = \operatorname{Span}(w_1,\ldots,w_i)
$$
In particular, $w_1,\ldots,w_d$ spans $V$ and must be a basis. 

{% include beginproof.html %}
We proceed by induction on $i$. Since $w_1$ is a scalar multiple of $v_1$, they have 
the same span. 

Assume that we know 
$$
   \operatorname{Span}(w_1,\ldots,w_j) = \operatorname{Span}(v_1,\ldots,v_j)
$$
for any $1 \leq j < i$. 

Let's show that 
$$
    v_i \in \operatorname{Span}(w_1,\ldots,w_i).
$$
We can rewrite 
$$
    u_i = v_i - \sum_{j = 1}^{i-1} \langle v_i, w_j \rangle w_j 
$$
as 
$$
    \begin{aligned}
        v_i = u_i + \sum_{j = 1}^{i-1} \langle v_i, w_j \rangle w_j \\
        v_i = \langle u_i, \rangle u_i \rangle w_i + \sum_{j = 1}^{i-1} \langle v_i, w_j \rangle w_j
    \end{aligned}
$$
This shows that 
$$
    v_i \in \operatorname{Span}(w_1,\ldots,w_i).
$$

From the induction hypothesis, we know that 
$$
    v_1,\ldots,v_{i-1} \in \operatorname{Span}(v_1,\ldots,v_i) = \operatorname{Span}(w_1,\ldots,w_{i-1})
$$
Since $v_1,\ldots,v_i \in \operatorname{Span}(w_1,\ldots,w_i)$ and we 
[know]({% link notes/vector_spaces/spans.md %}#consequences) that 
the span of $v_1,\ldots,v_i$ is the smallest subspace containing 
$v_1,\ldots,v_i$ we have 
$$
    \operatorname{Span}(v_1,\ldots,v_i) \subseteq \operatorname{Span}(w_1,\ldots,w_i)
$$

Next, let's check that 
$$
    w_i \in \operatorname{Span}(v_1,\ldots,v_i)
$$
Since 
$$
    u_i = v_i - \sum_{j = 1}^{i-1} \langle v_i, w_j \rangle w_j 
$$
we have 
$$
    u_i \in \operatorname{Span}(w_1,\ldots,w_{i-1},v_i).
$$
As $w_1,\ldots,w_{i-1} \in \operatorname{Span}(v_1,\ldots,v_{i-1})$, 
any linear combination of $w_1,\ldots, w_{i-1}$ can be rewritten as 
a linear combination of $v_1,\ldots,v_{i-1}$. So we have  
have 
$$
    u_i \in \operatorname{Span}(w_1,\ldots,w_{i-1},v_i) \subseteq 
    \operatorname{Span}(v_1,\ldots,v_{i-1},v_i)
$$
As $w_i = \langle u_i, u_i \rangle u_i$, we are just scaling the coefficients in the linear 
combination given $u_i$. So we stay in the span 
$$
    w_i \in \operatorname{Span}(v_1,\ldots,v_{i-1},v_i)
$$

Thus, $w_1,\ldots,w_i \in \operatorname{Span}(v_1,\ldots,v_{i-1},v_i)$ and so 
$$
    \operatorname{Span}(w_1,\ldots,w_i) \subseteq \operatorname{Span}(v_1,\ldots,v_i)
$$

We can conclude that 
$$
   \operatorname{Span}(v_1,\ldots,v_i) = \operatorname{Span}(w_1,\ldots,w_i)
$$

Since $v_1,\ldots,v_d$ is a basis, we have 
$$
    V = \operatorname{Span}(v_1,\ldots,v_d) = \operatorname{Span}(w_1,\ldots,w_d)
$$
and $w_1,\ldots,w_d$ also spans. If $w_1,\ldots,w_d$ were not a basis, then 
some subset of it would be. This would make $\dim V < d$ giving a contradiction. 
{% include endproof.html %}

All that is left is to check that $w_1,\ldots,w_d$ forms an orthonormal set. 

Let's check that we actually get an orthonormal set. Before we do that, it is 
useful to check something more general. Recall from 
[Homework 8]({% link homework/08.md %}) we have the orthogonal of a subspace 
$U \subseteq V$ given by 
$$
    U^{\perp} = \lbrace v \in V \mid \langle v, u \rangle = 0 \ \forall u \in U \rbrace. 
$$



**Lemma**. The output of Gram-Schmidt is an orthonormal set of vectors. 

{% include beginproof.html %}
Note that each $w_i$ satisfies 
$$
    \langle w_i, w_i \rangle = \left\langle \frac{1}{\sqrt{\langle u_i, u_i \rangle} u_i, \sqrt{\langle u_i, u_i \rangle} u_i} = 
    \frac{\langle u_i, u_i \langle}{\langle u_i, u_i \langle} = 1
$$

Now we prove be induction that $w_1,\ldot,w_i$ is orthonormal. For the case of $i=1$, there is nothing prove. 

Assume that we know that $w_1,\ldots,w_{i-1}$ is an orthonormal set. Let's compute $\langle w_i, w_j \rangle$ for $j < i$. 
We have 
$$
    \langle w_i, w_j \rangle = \frac{1}{\langle u_i,u_i \rangle} \langle u_i, w_j \rangle =  
    \frac{1}{\langle u_i,u_i \rangle}\left( \langle v_i, w_j  \right)
$$
{% include endproof.html %}


**Lemma**. We can write $u_i$ in closed form as 
$$
    u_i := v_i - \sum_{j = 1}^{i-1} \langle v_i, w_j \rangle w_j 
$$

{% include beginproof.html %}

{% include endproof.html %}


The following will help. Note that we don't yet know that we are not dividing by $0$ in 
$$
    w_i := \frac{1}{\sqrt{\langle u_i, u_i \rangle}} u_i
$$


**Lemma**. Let $\langle -,- \rangle$ be a positive definite inner product on a vector space. 
If $w_1,\ldots,w_i$ is a set of nonzero orthogonal vectors, then 
it is a linearly independent. In particular, if $\dim V = d$, and $i = d$, 
it is a basis.  

{% include beginproof.html %}
Assume we have a relation 
$$
    0 = a_1 w_1 + \cdots + a_i w_i
$$
For each $1 \leq j \leq i$, we have 
$$
    0 = \langle 0, w_j \rangle = a_1 \langle w_1, w_j \rangle + \cdots + a_i \langle w_i, w_j \rangle 
    = a_j \langle w_j, w_j \rangle 
$$
Since $\langle w_j, w_j \rangle \neq 0$, we see that $a_j = 0$. Thus, $w_1,\ldots,w_i$ are 
linearly independent.

If $\dim V = d$ and $i=d$, then since $w_1,\ldots,w_d$ spans, we 
[know]({% link notes/vector_spaces/bases.md %}#consequences)
it must be a basis. 
{% include endproof.html %}





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