---
layout: page
title: Subspaces
nav_order: 3
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: false
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

### Consequences of the definition

Notice that the definition of a subspace did not say it is a vector space! That is a consequence of 
the definition.

**Proposition**. Suppose that $V$ is a $k$-vector space and $W$ is a subset of $V$. If $W$ is a 
subspace, then $W$, with addition and scaling inherited from $V$, is also a vector space. 

<details markdown="block">
<summary>
<b>Proof</b>. (Expand for details)
</summary>

Let's try to spell out what "addition and scaling inherited from $V$" is precisely. 

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
     <span style="float:right;"> &#9632; </span>

</details>

A nice aspect about the definition of a subspace is that it is usually easier to check that running the 
list of axioms for a vector space directly. We have already seen this in practice for the 
[example of a null space]({% link notes/vector_spaces/def_egs.md%}#examples). 

We can boil the check down to a single statement too. 

**Lemma**. Let $V$ be a vector space. Then the following are equivalent:
1. $W \subseteq V$ is subspace.
2. $W$ is  _closed under linear combinations_, meaning for any $w_1, \ldots, w_n \in W$ and 
$c_1,\ldots,c_n \in k$, we have 
$$
    c_1 w_1 + c_2 w_2 + \cdots + c_n w_n \in W. 
$$
3. $W$ is closed under linear combinations involving two vectors: for any $w_1,w_2 \in W$ and 
$c_1,c_2 \in k$, we have 
$$
    c_1 w_1 + c_2 w_2 \in W. 
$$

<details markdown="block">
<summary>
<b>Proof</b>. (Expand for details)
</summary>

Lets show that 1) $\Rightarrow$ 2). Assume that $w_1 + w_2 \in W$ if $w_1, w_2 \in W$ and 
$c \cdot w \in W$ if $c \in k$ and $w \in W$. 

We therefore know $c_i w_i \in W$ for each $i$. Now, we will show by induction on $n$ that 
$$
    c_1 w_1 + c_2 w_2 + \cdots + c_n w_n \in W.
$$
The base case is $n = 1$ which already know. Assume that any length $n$ linear combination 
of vectors in $W$ remains in $W$. Then, we write 
$$
    c_1 w_1 + c_2 w_2 + \cdots + c_{n+1} w_{n+1} = (c_1 w_1 + \cdots + c_n w_n) + c_{n+1} w_{n+1}
$$
with $c_1 w_1 + \cdots + c_n w_n \in W$ by the induction hypothesis and $c_{n+1} w_{n+1} \in W$ 
from before. Thus, 
$$
    c_1 w_1 + c_2 w_2 + \cdots + c_{n+1} w_{n+1} \in W
$$
and we know that $W$ is closed under linear combinations. 

Next let's show that 2) $\Rightarrow$ 3). Assume that $W$ is closed under linear combinations 
of any number of vectors. Then, it is, of course, closed under linear combinations involving 
two vectors. 

Finally, let's show that 3) $\Rightarrow$ 1). Assume that $W$ is closed under linear combinations 
of two vectors. To show that $c \cdot w \in W$, we can take $c_1 = c$, $w_1 = w_2 = w$ and $c_2 = 0$ 
and we know that 
$$
    c_1 w_1 + c_2 w_2 = 1 \cdot w + 0 \cdot w = w \in W
$$
Finally, to show that $w_1 + w_2 \in W$, we just take $c_1 = c_2 = 1$. 
<span style="float:right;"> &#9632; </span>

</details>

Let's look at more examples. 

### Examples

- As a reminder, we already [saw]({% link notes/vector_spaces/def_egs.md%}#examples) that 
the null space $\mathcal Z(A)$ is a subspace of $k^n$ for a $m \times n$ matrix. 

- Let's give a direct proof that the range $\mathcal R(A)$ is a subspace of $k^{m}$ for an 
$m \times n$ matrix $A$. 

    We will check that $\mathcal R(A)$ is closed under linear combinations of two vectors. Take 
    $\mathbf{b}_1, \mathbf{b}_2 \in \mathcal R(A)$ and $c_1,c_2 \in k$. From the definition 
    of $\mathcal R(A)$, we know that there are $\mathbf{x}_1,\mathbf{x}_2 \in k^n$ with 
    $$
        A\mathbf{x}_1 = \mathbf{b}_1, \ A \mathbf{x}_2 = \mathbf{b}_2
    $$
    Using the properties of matrix and scalar multiplication, we have 
    $$
        A \left( c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2 \right) = c_1 A\mathbf{x}_1 + c_2 A\mathbf{x}_2. 
    $$
    This says $c_1 A\mathbf{x}_1 + c_2 A\mathbf{x}_2$ lies in the range of $A$ because we get it 
    from applying $A$ to $c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2$. 

- Consider the space of functions $\operatorname{Func}(\mathbb{R},\mathbb{R})$. Remember that a 
polynomial in one variable is function of the form 
$$
    p(x) = a_n x^n + a_{n-1} x^{n-1} + \cdots a_1 x + a_0. 
$$
for scalars $a_i \in \mathbb{R}$. The _degree_ of $p(x)$ is the largest $a_i$ that is 
nonzero. 

    Let $\operatorname{Poly}_d(\mathbb{R})$ be \
    the subset of polynomial functions in $\operatorname{Func}(\mathbb{R},\mathbb{R})$ of 
    degree $\leq d$. 

    Let's check that $\operatorname{Poly}_d(\mathbb{R})$ is a subspace. Given 
    $$
        \begin{aligned}
            p(x) & = a_d x^d + a_{d-1} x^{d-1} + \cdots a_1 x + a_0 \\
            q(x) & = b_d x^d + b_{d-1} x^{d-1} + \cdots b_1 x + b_0
        \end{aligned}
    $$ 
    then 
    $$
        c_1p(x) + c_2 q(x) = (c_1a_d+c_2b_d) x^d + (c_1a_{d-1} + c_2b_{d-1}) x^{d-1} + \cdots + (c_1a_0 + c_2b_0)
    $$
    is also a polynomial of degree at most $d$ whose coefficients are the linear combination of the coefficients of 
    each. 

    More generally, if we let $\operatorname{Poly}(\mathbb{R})$ be the set of all 
    polynomial functions, it is also a subspace via the exact same argument. 

- A square matrix $A$ is _anti-symmetric_ if $A^T = -A$. So for example, 
$$
    A = 
    \begin{pmatrix}
        0 & 1 & 2 \\
        -1 & 0 & 1 \\
        -2 & -1 & 0 
    \end{pmatrix}
$$
is an anti-symmetric matrix. 

    The set of anti-symmetric matrices is a subspace of $\operatorname{Mat}_{n,n}(k)$. If $A^T = -A$ and 
    $B^T = -B$, then 
    $$
        (c_1 A + c_2 B)^T = c_1 A^T + c_2 B^T = - (c_1 A + c_2 B). 
    $$

- Consider the subset of functions $f : \mathbb{R} \to \mathbb{R}$ given by 
$$
    \left \lbrace f : \mathbb{R} \to \mathbb{R} \mid \frac{d^2f}{dx^2} = f \right\rbrace
$$

    This is a subspace of $\operatorname{Func}(\mathbb{R},\mathbb{R})$. Indeed, we remember that 
    $d/dx$ satisfies 
    $$
        \frac{d}{dx}(f+g) = \frac{df}{dx} + \frac{dg}{dx} \\
        \frac{d}{dx}(cf) = c \frac{df}{dx}. 
    $$

    Thus, 
    $$
        \begin{aligned}
            \frac{d^2}{dx^2}(c_1 f + c_2 g) & = \frac{d}{dx}(c_1 \frac{df}{dx} + c_2 \frac{dg}{dx}) \\
            & = c_1 \frac{d^2f}{dx^2} + c_2 \frac{d^2g}{dx^2}
        \end{aligned}
    $$
    So if $d^2f/dx^2 = f$ and $d^2g/dx^2 = g$, we know that 
    $$
        \frac{d^2}{dx^2}(c_1 f + c_2 g) = c_1 f + c_2 g.
    $$

Many of these examples betray a commonality. If our subset of $W \subseteq V$ is cut out by a function 
$F: V \to V^\prime$, meaning $F^{-1}(0) = W$, then for $W$ to be a subspace we want $F$ to be _linear_ itself:
$$
    F(c_1 v_1 + c_2 v_2) = c_1F(v_1) + c_2 F(v_2)
$$
for any $c_1,c_2 \in k$ and $v_1, v_2 \in V$. 

In the examples,
- $\mathbf{x} \mapsto A \mathbf{x}$ 
- $f \mapsto f^{\prime \prime} - f$ 
are both linear functions. 

Such functions $F: V \to V^\prime$ between vector spaces are called _linear transformations_ and we will return 
to study them shortly. 