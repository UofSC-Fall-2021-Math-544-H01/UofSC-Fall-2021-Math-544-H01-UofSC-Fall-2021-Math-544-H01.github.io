---
layout: page
title: Bases and dimension
nav_order: 6
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Bases

In the our [discussion]({% link notes/vector_spaces/linear_independence.md %}) 
of linear independence, we said the phrase "linearly independent spanning set" 
often. 

Given the importance, we name it.

**Definition**. A _basis_ for a vector space $V$ is a linearly independent spanning 
set for $V$. 

**Example**. For the vector space $k^n$, the _standard basis_ is the set of 
$$
    \mathbf{e}_i := \begin{pmatrix} 0 \\ \vdots \\ 0 \\ 1 \\ 0 \\ \vdots 
    \\ 0 \end{pmatrix} \leftarrow i^{th},   \text{ for } 1 \leq i \leq n 
$$
We have seen this spans $k^n$. It is also linearly independent as the matrix whose 
columns are these vectors is the identity matrix. 

Bases can compress the information of a vector space (often into a finite amount). 

**Lemma**. If $v_i$ for $i \in S$ is a basis for a vector space $V$, then any 
vector $v \in V$ can be written as unique linear combination of the elements of $S$.

{% include beginproof.html %}
Since we know that the $v_i$'s span, we know by definition that any vector can be 
written as a linear combination of them.

Assume that we can write $v$ in two ways 
$$
    \sum_{i \in S} a_i v_i = v = \sum_{i \in S} c_i v_i
$$
Then, taking the difference we have a linear relation
$$
    \sum_{i \in S} (a_i-c_i) v_i = 0
$$
Thus, $a_i - c_i = 0$ for all $i$. 
{% include endproof.html %}

The converse of this statement is also true.

**Lemma**. Assume that any vector in $V$ can be uniquely written as a linear combination 
of the vectors $v_i$ for $i \in S$. Then, the $v_i$ are a basis. 

{% include beginproof.html %}
If we can write any vector as a linear combination, then by definition we span. 

A relation 
$$
    \sum_{i \in S} c_i v_i = 0
$$
is a way to write the zero vector as a linear combination. But, we already have one way: 
take all the coefficients to be $0$. Since we can only write $0$ one way, $c_i = 0$ for 
all $i$ and $S$ is linearly independent. 
{% include endproof.html %}

Assume we have a vector space $V$ and a finite basis set $v_1,\ldots,v_n$ for $V$. 
Then for any $v \in V$ there are unique scalars $c_1,\ldots,c_n$ such that 
$$
    v = c_1v_1 + \cdots + c_nv_n
$$
We call the vector (in $k^n$)
$$
    \begin{pmatrix} 
        c_1 \\ c_2 \\ \vdots \\ c_n
    \end{pmatrix}
$$
the _representation_ of $v$ in the basis $v_1,\ldots,v_n$. 

Notice that different bases can yield different representations of the same vector. 

**Example**. Both 
$$
    \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}, \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix}, 
    \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}
$$
and 
$$
    \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}, 
    \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}
$$
are bases for $\mathbb{R}^3$. 

Take the vector 
$$
    v = \begin{pmatrix} 1 \\ 2 \\ 3 \end{pmatrix}
$$

Then the representation of $v$ in the first basis (the standard basis) is just 
$$
    \begin{pmatrix} 1 \\ 2 \\ 3 \end{pmatrix}
$$

But the representation of $v$ in the second basis is 
$$
    \begin{pmatrix} -1 \\ -1 \\ 3 \end{pmatrix}
$$

Given a basis $v_1,\ldots,v_n$ and a set of vectors $w_1,\ldots,w_m$ in $V$ we get an 
$m \times n$ matrix $A$ given by using the coefficients in the representations 
$$
    w_j = A_{1j}v_1 + A_{2j} v_2 +\cdots + A_{nj} v_n  
$$
for each $1 \leq j \leq m$. 

Assume now that $v_1,\ldots,v_n$ and $w_1,\ldots,w_m$ are 
both bases for $V$. Then we get an $m \times n$ matrix $A$ expressing the $w_j$ as 
linear combinations of the $v_i$ and a $n \times m$ matrix $B$ expressing the 
$v_i$ as linear combinations of $w_j$.

In this case, we call $A$ and $B$ _change of basis_ matrices. 

**Example**. Coming back to our example of two bases:
$$
    \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}, \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix}, 
    \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}
$$
and 
$$
    \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}, 
    \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}
$$
The change of basis from the standard basis to the other one is 
$$
    A = \begin{pmatrix}
        1 & 1 & 1 \\
        0 & 1 & 1 \\
        0 & 0 & 1
    \end{pmatrix}
$$
while the change of basis matrix in the other direction is 
$$
    B = \begin{pmatrix}
        1 & -1 & 0 \\
        0 & 1 & -1 \\
        0 & 0 & 1 \\
    \end{pmatrix}
$$
Notice that $AB = BA = I$. 

**Lemma**. Assume now that $v_1,\ldots,v_n$ and $w_1,\ldots,w_m$ are 
both bases for $V$ and let $A$ and $B$ be the two change of bases 
matrices. Then 
$$
    AB = I_m \\
    BA = I_n
$$

{% include beginproof.html %}
Notice that 
$$
    v_i = (BA)_{1i}v_1 + \cdots + (BA)_{ni}v_n
$$
As $v_1,\ldots,v_n$ are linearly independent, we must have 
$$
    (BA)_{ij} = \begin{cases} 1 & i=j \\ 0 & i \neq j \end{cases}
$$

Reversing the roles of $v_i$ and $w_j$, we have $AB = I_m$.
{% include endproof.html %}

**Theorem**. If $v_1,\ldots,v_n$ and $w_1,\ldots,w_m$ are 
both bases for $V$, then $n = m$. In other words, the length of 
a basis for $V$ is independent of the choice of basis. 

{% include beginproof.html %}
Assume for that $m > n$. Then, we know that the reduced row echelon 
form of $A$ must have free variables. Thus,
$$
    \mathcal Z(A) \neq \lbrace 0 \rbrace
$$
But if $Ax = 0$ then 
$$
    0 = B0 = BAx = Ix = x
$$
which is a contradiction. Thus, $m \leq n$. Similarly, we must have 
$n \leq m$, giving
$$
    n = m. 
$$
{% include endproof.html %}

## Dimension

It turns out that the following number captures everything about 
vector spaces spanned by a finite number of vectors. 

**Definition**. Let $V$ be a vector space. If $v_1,\ldots,v_d$ is 
a basis for $V$, we say the _dimension_ of $V$ is $d$. We write 
$$
    \dim V = d. 
$$
We will sometimes say that $V$ is _finite-dimensional_. 

If $V$ is not finite-dimensional, we will write $\dim V = \infty$. 

Note that the dimension of the zero vector space is $0$. 

### Consequences

**Lemma**. Assume that $\operatorname{Span}(S)$ contains a basis 
for a vector space $V$. Then 
$$
    \operatorname{Span}(S) = V
$$

{% include beginproof.html %}
Since we can write any element $v \in V$ as 
$$
    v = \sum_{b \in B} c_bv_b
$$
for the basis $B$ and we can write 
$$
    v_b = \sum_{i \in S} a_{ib} v_i 
$$
we have 
$$
    v = \sum_{b \in B} c_b \left( \sum_{i \in S} a_{ib} v_i \right) = \sum_{i \in S} \left(\sum_{b \in B} c_ba_{ib} \right) v_i
$$
we see that $v \in \operatorname{Span}(S)$. 
{% include endproof.html %}

**Lemma**. Let $\dim V = d$. Then any collection of $\geq d+1$ vectors 
is linearly dependent. 

{% include beginproof.html %}
Let $v_1,\ldots,v_d$ be a basis for $V$ and $w_j$ for $j \in S$ be linearly 
independent and $|S| > d$. If $|S| = \infty$, we replace $S$ by a finite subset of 
$> d$ elements. Demonstrating a relation between the subset will prove that 
$S$ is linearly dependent. 

If $v_1 \not \in \operatorname{Span}(S)$, we replace $S$ with 
$S \cup \lbrace v_1 \rbrace$ (but we still call it $S$). We continue 
inductively: if $v_i \not \in \operatorname{Span}(S)$, we replace 
$S$ with $S \cup \lbrace v_i \rbrace$. 

Finishing, we can assume that $S$ 
remains linearly independent and $v_i \in \operatorname{Span}(S)$ for each 
$i$. Thus, from the previous lemma, we know that $S$ also spans $V$. Moreover, 
$S$ only got bigger so $|S| > d$ remains true.  

Now we can apply the Theorem to conclude $|S| = d$ and we have a contradiction. 
{% include endproof.html %}

**Lemma**. Let $\dim V = d$. Any collection $d$ linearly independent vectors is a
basis. Any collection $d$ spanning vectors is a basis. 

{% include beginproof.html %}
If $v_1,\ldots,v_d$ is linearly independent, then we can add in vectors to the set 
to complete it to a basis. But then $\dim V > d$ which is a contradiction.

Similarly, if $v_1, \ldots, v_d$ spans $V$, we can throw out vectors from the set 
to get a basis. But then $\dim V < d$ which is also a contradiction. 
{% include endproof.html %}

**Proposition**. Let $U \subseteq V$ be a subspace of a vector space. 
Then, 
$$
    \dim U \leq \dim V
$$
In particular, any subspace of a finite-dimensional vector space is 
also finite-dimensional.

{% include beginproof.html %}
The convention here is that if $\dim V = \infty$, anything is less than 
$\infty$. So we only need to handle case $V$ is finite-dimensional.

If $U = 0$, then we are done. Pick some nonzero vector $u_1 \in U$. Now if 
$$
    \operatorname{Span}(u_1,\ldots,u_i) \neq U
$$
we pick $u_{i+1} \not \in \operatorname{Span}(u_1,\ldots,u_i)$ to get 
a linearly independent set $u_1,\ldots,u_{i+1}$. 

From the previous lemma we cannot pick $u_{d+1}$. Thus, there is some $e \leq d$ 
with 
$$
    \operatorname{Span}(u_1,\ldots,u_e) = U
$$
and the dimension of $U$ is $e$.
{% include endproof.html %}

### Examples
- The dimension of $k^n$ is $n$. We have already seen the standard 
basis, which has length $n$.

- The dimension of $\mathcal Z(A)$ is number of free variables in 
row echelon form. 

    Indeed, we have 
    [seen]({% link notes/vector_spaces/spans.md %}#spanning-sets-for-null-spaces)
    how to construct a spanning set $v_i$ for $\mathcal Z(A)$ indexed by the 
    free variables $x_i$. 

    Let us denote the number of free variables by $r$.

    We take the general parameterized solution and, for each free variable $x_i$, 
    we set that variable to $1$ and the others to $0$ to get $v_i$. 

    Let $B$ be the matrix whose columns are the $v_i$. Notice that up to permuting the 
    rows of $B$ we can write $B$ as 
    $$
        \begin{pmatrix} B^\prime \\ I \end{pmatrix}
    $$

    Assume we had a relation 
    $$
        \sum c_i v_i = 0.
    $$
    Then for  
    $$
        x = \begin{pmatrix} c_1 \\ \vdots \\ c_r \end{pmatrix}
    $$
    we have a solution of $Bx = 0$. But then we need 
    $$
        Ix = 0 
    $$
    which immediately gives $x = 0$. 

    For a particular example, take 
    $$
        A = 
        \begin{pmatrix}
            1 & 2 & 2 & 3\\
            3 & 6 & 7 & 8
        \end{pmatrix}
    $$
    which in row echelon form is 
    $$
        \begin{pmatrix} 
            1 & 2 & 0 & 5 \\
            0 & 0 & 1 & -1 
        \end{pmatrix}
    $$
    Thus the general parametrized solution to $Ax = 0$ is 
    $$
        \begin{pmatrix} -2x_2 - 5x_4 \\ x_2 \\ x_4 \\ x_4 \end{pmatrix}
    $$
    We have the basis 
    $$
        \begin{pmatrix} -2  \\ 1 \\ 0 \\ 0 \end{pmatrix}, \ \begin{pmatrix} -5 \\ 0 \\ 1 \\ 1 \end{pmatrix}
    $$
    Note that $2 \times 2$ block given by the second and fourth row is just $I_2$.

- The dimension of $\mathcal R(A)$ is the number of pivots in the row echelon 
form for $A^T$. 

    We [saw]({% link notes/vector_spaces/spans.md%}#linear-dependence-and-matrices) 
    that row span of $A^T$ equals the row span of the row echelon form of $A^T$ and the 
    nonzero rows of a matrix in row echelon form are linear independent. 

    The number of nonzero rows is exactly the number of pivots. 

- In general, a vector space need not be finite dimensional. The space 
$\operatorname{Poly}(\mathbb{R},\mathbb{R})$ is not finite dimensional since there is 
no finite spanning set. 

    But it turns out that any vector space will have a basis. You have use 
    [Zorn's Lemma](http://www.math.lsa.umich.edu/~kesmith/infinite.pdf). 
