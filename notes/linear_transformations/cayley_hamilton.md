---
layout: page
title: Cayley-Hamilton
nav_order: 12
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: true
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## The Cayley-Hamilton Theorem 

For an $n \times n$ matrix $A$, we have already seen one polynomial: 
the characteristic polynomial $\chi_A$. 

There is another important polynomial associated to $A$: its 
_minimal polynomial_ $m_A$. 

**Definition**. Let $A$ be a $n \times n$ matrix over a field $k$ and 
let $p(x)$ be a polynomial with coefficient in $k$. We say that 
$A$ _satisfies_ $p(x)$ if 
$$
p(A) = 0 
$$

Let's look at some examples. 

**Example**. 
- Let's take $A = I_n$ the identity matrix. Then, $A$ satisfies the 
polynomial $x-1$. Notice that to make sense of plugging in a matrix 
we need to promote $1$ to a $n \times n$ matrix itself. We do this 
by replace the constant term $c$ by $cI_n$. Thus, 
$$
	I_n - I_n = 0 
$$

- Let's take 
$$
A = 
\begin{pmatrix}
1 & -1 \\
1 & 1 
\end{pmatrix}
$$
Then, $A$ will not satisfy any polynomial of degree $1$ since it is 
not equal to $cI_2$ for any scalar $c$. Let's try to find a degree 
polynomial that $A$ satisfies. We have 
$$
A^2 = 
\begin{pmatrix}
0 & -2 \\
2 & 0 
\end{pmatrix}
$$
Note that 
$$
 A^2 -2A + 2I_2 = 0 
$$
Thus $A$ satisfies $x^2 - 2z + 2$. You might notice that this is 
_also_ the characteristic polynomial of $A$. 

**Theorem** (Cayley-Hamilton). A $n \times n$ matrix satisfies 
its own characteristic polynomial.  

Unforunately, we don't have time to delve into a proof of this result 
but it involves some fundamental ideas in modern algebra. 

We will content ourselves with observing some consequences. A polynomial 
is called _monic_ if its leading coefficient is $1$, ie 
$$
p(x) = x^d + a_{d-1} x^{d-1} + \cdots + a_0 
$$

**Definition**. The _minimal polynmomial_ of $A$ is the minimal degree 
monic polynomial that $A$ satisfies. We denote as $m_A(x)$. 

In both our examples, we have actually written down minimal polynomials. 

**Corollary**. The degree of $m_A(x)$ is at most $n$. 

{% include beginproof.html %}
By Cayley-Hamilton, $A$ satisfies $\chi_A(x)$. We have seen that 
$(-1)^n\chi_A(x)$ is a monic polynomial. Since $m_A(x)$ is the minimal 
degree monic polynomial satisfied by $A$, we must have 
$$
\operatorname{deg} m_A(x) \leq n 
$$
{% include endproof.html %}

In fact, one can deduce that there is another polynomial $r(x)$ such 
that 
$$
\chi_A(x) = m_A(x) r(x) 
$$
so that $m_A(x)$ actually _divides_ $\chi_A(x)$. 

We also know how the roots of the two polynomials compare. 

**Theorem**. The roots of $m_A(x)$ and the roots $\chi_A(x)$ are equal 
sets. 

Let's see how these compare in some examples. 

**Example**. 
- For the identity matrix $I_n$, we have 
$$
\chi_{I_n) = (1-x)^n 
$$
and 
$$
m_{I_n}(x) = x-1
$$
so clearly $m_{I_n} \mid \chi_{I_n)$ and they are pretty far from equal. 

- Consider the matrix 
$$
A = 
\begin{pmatrix}
1 & 1 \\
0 & 1 
\end{pmatrix}
$$
Then, $A$ has the same characteristic polynomial as $I_2$ 
$$
\chi_A(x) = (1-x)^2
$$
but its minimal polynomial is 
$$
m_A(x) = (1-x)^2 = (x-1)^2
$$
equal to its characteristic polynomial. 

