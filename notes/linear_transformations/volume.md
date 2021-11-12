---
layout: page
title: Volumes
nav_order: 9
has_children: false
has_toc: false
parent: Linear Transformations
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Volumes and determinants

Determinants also relate to volumes of geometric objects. It may 
seem silly but let's look at the one-dimensional setting first. 
(In general, if you don't understand the 1-d setting, then you 
should start your learning there.) 

In $\mathbb{R}^1 = \mathbb{R}$, a vector is just a scalar or a 
element of $\mathbb{R}$. The length of the vector $a$ is $|a|$. 
In 1-d, length is volume. So we have the following 
relation between the volume of the line segment $P(a)$ spanned 
by $a$ is 
$$
    \operatorname{Vol}(P(a)) = |\det(a)|
$$
The determinant is a signed volume in 1-d. 

With some confidence with one dimension, we turn to 2-d. 
Let's start with a $2 \times 2$ matrix
$$
    A = \begin{pmatrix} a & b \\ c & d \end{pmatrix}
$$
The columns give up two vectors 
$$
    \mathbf{v}_1 = \begin{pmatrix} a \\ c \end{pmatrix}, \ 
    \mathbf{v}_2 = \begin{pmatrix} b \\ d \end{pmatrix} 
$$
The vectors $\mathbf{v}_1, \mathbf{v}_2$ span a parallelogram 
$P = P(A)$. 
<center>
<img src="/assets/images/svg/parallelogram.svg" title="Parallelogram 
spanned by two vectors">
</center>
Let's check that 
$$
    \operatorname{Vol}(P(A)) = |\det(A)| 
$$

Neither the volume nor the determinant depend on where we place the 
parallelogram in the plane so assume that the unlabelled vertex is 
at the origin.

Let's rotate $P$ so that $\mathbf{v}_1$ lies along the $x$-axis. 
<center>
<img src="/assets/images/svg/rotated_parallelogram.svg" title="Rotated parallelogram 
spanned by two vectors">
</center>
Notice that 
$$
    \mathbf{v}_1^\prime = \begin{pmatrix} a^\prime \\ 0 \end{pmatrix}, \
    \mathbf{v}_2^\prime = \begin{pmatrix} b^\prime \\ d^\prime \end{pmatrix}
$$
so for the rotated matrix 
$$
    \det A^\prime = a^\prime d^\prime 
$$
which is exactly the volume of the rotated parallelogram $P^\prime$ 
(base $\times$ height). 

To finish, we want to see that the determinant also does not change up 
when rotating in $\mathbb{R}^2$. However, a rotation is a linear 
transformation! So it can be represented by a matrix when using 
the standard basis. For rotating counter-clockwise through an 
angle $\theta$ from $x$-axis, we have
$$
    R_\theta := 
    \begin{pmatrix} 
        \cos(\theta) & -\sin(\theta) \\
        \sin(\theta) & \cos(\theta)
    \end{pmatrix}
$$
as the matrix. Since
$$
    A^\prime = R_\theta A 
$$
we get
$$
    \det A^\prime = \det(R_\theta) \det(A) 
$$
and 
$$
    \det R_\theta = \cos^2 \theta + \sin^2 \theta = 1. 
$$
So the determinant is unchanged also. 

We can conclude that 
$$
    \operatorname{Vol} P = |\det(A)|
$$
in 2-d, like 1-d. 

We feel pretty good about making the following statement. 

For any $n \times n$ matrix $A$ we have 
$$
    \operatorname{Vol} P(A) = |\det(A)|
$$
where $P(A)$ is the parallelopiped spanned by the column 
vectors of $A$. 

In three dimensions, the parallelopiped looks like 
<center>
<img src="/assets/images/svg/parallelopiped.svg" title="Three dimensional 
parallelopiped">
</center>
For higher dimensions, we rely on our intuition from dimensions 
1 through 3. 

The proof of 
$$
    \operatorname{Vol} P(A) = |\det(A)|
$$
can go one of two ways:
- We can brute force things along lines of two dimensions above. 
Use explicit formulas and manipulations to match up the results. 
- Or we can reach for the power of abstraction and use the 
properties that completely capture the behavior 
$\operatorname{Vol}$ and $|\det(A)|$. 

**Proposition**. If 
$$
    f,g : \operatorname{Mat}_{n \times n}(\mathbb{R}) \to \mathbb{R}
$$
are two functions which both satisfy 
- 
$$
    \phi(L(i,j,c)A) = \phi(A)
$$
- 
$$
    \phi(P(i,j)A) = \phi(A) 
$$
- 
$$
    \phi(S(i,c)A) = |c|\phi(A) 
$$ 
- 
$$
    \phi(I_n) = 1. 
$$
- and 
$$
    \phi(A) = 0 
$$
for singular $A$.

Then, $f = g$. 

{% include beginproof.html %}
From Gaussian Elimination, we know that any matrix can be written as 
$$
    A = C U
$$
where $C$ is a product of $L(i,j,c), S(i,c)$, and $P(i,j)$ and $U$ 
is in reduced row echelon form. Thus, 
$$
    \phi(A) = \phi(U)
$$
and $\phi$ only depends on the reduced row echelon form. We have seen 
that $A$ is invertible if and only $U = I_n$. Thus, we have 
specified $\phi(A)$ for invertible $A$ completely from the properties. 

For non-invertible $A$, we know that $\phi(A) = 0$. 
{% include endproof.html %}

**Corollary**. For any $n \times n$ matrix $A$ we have 
$$
    \operatorname{Vol} P(A) = |\det(A)|
$$
where $P(A)$ is the parallelopiped spanned by the column 
vectors of $A$. 

{% include beginproof.html %}
Both $\operatorname{Vol}(P(-))$ and $|\det(-)|$ satisfy the conditions 
of the previous proposition. 

We have already 
[seen]({% link notes/linear_transformations/determinants.md %}) 
that $\det(A)$ satisfies all the conditions with the exception that 
$$
    \det(P(i,j)A) = -\det(A) 
$$
But the absolute value doesn't change. 

For the volume, we know it doesn't change with rigid motions. Let's 
write $\mathbf{v}_1,\ldots,\mathbf{v}_n$ be the _row_ vectors of 
$A$. Then, we have an intuitively clear formula
$$
    \operatorname{Vol} (P(A)) = \operatorname{ht}(\mathbf{v}_i}) 
    \operatorname{Vol} (P_i)
$$
where $P_i$ is the parallelopiped spanned by all the vectors
$\mathbf{v}_1,\ldots,\mathbf{v}_n$ _except_ $\mathbf{v}_i$ and 
$\operatorname{ht}(\mathbf{v}_i})$ is height of $\mathbf{v}_i$ 
above that parallelopiped. (We should really prove this too but 
we will rely a bit on "geometric intuition" here and below.)

From this formula, we see that 
$$
    \operatorname{Vol}(P(P(i,j)A)) = \operatorname{Vol}(P(A))
$$
and 
$$
    \operatorname{Vol}(P(S(i,c)A)) = |c|\operatorname{Vol}(P(A))
$$
using induction on $n$. 

For 
$$
    \operatorname{Vol}(P(L(i,j,c)A)) = \operatorname{Vol}(P(A))
$$
we note that the height of $\mathbf{v}_j + c\mathbf{v}_i$ 
has the same height above $P_j$ as $\mathbf{v}_j$. 

Finally, the volume of $P(I_n)$ is the volume of the unit 
cube in $n$-dimensions which is $1$. And if $A$ is singular, 
then it spans at most a $(n-1)$-dimensional subspace and 
must have $0$ volume. 
{% include endproof.html %}

This corollary tells us that the determinant can also 
be viewed as a way to provide signed volumes in all dimensions. 
This is useful for multi-variable integration, for example, which 
is why you find determinants showing up in change of variable 
formulae for multi-variable integrals. 