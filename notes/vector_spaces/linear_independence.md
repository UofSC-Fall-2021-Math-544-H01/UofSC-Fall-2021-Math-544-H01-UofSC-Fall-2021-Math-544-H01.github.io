---
layout: page
title: Linear independence
nav_order: 5
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Linear independence

Hiding behind all of [Gaussian Elimination]({% link notes/solving_linear_systems/gaussian_elimination.md %}) 
is the central fact that: 
<center> For a matrix $A$, quite often some of its rows can be redundant. </center>
Gaussian Elimination can be viewed as a means to eliminate that redundancy. 

For example, if we take 
$$
    A = 
    \begin{pmatrix}
        1 & 2 \\
        1 & 2 \\
    \end{pmatrix}
$$
then its reduced row echelon form is 
$$
    A = 
    \begin{pmatrix}
        1 & 2 \\
        0 & 0 \\
    \end{pmatrix}
$$
The last row is obviously redundant and can, therefore, be eliminated by subtracting off the first 
row. 

Of course, not all redundancy will be this simple. If the reduced row echelon form of $A$ has some 
zero rows, then there is no guarantee that some of the rows were _equal_ to start with. 

But they are still redundant in a more general way. 

**Definition**. A list $S$ of vectors in a vector space $V$ is called 
_linearly dependent_ if there exists scalars $c_1,\ldots,c_s$ with at least one 
$c_i \neq 0$ such that 
$$
    c_1 v_1 + c_2 v_2 + \cdots + c_s v_s = 0
$$
and each $v_i \in S$. 

In other words, there needs to be a _nontrivial_ linear combination of the $v_i$ 
that yields the zero vector. This nontrivial linear combination we call a _linear relation_ 
between the $v_i$. 

If $S$ is not linearly dependent, we call the it _linearly independent_. 

In our simple from above, the two vectors 
$$
    \left\lbrace \begin{pmatrix} 1 \\ 2 \end{pmatrix}, \ \begin{pmatrix} 1 \\ 2 \end{pmatrix}\right\rbrace
$$
are linearly dependent since 
$$
    \begin{pmatrix} 1 \\ 2 \end{pmatrix} + (-1) \ \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}
$$

However, after row reduction, the set of nonzero row vectors 
$$
    \left\lbrace \begin{pmatrix} 1 \\ 2 \end{pmatrix} \right\rbrace
$$
is linearly independent. The only way to solve 
$$
    \begin{aligned}
        c \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix} 
    \end{aligned}
$$
is to set $c = 0$. 

### Consequences 

**Lemma**. If $S$ is a list of vectors and $0 \in S$, then $S$ is linearly dependent. 

{% include beginproof.html %}
For the zero vector, we know that 
$$
    1 \cdot 0 = 0
$$
which gives a relation. 
{% include endproof.html %}

Spans and linear (in)dependence are closely tied together. 

**Lemma**. Let $S$ be a collection of vectors in a vector space $V$. 
$S$ is linearly dependent if and only if there is some $v \in S$ such that 
$$
    \operatorname{Span}(S) = \operatorname{Span}(S \setminus \lbrace v \rbrace).
$$
In other words, the set $S$ is linearly dependent if and only if a proper subset of 
$S$ (meaning we have removed some vectors from $S$) also spans $\operatorname{Span}(S)$. 

{% include beginproof.html %}
Assume that $S$ is linearly dependent. Then we have a linear relation 
$$
    c_1 v_1 + \cdots + c_s v_s = 0
$$
We know that, for some $1 \leq j \leq s$, $c_j \neq 0$. We can rewrite the relation as 
$$
    v_j = -\sum_{i \neq j} \frac{c_i}{c_j} v_i \tag{*}
$$

Now take any (finite) linear combination 
$$
    \sum_{w \in S} a_w w  
$$
from $\operatorname{Span}(S)$ and we can eliminate $v_j$ by substituting in (*). We get 
$$
    \sum_{w \in S} a_w w = \sum_{w \neq v_i} a_w w + \sum_{i \neq j} \left( a_i - a_j \frac{c_i}{c_j} \right)v_i
$$
The right hand side is a linear combination of vectors from $S\setminus \lbrace v_j \rbrace$. Thus, 
$$
    \sum_{w \in S} a_w w  \in \operatorname{Span}(S \setminus \lbrace v_j \rbrace)
$$
And we have the containment of sets 
$$
    \operatorname{Span}(S) \subseteq \operatorname{Span}(S \setminus \lbrace v_j \rbrace).
$$

Since any linear combination of the vectors from $S\setminus \lbrace v_j \rbrace$ is immediately a 
linear combination of those from $S$ by settings $a_j = 0$, we always have 
$$
    \operatorname{Span}(S \setminus \lbrace v_j \rbrace) \subseteq \operatorname{Span}(S)
$$
Consequently, we have 
$$
    \operatorname{Span}(S) = \operatorname{Span}(S \setminus \lbrace v_j \rbrace).
$$

Now assume that 
$$
    \operatorname{Span}(S) = \operatorname{Span}(S \setminus \lbrace v_j \rbrace).
$$
In particular, $v_j \in \operatorname{Span}(S \setminus \lbrace v_j \rbrace)$ so we can write 
$$
    v_j = \sum_{i \neq j} a_i v_i
$$
which gives the relation 
$$
    \sum_{i \neq j} a_i v_i - v_j = 0. 
$$
{% include endproof.html %}

Through our arguments, we also have established the following useful statement. 

**Corollary**. A set of vectors $v_1, \ldots, v_s$ is linearly independent if and only if we have an (strictly)
increasing chain of subspaces 
$$
    0 \subsetneq \operatorname{Span}(v_1) \subsetneq \operatorname{Span}(v_1,v_2) \subsetneq 
    \cdots \subsetneq \operatorname{Span}(v_1,\ldots,v_s) 
$$  

A particularly important consequence of this line of reasoning is the following fact. 

**Proposition**. Take a finite list of vectors $v_1, \ldots, v_s$ in a vector space $V$. 
Assume that their span is not $\lbrace 0 \rbrace$. There is a subset of the $v_i$ which is both 
- linearly independent and
- and a spanning set for the span of $v_1,\ldots,v_s$. 

{% include beginproof.html %}
We proceed by induction on $s$. For the case of $s=1$, either $v_1 = 0$ or not. If $v_1 = 0$, 
then $\operatorname{Span}(v_1) = \lbrace 0 \rbrace$ which contradicts the assumption. So 
$v_1 \neq 0$ and therefor there is no nonzero $c$ with $cv_1 = 0$. Thus, $v_1$ spans and 
is linearly independent. 

Assume we know the result is true for $s-1$ vectors. For $s$ vectors $v_1, \ldots, v_s$, 
we first apply the induction hypothesis $v_1, \ldots, v_{s-1}$. To do so, we need to know that 
$\operatorname{Span}(v_1,\ldots,v_{s-1}) \neq \lbrace 0 \rbrace$ or give a separate proof in 
that case. 

Assume that $\operatorname{Span}(v_1,\ldots,v_{s-1}) = \lbrace 0 \rbrace$. Then $v_i = 0$ for 
each $1 \leq i \leq s-1$. Otherwise, $v_i \in \operatorname{Span}(v_1,\ldots,v_{s-1})$ would be a 
nonzero vector. 

The span does not change if we throw in any number of zero vectors to the spanning set. Thus, 
$$
    \operatorname{Span}(v_1,\ldots,v_{s-1},v_s) = \operatorname{Span}(v_s)
$$
and we can appeal to the case of $s=1$. 

Now assume that $\operatorname{Span}(v_1,\ldots,v_{s-1}) \neq \lbrace 0 \rbrace$. We can use 
the induction hypothesis to select a subset $S$ of the $v_1, \ldots, v_{s-1}$ that spans 
$\operatorname{Span}(v_1,\ldots,v_{s-1})$ and is linearly independent. 

We have two possibilities: 
1. $$\operatorname{Span}(S) = \operatorname{Span}(v_1,\ldots,v_{s-1}) = \operatorname{Span}(v_1,\ldots,v_{s-1},v_s)$$
2. $$\operatorname{Span}(S) = \operatorname{Span}(v_1,\ldots,v_{s-1}) \neq \operatorname{Span}(v_1,\ldots,v_{s-1},v_s)$$

In the case of 1, we are done already. $S$ is our desired linearly independent spanning set. 

In the case of 2, we know that there cannot be a linear relation amongst the $S \cup \lbrace v_s \rbrace$ since the 
span increased in size when adding $v_s$. Thus $S \cup \lbrace v_s \rbrace$ is our 
desired linearly independent spanning set. 
{% include endproof.html %}

## Linear dependence and matrices

Suppose we have a list of vectors from $k^m$. How do we figure out if they are linearly dependent? 

The answer (as is often the case) is Gaussian Elimination. Let $v_1,\ldots,v_n$ be the vectors. 
Let's form the $m \times n$ matrix 
$$
    A_{ij} := (v_j)_i
$$
In other words, $A$ is the matrix whose columns are the vectors $v_1, \ldots, v_n$. 

We have the equality 
$$
    Ax = c_1 v_1 + \cdots + c_n v_n
$$
where 
$$
    x = 
    \begin{pmatrix}
        c_1 \\
        \vdots \\
        c_n
    \end{pmatrix}
$$

Thus, finding a relation 
$$
    c_1 v_1 + \cdots + c_n v_n = 0
$$
is _exactly the same_ as solving the homogeneous system 
$$
    Ax = 0
$$
for some $x \neq 0$. 

We have established the following fact.

**Proposition**. A collection of vectors $v_1,\ldots,v_n$ in $k^m$ is 
linearly independent if and only if the matrix $A$ formed by taking the $v_i$ 
as the column vectors of $A$ has trivial null space, 
ie $\mathcal Z(A)= \lbrace 0 \rbrace$. 

**Corollary**. If $n > m$, then $v_1,\ldots,v_n$ are linearly dependent. 
{% include beginproof.html %}
If we form the matrix $A$ whose columns are the $v_i$ and perform Gaussian 
elimination to convert it to reduced row echelon form, we will always have 
a free variable and thus nonzero zero solutions to $Ax = 0$. 
{% include endproof.html %}

Is there an effective way to find a spanning set for the span of $v_1,\ldots,v_s$ 
in $k^m$? Again, the answer is Gaussian elimination but now 
with a twist (or transpose). 

The span of set of vectors remains unchanged under the three classes of row operations. 

**Proposition**. Let $S = \lbrace v_1, \ldots, v_s\rbrace$ be vectors in a vector space $V$.
- Let $S^\prime$ be the set resulting from replacing $v_i$ by $cv_i$ for some nonzero $c$. 
Then 
$$
    \operatorname{Span}(S) = \operatorname{Span}(S^\prime).
$$
- Let $S^\prime$ be the set resulting from exchanging $v_i$ and $v_j$. Then 
Then 
$$
    \operatorname{Span}(S) = \operatorname{Span}(S^\prime).
$$
- Let $S^\prime$ be the set resulting from replacing $v_i$ by $v_i - cv_j$ for $i \neq j$. 
Then 
$$
    \operatorname{Span}(S) = \operatorname{Span}(S^\prime).
$$

{% include beginproof.html %}
- Pick a linear combination of the vectors from $S^\prime$. It looks like 
$$
    c_1 v_1 + \cdots + c_i(cv_i) + \cdots + c_sv_s
$$
This is immediately a linear combination of the vectors from $S$: 
$$
    c_1 v_1 + \cdots + (c_ic)v_i + \cdots + c_sv_s \in \operatorname{Span}(S)
$$
Therefore, 
$$
    \operatorname{Span}(S^\prime) \subseteq \operatorname{Span}(S).
$$
We can obtain $S$ from $S^\prime$ by multiplying $cv_i$ by $1/c$. Thus we also 
know that 
$$
    \operatorname{Span}(S) \subseteq \operatorname{Span}(S^\prime)
$$
and hence
$$
    \operatorname{Span}(S) = \operatorname{Span}(S^\prime). 
$$

- Since linear combinations do not depend on the order of the terms in 
the sum, this is clear. 

- Finally, pick a linear combination of the vectors from $S^\prime$. It looks like 
$$
    c_1 v_1 + \cdots + c_i(v_i-cv_j) + \cdots + c_sv_s
$$
which can be rewritten as 
$$
    c_1 v_1 + \cdots + c_iv_i + \cdots + (c_j-c_ic)v_j + \cdots  + \cdots + c_sv_s
$$
Thus, 
$$
    \operatorname{Span}(S^\prime) \subseteq \operatorname{Span}(S).
$$
Since we can obtain $S$ from $S^\prime$ by replacing $v_i - cv_j$ by 
$(v_i - cv_j) + cv_j = v_i$, we have already shown that 
$$
    \operatorname{Span}(S) \subseteq \operatorname{Span}(S^\prime)
$$
and hence
$$
    \operatorname{Span}(S) = \operatorname{Span}(S^\prime). 
$$
{% include endproof.html %}
<br>
To perform Gaussian elimination, we just systematically apply row operations. 

**Corollary**. Given a matrix $A$, the span of the row vectors does not change 
under Gaussian elimination. 

We want to make one more useful observation about Gaussian elimination and 
linear dependence. 

**Proposition**. The nonzero rows of any matrix in row echelon form are 
linearly independent. 

{% include beginproof.html %}
We proceed by induction on the number of rows. For one nonzero, we know a single 
nonzero vector is a linearly independent set. 

Assume now we know it for a matrix with $s-1$ nonzero rows and let $A$ be a 
matrix in row echelon form with $s$ nonzero rows. 

Let $A^\prime$ be the matrix obtained from $A$ by removing the first row. It is 
also in row echelon form. Thus, there are no nonzero linear relations between 
all the rows of $A^\prime$ from the induction hypothesis. 

Assume we have a relation 
$$
    \sum_i c_i \mathbf{R}_A^i = 0 \tag{$\star$}
$$
Let $p$ be the column number of the pivot in row one. Then,
$$
    (\mathbf{R}_A^i)_p = A_{ip} = 0
$$
for $i \neq 1$, by definition of row echelon form. Thus, if we take the $p$-th component of 
($\star$) we are only left with 
$$
    c_1 A_{1p} = 0
$$
As this is the pivot $A_{1p} \neq 0$, so $c_1 = 0$. Thus, ($\star$) is a linear 
relation amongst the other rows. We have already shown this must be the zero. 
{% include endproof.html %}

### Examples

At this point, we have all the tools we need to quickly 
1. determine if a set of vectors in $k^m$ is linearly dependent and 
2. find a finite linearly independent spanning set for the span of a finite 
number of vectors. 

Let's take the vectors 
$$
    \begin{pmatrix} 1 \\ 2 \\ 3 \\ 4 \end{pmatrix}, \
    \begin{pmatrix} 1 \\ 0 \\ 0 \\ -1 \end{pmatrix}, \
    \begin{pmatrix} 0 \\ 1 \\ 1 \\ 0 \end{pmatrix}, \
    \begin{pmatrix} 3 \\ 2 \\ 3 \\ 2 \end{pmatrix}
$$

Are these linearly independent? If we take the matrix 
$$
    \begin{pmatrix}
        1 & 1 & 0 & 3 \\
        2 & 0 & 1 & 2 \\
        3 & 0 & 1 & 3 \\
        4 & -1 & 0 & 2
    \end{pmatrix}
$$
whose columns are these vectors, we just need to reduce it and figure out if it 
has any free variables. 

In reduced row echelon form we have 
$$
    \begin{pmatrix}
        1 & 0 & 0 & 1 \\
        0 & 1 & 0 & 2 \\
        0 & 0 & 1 & 0 \\
        0 & 0 & 0 & 0 \\
    \end{pmatrix}
$$
Since there is a free variable, we know that the original vectors are linearly dependent. 

Can we find a linearly independent spanning set for 
$$
    \operatorname{Span} \left(\begin{pmatrix} 1 \\ 2 \\ 3 \\ 4 \end{pmatrix}, \
    \begin{pmatrix} 1 \\ 0 \\ 0 \\ -1 \end{pmatrix}, \
    \begin{pmatrix} 0 \\ 1 \\ 1 \\ 0 \end{pmatrix}, \
    \begin{pmatrix} 3 \\ 2 \\ 3 \\ 2 \end{pmatrix} \right) \ ?
$$

We take $A^T$ 
$$
    \begin{pmatrix}
        1 & 2 & 3 & 4 \\
        1 & 0 & 0 & -1 \\
        0 & 1 & 1 & 0 \\
        3 & 2 & 3 & 2
    \end{pmatrix}
$$
and reduce it to get 
$$
    \begin{pmatrix}
        1 & 0 & 0 & -1 \\
        0 & 1 & 0 & -5 \\
        0 & 0 & 1 & 5 \\
        0 & 0 & 0 & 0 \\
    \end{pmatrix}
$$
Thus, 
$$
    \begin{pmatrix}
        1 \\ 0 \\ 0 \\ -1 \end{pmatrix}, \ 
        \begin{pmatrix}
        0 \\ 1 \\ 0 \\ -5 \end{pmatrix}, \ 
        \begin{pmatrix}
        0 \\ 0 \\ 1 \\ 5 \end{pmatrix}
$$
is a linearly independent spanning set. 