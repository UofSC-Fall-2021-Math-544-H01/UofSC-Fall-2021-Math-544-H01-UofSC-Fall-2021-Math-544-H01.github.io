---
layout: page
title: Fields
nav_order: 1
has_children: false
has_toc: false
parent: Vector spaces
grand_parent: Notes
work_in_progress: true
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Fields 

Before we talk about vector spaces, we first need to talk about scalars. Up to 
this point, we have been treating our scalars as real numbers. 

But, it turns out that real numbers are a special case of more general notion. 
Other examples of this more general notion can be quite interesting. 

### Definition 

A _field_ $k$ is a set equipped with two operations 
$$
    \begin{aligned}
        + : k \times k & \to k \\ 
        \times : k \times k & \to k 
    \end{aligned}
$$
satsifying the following the conditions:
- $+$ and $\times$ are associative. This means that for any 
$a,b,c \in k$ we have 
$$
    (a + b) + c = a + (b + c)
$$
and 
$$
    (a \times b) \times c = a (b \times c)
$$
In other words, order of application does not affect the result of 
applying either $+$ or $\times$ to a list of elements. 
- $+$ and $\times$ are commutative. This means that for any $a,b \in $k
$$
    a + b = b + a
$$
and 
$$
    a \times b = b \times a
$$
In other words, we can swap the inputs for both $+$ and $\times$ 
and the outputs remain the same. 
- We can distribute $\times$ over $+$. For any $a,b,c \in k$, we have 
$$
    a \times (b + c) = a \times b + a \times c 
$$
- There is a special element denoted $0 \in k$ with the property that 
for any $a \in k$ we have
$$
    a + 0 = 0 + a = a
$$
This element is called the identity for $+$. 
- There is special element often denoted $1 \in k$ with the property that 
$$
    a \times 1 = 1 \times a = a
$$
for any $a \in k$. This element is called the identity for $\times$. 
- For any element $a \in k$, there is another element $-a \in k$ with 
so that 
$$
    a + (-a) = (-a) + a = 0 
$$
- Finally for any $a \in k$ with $a \neq 0$, there is another element 
$a^{-1} \in k$ satisfying 
$$
    a \times a^{-1} = a^{-1} \times a = 1. 
$$

### Examples 

- The most familiar example is the real numbers $\mathbb{R}$ where $+$ is 
addition and $\times$ is multiplication. $0$ is zero and $1$ is one. The 
additive inverse to $r$ is just $-r$ or negative $r$ while the multiplicative 
inverse $r^{-1}$ is $1/r$. 

- In $\mathbb{R}$, we have the field of rational numbers of $\mathbb{Q}$. 
These are all real numbers that can be reprsented as a ratio $r = m/n$ of 
integers $m,n$ with $n \neq 0$. 

    Given a rational number $q$, $-q$ is rational as is $1/q$ if $q \neq 0$. 
    Both $0$ and $1$ also rational numbers. 

    It is useful to note that not all real numbers are rational. For example, 
    $\pi$ is known to be irrational. 

- A class of examples that are more novel are finite fields. We can consider 
the set $\lbrace 0,1 \rbrace$ alone. Declaring that $0$ is the additive 
identity determines $+$ most pairs
$$
    \begin{aligned} 
        0 + 0 & = 0 \\
        1 + 0 & = 1 \\
        0 + 1 & = 1 
    \end{aligned}
$$
We also need an additive inverse to $1$. It cannot be $0$ since $0 + 1 = 1$. 
So it must be $1$: 
$$
    1 + 1 = 0 
$$
Similarly, having $1$ be the multiplicative identity forces 
$$
    \begin{aligned} 
        1 \times 1 & = 1 \\
        1 \times 0 & = 0 \\
        0 \times 1 & = 0 
    \end{aligned}
$$
What could $0 \times 0$ be? If $0 \times 0 = 1$, then we have a problem with 
associativity:
$$
    (0 \times 0) \times = 1 \times 1 = 1
$$
while 
$$
    0 \times (0 \times 1) = 0 \times 1 = 0
$$
which are not equal. So $0 \times 0 = 0$. 

    The set $\lbrace 0,1 \rbrace$ with this choice of $+$ and $\times$ is also a field, 
    often written $\mathbb{F}_2$ since it has two elements. 

    An interesting incarnation of $\mathbb{F}_2$ is obtained by replacing $0$ with False or $F$ 
    and $1$ with True or $T$. Then $+$ is the exclusive or (XOR) operation while $\times$ is 
    the and operation on the set $\lbrace F, T \rbrace$. 

    For any prime number $p$ and any natural number $r > 0$, there are also fields 
    $\mathbb{F}_{p^r}$ with $p^r$ many elements. 

- Finally, the complex numbers $\mathbb{C}$ are a field built by taking $\mathbb{R}$ and 
pretending we have a solution $\imath$ to $x^2 = -1$.  

    The elements of $\mathbb{C}$ are written as $a + b \imath$ for $a, b \in \mathbb{R}$. 
    $0$ is $0 + 0 \imath$ and $1$ is $1 + 0 \imath$. We add complex numbers as 
    $$
        (a + b \imath ) + (c + d\imath) = (a+c) + (b+d) \imath 
    $$
    and we multiply them via 
    $$
        (a + b \imath ) (c + d\imath) = (ac - bd) + (ad + bc) \imath
    $$
    You can quickly convince yourself that this is the same as allowing us to distribute multiplication 
    over addition and using multiplication in $\mathbb{R}$ plus $\imath^2 = -1$.

    The additive inverse to $a + b \imath$ is $-a - b\imath$ but what is the multiplicative 
    inverse? 
    $$
        (a + b\imath)^{-1} = \frac{a - b \imath}{a^2 + b^2}
    $$
    which makes sense for all $a + b\imath \neq 0$. 

    Adding $\imath$ to $\mathbb{R}$ to make $\mathbb{C}$ is surprisingly powerful. The complex 
    numbers make appearances in surprising places from understanding the motion of water waves to 
    the fabric of our universe. 