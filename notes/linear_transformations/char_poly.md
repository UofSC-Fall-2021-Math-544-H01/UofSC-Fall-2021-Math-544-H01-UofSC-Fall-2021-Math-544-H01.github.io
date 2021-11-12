---
layout: page
title: Characteristic Polynomials
nav_order: 10
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: true
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## The characteristic polynomial 

Let's start with $T: V \to V$ a linear transformation 
between finite dimensional vector spaces. 

**Lemma**. For a linear transformation $T : V \to V$ 
with $\dim V < \infty$, we have $\mathcal Z(T) = 0$
if and only if $T$ is an isomorphism. 

{% include beginproof.html %}
To check that $T$ is an isomorphism it 
[suffices]({% link homework/09.md %}) to check $T$ 
is a bijection and it [suffices]({% link worksheets/17.md %})
to show that $\mathcal Z(T) = 0$ and $\mathcal R(T) = V$ to 
check it is bijection. 

So clearly if $T$ is an isomorphism, we must have $\mathcal Z(T) = 0$. 

In the other direction, we use the 
[Rank Nullity Theorem]({% link notes/linear_transformations/kernels_ranges.md %})
$$
    \dim \mathcal Z(T) + \dim \mathcal R(T) = \dim V
$$

Assume that $\mathcal Z(T) = 0$. Then, 
$$
    \dim \mathcal R(T) = \dim V
$$
so [$\mathcal R(T) = V$]({% link notes/vector_spaces/bases.md %}#consequences)
{% include endproof.html %}

We have [seen]({% link worksheets/21.md %}) that 
$\lambda$ is eigenvalue for $T$ if and only if 
$$
    \mathcal Z(T - \lambda \operatorname{Id}) \neq 0
$$

Let's pick a basis and get a matrix representation $A$ of 
$T$. With the matrix, we have the power of the determinant. 

**Proposition**. $\lambda$ is an eigenvalue of $A$ if and only 
$$
    \det (A - \lambda I_n) = 0 
$$

{% include beginproof.html %}
From the discussion above, we know that $\lambda$ is an eigenvalue if 
and only $\mathcal Z(A-\lambda I_n) \neq 0$. 

We know that $\mathcal Z(A -\lambda I_n) \neq 0$ if and only if 
$A - \lambda I_n$ invertible from the previous lemma. Finally, 
we [saw that](% link notes/linear_transformation/determinants.md %) 
$A - \lambda I_n$ is invertible if and only 
$$
    \det(A - \lambda I_n) \neq 0. 
$$
{% include endproof.html %}

This proposition tells us we really want to understand the zeroes 
of a function of a single variable. 

**Definition**. The _characteristic polynomial_ $\chi_A(x)$ of a 
$n \times n$ matrix $A$ is the function 
$$
    x \mapsto \det(A - xI_n)
$$

We should probably check $\chi_A(x)$ is actually a polynomial in 
$x$. Before giving a general proof, let's look at some low dimensions. 

For $A = (a)$, we just have 
$$
    \chi_A(x) = x-a
$$

For 
$$
    A = \begin{pmatrix} 
    a & b \\
    c & d 
    \end{pmatrix}
$$
we have 
$$
    A - xI_2 = 
    \begin{pmatrix} 
    a-x & b \\
    c & d-x 
    \end{pmatrix}
$$
and so 
$$
    \chi_A(x) = (a-x)(d-x) - bc = x^2 - (a+d)x + (ad-bc)
$$

For 
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
    A - xI = 
    \begin{pmatrix} 
        a-x & b & c \\
        d & e-x & f \\
        g & h & i-x 
    \end{pmatrix}
$$
We compute $\chi_A(x)$ using a cofactor expansion along the top row: 
$$
    \begin{aligned}
    \chi_A(x) & = (a-x) \det\begin{pmatrix} e-x & f \\ h & i-x\end{pmatrix} - 
    b \det \begin{pmatrix} d & f \\ g & i-x\end{pmatrix} + 
    c \det \begin{pmatrix} d & e-x \\ g & h \end{pmatrix} \\
    & = (a-x)(e-x)(i-x) - (a-x)fh - bd(i-x)+bfg + cdh - cg(e-x) \\
    & = -x^3 + (a+e+i)x^2 - (ae+ai+ie-fh-bd-cg)x \\ 
    & + aei - afh - bdi + bfg + cdh - ceg
    \end{aligned}
$$

In general, we have the following result. A polynomial $p(x)$ of degree $d$ is called 
_monic_ if 
$$
    p(x) = x^d + a_{d-1}x^{d-1} + \cdots + a_0
$$

**Proposition**. For any $n \times n$ matrix $A$, $\chi_A(x)$ is a monic 
polynomial of degree $n$ with constant coefficient equal to $\det A$. 

{% include beginproof.html %}

{% include endproof.html %}

A scalar $a \in k$ is a _root_ of a polynomial $p(x)$ if 
$$
    p(a) = 0. 
$$

Thus, to find the eigenvalues of $A$, we need to find the roots of $\chi_A(x)$. 

**Example**. Let's compute the eigenspaces of 
$$
    A = 
    \begin{pmatrix}
        0 & -1 \\
        1 & 2 
    \end{pmatrix}
$$
We do this by first finding the eigenvalues using 
the characteristic polynomial. 

We have 
$$
    A - xI = 
    \begin{pmatrix}
        -x & -1 \\
        1 & 2-x
    \end{pmatrix}
$$
so 
$$
    \det(A -xI) = -x(2-x)-1 = -x^2 - 2x -1 = -(x+1)^2
$$
We see that the only eigenvalue is $-1$. 

Now, we want to find the null space of $A - \lambda I$ 
for each eigenvalue. The null space of 
$$
    A + I = 
    \begin{pmatrix}
        -1 & -1 \\
        1 & 1
    \end{pmatrix}
$$
is 
$$
    E_{-1}(A) = \left\lbrace \begin{pmatrix} a \\ - a \end{pmatrix} \mid a \in k \right\rbrace
$$
This is one dimensional so we do not have a basis of eigenvectors 
for $A$. 

