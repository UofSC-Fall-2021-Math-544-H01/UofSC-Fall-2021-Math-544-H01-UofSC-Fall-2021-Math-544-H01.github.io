---
layout: page
title: Gram Schmidt
nav_order: 9
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: false
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

**Definition**. If we have a positive definite inner product $\langle -,- \rangle$ on 
a vector space $v$, then we say the _length_ (or _norm_) of a vector $v$ is 
$$
    ||v|| := \sqrt{\langle v,v \rangle}
$$  
A vector is of _unit length_ (or is _norm one_) if $\|\|v\|\| = 1$. 

Note that $v = 0$ if and only if its norm is $\|\|v\|\| = 0$. 

### The Gram-Schmidt Algorithm 

The inputs to Gram-Schmidt are a vector space $V$ with a positive definite inner product 
$\langle -, - \rangle$ and a basis for $V$. The output is an 
orthonormal basis $w_1,\ldots,w_d$. 

1. Establish an ordering for your basis $v_1,\ldots,v_d$. Now recursively do 2 and 3.

2. Define 
$$
    u_i := v_i - \sum_{j=1}^{i-1} \langle v_i, w_j \rangle w_j 
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

**Lemma**. Suppose $u_j \neq 0$ for all $1 \leq j \leq i$. Then $w_1,\ldots,w_i$ is 
an orthonormal set. 

{% include beginproof.html %}
Note that from our assumption 
$$
    w_j := \frac{1}{\sqrt{\langle u_j,u_j \rangle}}u_j 
$$
is well-defined for each $1 \leq j \leq i$. 

We have 
$$
    \langle w_j, w_j \rangle = \left \langle \frac{1}{\sqrt{\langle u_j, u_j \rangle}} u_j, 
    \frac{1}{\sqrt{\langle u_j, u_j \rangle}} u_j \right \rangle 
    = \frac{\langle u_j, u_j \rangle}{\langle u_j, u_j \rangle} = 1
$$

Next we prove that $w_1,\ldots,w_j$ is an orthogonal set for each $1 \leq j \leq i$. 
We work using induction. For the base case of $j = 1$ there is nothing to prove. 

Assume that $w_1,\ldots,w_{j-1}$ is an orthogonal set. We want to 
show that $w_1,\ldots,w_j$ is an orthogonal. From the induction hypothesis, 
we know that $\langle w_r, w_s \rangle = 0$ for $1 \leq r,s \leq j-1$. We 
need to check that $\langle w_r, w_j \rangle = 0$. 
$$
    \begin{aligned}
        \langle w_r , w_j \rangle & = \langle u_j, u_j \rangle \langle w_r, v_j - 
        \sum_{s =1}^{j-1} \langle v_j, w_s \rangle w_s \rangle \\ 
        & = \langle u_j, u_j \rangle \left( \langle w_r, v_j \rangle - \sum_{s=1}^{j-1} 
        \langle v_j, w_s \rangle \langle w_r, w_s \rangle \right)
    \end{aligned}  
$$
Since $w_1,\ldots,w_{j-1}$ is an orthogonal set, $\langle w_r,w_s \rangle =0$ for 
$r \neq s$ and this expression simplifies as 
$$
    = \langle u_j, u_j \rangle ( \langle w_r, v_j \rangle - \langle v_j, w_r \rangle 
    \langle w_r, w_r \rangle ) = 0
$$
This is zero since $\langle -,- \rangle$ is symmetry and we already saw that 
$\langle w_r, w_r \rangle = 1$.
{% include endproof.html %}

Next we have a simple criteria for an orthogonal set to be a basis: it just has 
to have the dimension many vectors in it. 

**Lemma**. Let $\langle -,- \rangle$ be a positive definite inner product on a vector space. 
If $w_1,\ldots,w_i$ is a set of nonzero orthogonal vectors, then 
it is a linearly independent. In particular, if $\dim V = d$, and $i = d$, 
it is a basis.  

{% include beginproof.html %}
See [Worksheet 15](% link worksheet/15.md %)
{% include endproof.html %}

As corollary of the previous two results, we have the following.

**Corollary**. If $u_i \neq 0$ for $1 \leq i \leq j$, then $w_1,\ldots,w_j$ is an 
orthonormal basis for the $\operatorname{Span}(v_1,\ldots,v_j)$. 

{% include beginproof.html %}
We first check that each $w_i$ lies in the span of the $v_1,\ldots,v_i$ using 
induction. In the base case, 
$$
    w_1 = \frac{1}{\sqrt{\langle v_1,v_1 \rangle}}v_1 \in \operatorname{Span}(v_1)
$$

Assume now that $w_1,\ldots,w_{i-1} \in \operatorname{Span}(v_1,\ldots,v_{i-1})$. 
Since
$$
    w_i = \frac{1}{\sqrt{\langle u_i, u_i \rangle}}\left(v_i - 
    \sum_{s=1}^{i-1} \langle v_i, w_s \rangle w_s \right)
$$
we have written $w_i$ as a linear combination of $w_1,\ldots,w_{i-1}$ and $v_i$. 
Since we can write each $w_1,\ldots,w_{i-1}$ as a linear combination of 
$v_1,\ldots,v_{i-1}$, we can substitute those in and simplify to get $w_i$ as 
a linear combination of $v_1,\ldots,v_i$. 

Since $v_1,\ldots,v_d$ is basis, it is linearly independent. Thus, the dimension 
of the span of $v_1,\ldots,v_i$ is $i$. We also have $i$ orthogonal vectors 
in $w_1,\ldots,w_i$. Each is nonzero since we assumed that $u_j \neq 0$ for all $j$. 
Using the previous lemma, we see that $w_1,\ldots,w_i$ is a basis for 
$\operatorname{Span}(v_1,\ldots,v_i)$. 
{% include endproof.html %}

We are left with checking that each $u_i \neq 0$ so Gram-Schmidt is well defined. 

**Lemma**. Each $u_i \neq 0$ for $1 \leq i \leq d$. 

{% include beginproof.html %}
We work by induction again. For case of $i=1$, we have $v_1 \neq 0$ 
since it is a member of a basis. And $u_1 = v_1$. 

Assume that $u_j \neq 0$ for $j < i$. If $u_i = 0$, then we have 
$$
    v_i = \sum_{s=1}^{i-1} \langle v_i,w_s \rangle w_s
$$
In other words, $v_i$ is in the span of $w_1,\ldots,w_{i-1}$. But, we just saw 
that 
$$
    \operatorname{Span}(w_1,\ldots,w_{i-1}) = \operatorname{Span}(v_1,\ldots,v_{i-1})
$$
This implies that 
$$
    v_i \in \operatorname{Span}(v_1,\ldots,v_{i-1})
$$
which is a contradiction to the linear independence of $v_1,\ldots,v_i$. Thus, $u_i \neq 0$. 
{% include endproof.html %}

**Example**. Let's go back to the example a basis which is not orthonormal
$$
    v_1,v_2,v_3 := \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}
$$
and let's apply Gram Schmidt. We have $w_1=v_1$ since the length of $v_1$ is already $1$. Next we have 
$$
    u_2 = \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix} - \left\langle \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}, 
    \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix} \right\rangle \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix} = 
    \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix}
$$
Since $\|\|u_2\|\|=1$, we have $w_2 = u_2$. Finally, 
$$
    u_3 = \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix} - \left\langle \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}, 
    \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix} \right\rangle \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix} - 
    \left\langle \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}, 
    \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix} \right\rangle \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix} = 
    \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}
$$
and $w_3 = u_3$. 

So in this case we recover the standard basis. But that is not always the case. Suppose we reverse the ordering 
of our basis and run Gram Schmidt again. Then we would a different orthonormal basis
$$
    \frac{1}{\sqrt{3}} \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}, 
    \frac{\sqrt{3}}{\sqrt{2}} \begin{pmatrix} 1/3 \\ 1/3 \\ -2/3 \end{pmatrix},
    \sqrt{2} \begin{pmatrix} 1/2 \\ -1/2 \\ 0 \end{pmatrix}
$$

In Sage, you can perform Gram Schmidt on the _rows_ of a matrix $A$ by calling `A.gram_schmidt()`. 


<!-- 
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



 -->

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


<!-- Assume we have a relation 
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
it must be a basis.  -->