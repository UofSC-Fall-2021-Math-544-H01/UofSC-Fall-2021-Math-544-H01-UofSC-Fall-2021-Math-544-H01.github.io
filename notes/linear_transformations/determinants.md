---
layout: page
title: Determinants
nav_order: 7
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Specifications for determinants 

Rather surprisingly, it turns out there is a single number built from 
a square matrix $A$ which can tell you whether or not $A$ is invertible. 

For small size matrices, we can given explicit formulae for this 
number. 

The simplest case is $1 \times 1$ matrix $(a)$. It is invertible if and 
if only if $a \neq 0$. 

A $2 \times 2$ matrix 
$$
    \begin{pmatrix} 
        a & b \\
        c & d 
    \end{pmatrix}
$$
is invertible if and only if 
$$
    ad-bc \neq 0.
$$ 

A $3 \times 3$ matrix
$$
    \begin{pmatrix} 
        a & b & c \\
        d & e & f \\
        g & h & i  
    \end{pmatrix}
$$
is invertible if and only if 
$$
    aei-afh-bdi+bfg+cdh-ceg \neq 0 
$$

This pattern generalizes to any $n \times n$ matrix. Instead of giving a 
formula for this number, we give a list of properties that completely 
capture the number and then show how to meet that specification with 
a formula. 

**Definition**. A _determinant_ is a function 
$$
    \det : \operatorname{Mat}_{n \times n}(k) \to k 
$$
which satisfies the following conditions:
- $\det$ is multiplicative: 
$$
    \det(AB) = \det(A) \det(B) 
$$
- recall $P(i,j)$ is the row exchange $i \leftrightarrow j$ 
matrix. The determinant of row exchange matrices is $-1$: 
$$
    \det(P(i,j)) = -1
$$
- if $U$ is upper triangular, then $\det(U)$ is 
the product of the diagonal entries  
$$
    \det(U) = \prod_{i=1}^n U_{ii}
$$
- if $L$ is a lower triangular matrix, then $\det(U)$ is 
the product of the diagonal entries 
$$
    \det(L) = \prod_{i=1}^n L_{ii}
$$

### Facts about determinants

The previous definition is definitely not constructive. It 
is prescriptive. It lists a collection of properties that 
a determinant must satisfy. Without any thought, it is not 
clear that 
- any determinant actually exists nor 
- we can't have more than one determinant. 

Below we work out some quick conclusions from the definition. 
Ultimately, we build up to showing the uniqueness of the 
determinant: there can be only one (like the Highlander). We 
will defer showing is at least one for the moment. 

**Lemma**. Assume $\det$ is a determinant. 
If $A$ is invertible, we have 
$$
    \det(A^{-1}) = \frac{1}{\det A}
$$
In particular, $\det A \neq 0$. 

{% include beginproof.html %}
Since $A$ is invertible, there is an $A^{-1}$ with 
$AA^{-1} = I_n$. Thus, we have 
$$
    1 = \det I_n = \det(A A^{-1}) = \det(A) \det(A^{-1})
$$  
So $\det(A) \neq 0$ and 
$$
    \det(A^{-1}) = \frac{1}{\det A}
$$
{% include endproof.html %}

**Lemma**. Assume $\det$ is a determinant. 
For the row scaling matrix, we have 
$$
    \det S(i,c) = c
$$

{% include beginproof.html %}
Recall that
$$
    \det S(i,c)_{lj} = 
    \begin{cases} 
        1 & l = j \neq i \\
        c & l = j = i \\
        0 & l \neq j 
    \end{cases}
$$
so $S(i,c)$ is both upper and lower triangular. Thus,
$$
    \det S(i,c) = \prod_{j=1}^n S(i,c)_jj = c. 
$$
{% include endproof.html %}

**Lemma**. Assume $\det$ is a determinant. 
For the row elimination matrix, we have 
$$
    \det L(i,j,c) = 1
$$

{% include beginproof.html %}
Recall that $L(i,j,c)$ is lower triangular with all $1$'s along 
the diagonal. Thus, 
$$
    \det L(i,j,c) = 1. 
$$
{% include endproof.html %}

**Proposition**. Assume that $A$ and $B$ are related 
via a sequence of elementary row operations. If $\det$ and 
$\det^\prime$ are both determinants and $\det A = 
\det^\prime A$, then 
$$
    \det B = \operatorname{det}^\prime B.
$$

{% include beginproof.html %}
For $A$ and $B$ to be related by elementary row operations, 
we have a sequence of matrices $A_i$ with 
$$
    A_{i+1} = C_i A_i
$$
where $A_0 = A$, $A_N = B$, and each $C_i$ is one of 
$P(i,j), L(i,j,c),$ or $S(i,c)$ or their inverse. 

We show that $\det(A_i) = \det^\prime(A_i)$ using induction. 

The base case is $A_0 = A$ is contained as assumption in the 
statement. 

Assume that $\det(A_i) = \det^\prime(A_i)$. We wish to 
show that $\det(A_{i+}) = \det^\prime(A_{i+1})$. We know 
that $A_i = C_i A_{i+1}$. Since both are determinants, we have 
$$
    \det(A_{i+1}) = \det(C_i) \det(A_i) \\
    \operatorname{det}^\prime(A_{i+1}) = 
    \operatorname{det}^\prime(C_i) \operatorname{det}^\prime(A_i)
$$
The previous lemmas allow us to conclude that 
$$
    \det(C_i) = \operatorname{det}^\prime(C_i)
$$
and we have assumed that $\det A_i = \operatorname{det}^\prime A_i$. 
Thus, 
$$
    \det A_{i+1} = \operatorname{det}^\prime A_{i+1}
$$

By induction, we have $\det A_i = \operatorname{det}^\prime A_i$ for 
all $i$. Hence 
$$
    \det B = \operatorname{det}^\prime B
$$
since $B = A_N$. 
{% include endproof.html %}

With these results in hand, we can check that there is at most 
one determinant. 

**Theorem**. There can be only one possible determinant. 
More precisely, if $\det$ and $\det^\prime$ are both determinants, 
then 
$$
    \det(A) = \operatorname{det}^\prime(A)
$$
for all $A \in \operatorname{Mat}_{n \times n}(k)$. 

{% include beginproof.html %}
Thanks to Gaussian Elimination, we know that any matrix $A$ 
is related via elementary row operations to a upper triangular 
matrix $U$ - one in row echelon form. Since 
$\det U = \det^\prime U$ we can use the previous Proposition to conclude 
that $\det A = \det^\prime A$. 
{% include endproof.html %}

We can also establish that any determinant completely captures 
invertibility of a matrix. 

**Theorem**. Assume $\det$ is a determinant. A square matrix $A$ is 
invertible (nonsingular) if and only if $\det A \neq 0$. 

{% include beginproof.html %}
We saw above that if $A$ is invertible then $\det A \neq 0$. 

Let's show that if $A$ is not invertible, then $\det A = 0$. Thanks to 
Gaussian Elimination we know that $A$ is related to an upper triangular 
matrix $U$ via elementary row operations so $A = C U$ where 
$C$ is a product of inverses to elementary row operation matrices. We 
can take $U$ to be the reduced row echelon form of $A$. 

We 
[have seen]({% link notes/solving_linear_systems/invertibility.md %}
#gaussian-elimination-can-produce-an-inverse) 
that $A$ is invertible if and only if $U = I_n$. If $U \neq I_n$, 
then it must have at least one $0$ along the diagonal. Thus, 
$\det U = 0$ and $\det A = 0$ too. 
{% include endproof.html %}

### A view to computation 

Our arguments also give us a means to compute a determinant. For 
each of our elementary row operation matrices $S(i,c), P(i,j),$ 
and $L(i,j,c)$ and for their inverses, we know its determinant. 

Thus, we can compute $\det A$ as a byproduct of the process of 
Gaussian Elimination. Let's step through an example. 

Take 
$$
    A = 
    \begin{pmatrix} 
        1 & 2 & -1 \\
        -1 & -1 & 3 \\
        1 & -2 & 0 
    \end{pmatrix}
$$

Then, we have 
$$
    L(1,3,-1)L(1,2,1)A = 
    \begin{pmatrix}
        1 & 2 & -1 \\
        0 & 1 & 2 \\
        0 & -4 & 2
    \end{pmatrix}
$$

Next we have 
$$
    L(2,3,4)L(1,3,-1)L(1,2,1)A = 
    \begin{pmatrix} 
        1 & 2 & -1 \\
        0 & 1 & 2 \\
        0 & 0 & 10 
    \end{pmatrix}
$$

Therefore, 
$$
    \begin{aligned}
        10 & = \det \begin{pmatrix} 
            1 & 2 & -1 \\
            0 & 1 & 2 \\
            0 & 0 & 10 
        \end{pmatrix} \\ 
        & = (\det L(2,3,4)) (\det L(1,3,-1)) (\det L(1,2,1)) (\det A) \\
        & = \det A
    \end{aligned}
$$

In general, given an LU factorization with partial pivoting 
$$
    P A = LU 
$$
then 
$$
    \det(P) \det(A) = \det(L) \det(U) = \left(\prod_{i=1}^n L_{ii} \right)
    \left(\prod_{i=1}^n U_{ii} \right)
$$
so 
$$
    \det(A) = \left( \det P\right)^{-1} \left(\prod_{i=1}^n L_{ii} \right)
    \left(\prod_{i=1}^n U_{ii} \right)
$$
is a very quick way to compute $\det A$. 

### Minimal specifications 

It turns out the following is sufficient to completely specify determinants. 

**Theorem**. Assume 
$$
    \det : \operatorname{Mat}_{n \times n}(k) \to k 
$$
satisfies 
- 
$$
    \det(AB) = \det(A) \det(B) 
$$
and 
- 
$$
    \det(cI) = c^n 
$$
for any scalar $c$. 

Then, $\det$ is a determinant. 

Note that any determinant must satisfy these conditions. 

We won't give a proof of this fact. If you are interested, 
[ask me](https://media.giphy.com/media/PHjiEBYrNPK6Y/giphy.gif). 