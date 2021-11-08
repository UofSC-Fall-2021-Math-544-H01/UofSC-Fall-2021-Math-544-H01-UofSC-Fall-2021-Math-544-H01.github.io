---
layout: page
title: Cofactor Formula
nav_order: 8
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Formulae for the determinant

[Previously]({% link notes/linear_transformations/determinants.md %}) 
we gave a specification for how the determinant should behave. We 
use this to deduce some rather impressive features of the 
determinant. Note that we can say _the_ determinant as we 
[know]({% link notes/linear_transformations/determinants.md %}#facts-about-determinants) 
any two determinants are equal. 

Here we turn to giving one determinant and a formula. The 
formula is, perhaps, the most common one. However, computing 
determinants through Gaussian Elimination is generally faster. 
The 
[Bareiss algorithm](https://en.wikipedia.org/wiki/Bareiss_algorithm) 
is the most common one used. 

We need some notation to concisely state the formula here. For a 
$m \times n$ matrix $A$, the $(i,j)$ minor of $A$ is the $(m-1) \times 
(n-1)$ matrix obtained by deleting the i-th row and j-th column of $A$. 
We denote the $(i,j)$-minor of $A$ by $M_{ij}(A)$ or, if the 
context allows, just by $M_{ij}$. 

For example, if 
$$
    A = 
    \begin{pmatrix} 
    1 & 2 & 3 \\
    4 & 5 & 6 \\
    7 & 8 & 9
    \end{pmatrix}
$$

Then, we have 
$$
    M_{11} = 
    \begin{pmatrix}
       5 & 6 \\
       8 & 9
    \end{pmatrix}, \
    M_{21} = 
    \begin{pmatrix}
        2 & 3 \\
        8 & 9
    \end{pmatrix}, \
    M_{23} = 
    \begin{pmatrix}
        1 & 2 \\
        7 & 8
    \end{pmatrix} 
$$

**Definition**. We define a function 
$$
    \det : \operatorname{Mat}_{n \times n}(k) \to k 
$$
recursively on $n$. For $n=1$, we set 
$$
    \det(a) := a
$$
For $n > 1$, we set 
$$
    \det A := \sum_{i=1}^n (-1)^{i-1} A_{i1} \det M_{i 1}
$$

This formula is often called a _cofactor expansion_ for 
the determinant. 

Let's write out a closed form formula for small values of $n$:
- Since $n=1$ is already given, let's take a look at $n=2$. 
Then, for 
$$
    A = 
    \begin{pmatrix} 
        a & b \\
        c & d 
    \end{pmatrix}
$$
we have 
$$
    \det A = a \det(d) - c \det(b) = ad-bc
$$
- For $n=3$, with
$$
    A = 
    \begin{pmatrix} 
        a & b & c \\
        d & e & f \\
        g & h & i 
    \end{pmatrix}
$$
we have 
$$
    \begin{aligned}
        \det A & = a \det \begin{pmatrix} e & f \\ h & i \end{pmatrix} - 
        d \det \begin{pmatrix} b & c \\ h & i \end{pmatrix} + 
        g \det \begin{pmatrix} b & c \\ e & f \end{pmatrix}  \\ 
        & = a (ei -fh) - d(bi-ch) + g(bf-ce) \\
        & = aei - afh - bdi + bfg + cdh - ceg 
    \end{aligned}
$$

At this point, you realize you never want to try to remember 
the closed form for the cofactor expansion. The recursive definition is 
far more amenable to human consumption and usage. 

Now, let's state that this definition actually meets the specification 
for a determinant. 

A proof is not necessarily hard, in terms of requiring new ideas, but it 
is too time consuming for us. We will therefore content ourselves with 
a skim of the ideas involved. 

- First, one shows that 
$$
    \det (P(i,j) A) = - \det A
$$
This comes by working inductively and carefully analyzing the 
terms in the sum 
$$
    \det (P(i,j) A) = \sum_{l=1}^n (-1)^{l-1} (P(i,j)A)_{l1} \det(M_{l1}(P(i,j)A))
$$
and comparing them to $A_{l1}$ and $P(u,v)M_{l1}(A)$. 

- Next, one checks that 
$$
    \det (S(i,c) A) = c \det A
$$
This one is a bit simpler but follows the same lines: working via induction 
and analyzing the terms in the sum for the cofactor expansion. 

- Finally, one checks that 
$$
    \det (L(i,j,c)A) = \det A
$$
again working along the same lines. 

We see that $\det$ is multiplicative when using the elementary operation matrices 
on $A$. It turns out this enough. 

In another direction, it turns out the multiplicativity of a determinant 
is actually determined by multiplicativity using elementary row operations. 

**Theorem**. Assume 
$$
    \operatorname{det}^\prime : \operatorname{Mat}_{n \times n}(k) \to k
$$
satisfying 
- 
$$
    \operatorname{det}^\prime(L(i,j,c) A) = \operatorname{det}^\prime A
$$
- 
$$
    \operatorname{det}^\prime(S(i,c)A) = c \operatorname{det}^\prime A
$$
- 
$$
    \operatorname{det}^\prime(P(i,j) A) = - \operatorname{det}^\prime A
$$

Then, $\det^\prime$ is a determinant. 

**Corollary**. The cofactor expansion formula gives a determinant. 

In fact, one can prove the more general cofactor expansion formula for 
the determinant.  

**Proposition**. For any $1 \leq j \leq n$, we have
$$
    \det A = \sum_{i = 1}^{n=1} (-1)^{i+j-1} A_{ij} \det M_{ij}
$$

This allows us to expand along any column at the cost of a sign. 

We can also expand along rows. 

**Proposition**. For any $1 \leq i \leq n$, we have
$$
    \det A = \sum_{j = 1}^{n=1} (-1)^{i+j-1} A_{ij} \det M_{ij}
$$

For a fuller discussion of the details of the results, a good 
reference is the suggested textbook [Chapter 4 Section I.4 of 
Hefferon's Linear Algebra](https://joshua.smcvt.edu/linearalgebra/book.pdf). 

For us, it is important to know that 
- determinants exist and 
- there are many interesting formulas to compute them. 

But, we understand determinants through their properties and compute 
them using Gaussian Elimination or a factorization. 