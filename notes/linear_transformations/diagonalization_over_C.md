---
layout: page
title: Diagonalization over $\mathbb{C}$
nav_order: 11
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: true
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Roots over $\mathbb{C}$

As you might have seen, for a quadratic polynoial $ax^2+bx+c$, 
we have a formula for the roots 
$$
\frac{-b \pm \sqrt{b^2 - 4ac}}{2a} 
$$
However, we cannot make sense of this as a real number if 
$$
b^2 - 4ac < 0 
$$

As mentioned briefly before, $\mathbb{R}$ is a subfield of a 
larger field, the complex numbers $\mathbb{C}$. 

In general, to build new fields from old ones, we _pretend_ 
we have a root to a polynomial which actually has no 
root. This process is called _adjoining a root_. 

The complex numbers come from adjoining a root to the 
equation 
$$
x^2 + 1 = 0 
$$
We introduce a new symbol $\imath$ which satisfies the 
algebraic identity 
$$
\imath^2 = -1
$$

With this symbol in hand, we can now make sense of any negative 
root in $\mathbb{C}$. For example, 
$$
\sqrt{-5} = \imath \sqrt{5}
$$

The elements of $\mathbb{C}$ are sums 
$$
a + \imath b 
$$
with $a,b \in \mathbb{R}$. We add two complex numbers as if we 
were adding a two-dimensional vector:
$$
a + b \imath + c + d \imath = (a+c) + (b+d)\imath 
$$
We mulitply using distributivity and remembering $\imath^2 = -1$:
$$
(a + b \imath)(c + d\imath) = ac + ad\imath + bc \imath + bd\imath^2 = 
(ac-bd) + (ad+bc)\imath 
$$

This is indeed a field though we won't provide all the details of the 
proof. The additive inverse is 
$$
-(a + b \imath) = -a - b\imath 
$$
which is, again, the same as if we treated $a + b\imath$ as the 
vector $(a,b)$. The zero element $0$ of $\mathbb{C}$ is $a=b=0$. The 
multiplicative identity $1$ is $a=1$ and $b=0$.  

**Lemma**. Let $a+b\imath$ be a nonzero complex number. Then, 
$$
(a+b\imath) \left(\frac{a-b\imath}{a^2+b^2} \right) = 1
$$

Therefore, 
$$
(a+b\imath)^{-1} = \frac{a-b\imath}{a^2+b^2}
$$

{% include beginproof.html %}
Let's first note that if $a +b \imath \neq 0$, then either $a \neq 0$ or 
$b \neq 0$. In either case $a^2 + b^2 \neq 0$ so the division in the 
formula is well-defined. We have 
$$
(a+b\imath)(a-b\imath) = a^2 + b^2 
$$
so 
$$
(a+b\imath) \left(\frac{a-b\imath}{a^2+b^2} \right) = 1
$$
{% include endproof.html %}

**Definition**. In general, the complex number $a-b\imath$ is called 
the _complex conjugate_ of $a+b\imath$. The complex conjugate of 
$z$ is denoted by $\overline{z}$. 

Thus, 
$$
z^{-1} = \frac{\overline{z}}{z\overline{z}}
$$

**Example**. So 
$$
(1-\imath)^{-1} = \frac{1}{2}(1 + \imath) 
$$

It turns out that adjoining a root of $x^2+1$ to $\mathbb{R}$ actually 
gives _all roots to any polynomial_. The following result is the 
strongest argument for the utility of complex numbers (with their 
use in quantum mechanics a close second). 

As convention, instead of using $x$ to denote a variable, we use 
$z$ to denote a complex variable. If we write $z = a+b\imath$, then 
we say $a$ is the _real part_ of $z$ and $b$ is the 
_imaginary part_ of $z$. We denote the real part by $Re(z)$ and the 
imaginary part by $Im(z)$.  

**Theorem** (The Fundamental Theorem of Algebra). Let $p(z)$ be a 
polynomial with complex coefficients. Then there is a $z_0 \in 
\mathbb{C}$ with 
$$
 p(z_0) = 0 
$$
In other words, any polynomial with coefficients in $\mathbb{C}$ 
has a root in $\mathbb{C}$. 

{% include beginproof.html %}
There are multiple interesting proofs of the Fundamental Theorem of 
Algebra, some algebraic, some analytic. 
{% include endproof.html %}

**Corollary**. Let $p(z)$ be a nonconstant polynomial one complex 
variable. Then, $p(z)$ factors completely: 
$$
	p(z) = a \prod_{i=1}^d (z-z_i) 
$$
for $a,z_1,\ldots,z_d \in \mathbb{C}$. 

{% include beginproof.html %}
We proceed by induction on the degree $d$ of $p(z)$. For $d=1$, we 
already have $p(z) = az+b$ and we take $z_1 = -b/a$. 

Now assume we know the result is true for degree $d-1$ and let 
$p(z)$ have degree $d$. From the Fundamental Theorem of Algebra, we 
have a root $z_d$ of $p(z)$. Thus, 
$$
p(z) = (z-z_d)q(z) 
$$
for a polynomial of degree $d-1$. Applying the induction hypothesis, 
we get 
$$
p(z) = a \prod_{i=d} (z-z_i) 
$$
{% include endproof.html %}

For us, we are interested in characteristic polynomials $\chi_A$ of 
$n \times n$ matrices $A$. 

We have already seen that we need not have an eigenvector in general 
for a matrix over $\mathbb{R}$. This is not the case for $\mathbb{C}$.

**Proposition**. Any $n \times n$ matrix $A$ with entries in 
$\mathbb{C}$ has an eigenvector. 

{% include beginproof.html %}
From the Fundamental Theorem of Algebra, we know that $\chi_A(z)$ has 
root $\lambda$. Thus, $A$ has an eigenvector with eigenvalue $\lambda$. 
{% include endproof.html %}

Given a complex matrix $A$, its complex conjugate $\overline{A}$ 
is given by taking the complex conjugates of its entries
$$
\overline{A}_{ij} = \overline{A_{ij}}
$$

The next lemma shows that honest complex eigenvalues come in pairs. 

**Lemma**. Assume we have a real $n \times n$ matrix. If $\lambda$ is 
a complex eigenvalue of $A$, then so is $\overline{\lambda}$. Morever, 
$$
E_{\overline{\lambda}}(A) = \overline{E_{\lambda}(A))
$$

{% include beginproof.html %}
Taking the complex conjugate of 
$$
A v = \lambda v 
$$
gives 
$$
A \overline{v} = \overline{Av} = \overline{\lambda v} 
= \overline{\lambda} \overline{v} 
$$
which shows that $\overline{v}$ is also an $A$-eigenvector with 
eigenvalue $\overline{\lambda}$. 

This also shows that 
$$
\overline{E_{\lambda}(a)) \subseteq E_{\overline{\lambda}}(a)
$$
But, we can apply complex conjugation here to get 
$$
E_{\lambda}(A) = \overline{\overline{E_{\lambda}(A)}} \subseteq 
\overline{E_{\overline{\lambda}}(A)}
$$
Applying this, but replacing $\overline{\lambda}$ with $\lambda$ gives 
$$
\overline{E_{\lambda}(a)) \superseteq E_{\overline{\lambda}}(a)
$$
{% include endproof.html %}

We also have a simple criteria to determine whether there is basis 
of eigenvectors. 

**Proposition**. Let $A$ be a $n \times n$ matrix over a field $k$. 
Assume that $\chi_A(x)$ has $n$ distinct roots. Then, there is a basis 
of $k^n$ consisting of $A$-eigenvectors. 

In particular, $A$ is diagonalizable. 

{% include beginproof.html %}
We have to have at least on eigenvector for each distinct eigenvalue, 
ie each distinct root of $\chi_A(x)$. As we saw, if we have a set of 
eigenvectors with distinct eigenvalues, then that set is linearly 
independent. If we have $n$ distinct roots, then we have a linearly 
independent set of size $n$ in an $n$-dimensional vector space. This 
must span, so it is a basis. 

The matrix representation of $A$ in its basis of eigenvectors is 
a diagonal matrix, where the entries on the diagonal are the 
eigenvalues. 
{% include endproof.html %}

We work through an example. 

**Example**. Let's compute the eigenspaces of 
$$
A = 
\begin{pmatrix}
	0 & -1 \\
	2 & -2 
\end{pmatrix}
$$
The characteristic polynomial is 
$$
\chi_A(z) = x^2 + 2x + 2  
$$
Using the quadratic formula, we have roots 
$$
\frac{-2 \pm \sqrt{-4}{2} = -1 \pm \imath
$$
Note that since we have two distinct eigenvalues we already know 
we have a basis of $\mathbb{C}^2$ consisting of $A$-eigenvectors. 

Let's compute the eigenspaces. We want the null space of
$$
A - (-1 + \imath)I_2 = 
\begin{pmatrix}
1 - \imath & -1 \\
2 & -1 - \imath 
\end{pmatrix}
$$
For simplicity let's scale the first row so that the $(1,1)$ entry is 
$1$. We have 
$$
(1-\imath)^{-1} = \frac{1}{2}(1+\imath)
$$
Scaling we get 
$$
\begin{pmatrix}
1 & -\frac{1}{2}(1+\imath) \\
2 & -1-\imath 
\end{pmatrix} 
$$
Eliminating the second row using the first gives 
$$
\begin{pmatrix}
1 & -\frac{1}{2}(1+\imath) \\
0 & 0 
\end{pmatrix}
$$
Thus, the $(-1+\imath)$-eigenspace is 
$$
E_{-1+\imath}(A) = \left\lbrace \begin{pmatrix} \frac{1}{2}(1+\imath)w \\ 
w \end{pmatrix} \mid w \in \mathbb{C} \right\rbrace 
$$

As we saw above, we can get the eigenspace for the complex conjugate 
eigenvalue via complex conjugation: 
$$
E_{-1 - \imath}(A) = \overline{E_{-1+\imath}(A)} = \left\lbrace 
\begin{pmatrix} 
\frac{1}{2}(1-\imath)w \\ 
w 
\end{pmatrix} \mid w \in \mathbb{C} \right\rbrace
$$
