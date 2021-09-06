---
layout: page
title: Equations for solvability
nav_order: 12
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
work_in_progress: false
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Equations for solvability of inhomogeneous systems

[Gaussian Elimination]({% link notes/solving_linear_systems/gaussian_elimination.md %}) and 
[row echelon form]({% link notes/solving_linear_systems/row_echelon_form.md %}) provide a 
simple and efficient means to check if a system $(A \mid b)$ has a solution or not. 

Perform Gaussian Elimination to reduce $A$ into row echelon form and then see if we have a row 
of the form $(\mathbf{0} \mid c)$ with $c \neq 0$. If so, there is no solution. If not, there will 
be a solution. 

One useful observation: if our system is of the form $A \mathbf{x} = \mathbf{0}$ to start with, then 
we will always have $0$ entries in the augmented portion of the matrix at any step of 
Gaussian Elimination. Thus, systems with $\mathbf{b} = \mathbf{0}$ will always have a solution. 

In retrospect, this is pretty easy see. We know $\mathbf{x} = \mathbf{0}$ solves $A \mathbf{x} = \mathbf{0}$. 

For such systems, we know that there either 
- there is a unique solution or
- there are infinitely many solutions. 

### Homogeneous vs inhomogeneous systems 

Given what we learned above, it makes sense to give such systems a name.

A system of the form 
$$
    A\mathbf{x} = \mathbf{0}
$$  
is called a _homogeneous_ linear system. 

A system 
$$
    A\mathbf{x} = \mathbf{b}
$$
with $\mathbf{b} \neq \mathbf{0}$ is called _inhomogeneous_. 

Restating our observations, a homogeneous system always has at least one solution, though it 
may be infinitely many. 

On the other hand, inhomogeneous systems may or may not have solutions in general. 

What can we say about the set 
$$
    \mathcal R(A) := \lbrace \mathbf{b} \mid A\mathbf{x} = \mathbf{b} \text { is solvable} \rbrace \ ?
$$
This set is called the _range_ of $A$. It, itself, is the solution set of a different linear system!

### Equations on the inhomogeneous term

Let's see how this works in an example. For general $\mathbf{b}$, let's use Gaussian Elimination to 
simplify the system:
$$
    5 x_1 + 3x_2 + x_3 = b_1 \\
    x_1 - x_2 + x_3 = b_2 \\
    x_2 + x_3 = b_3 \\
    3x_1 - x_3 = b_4 
$$

The augemented matrix is 
$$
    \begin{pmatrix} 
        5 & 3 & 1 & \bigg| & b_1 \\
        1 & -1 & 1 & \bigg| & b_2 \\
        0 & 1 & 1 & \bigg| & b_3 \\
        3 & 0 & -1 & \bigg| & b_4
    \end{pmatrix}
$$

If we convert this to row echelon form, we get 
$$
    \begin{pmatrix} 
        1 & -1 & 1 & \bigg| & b_2 \\
        0 & 1 & 1 & \bigg| & b_3 \\
        0 & 0 & -7 & \bigg| & b_4-3b_2-3b_3 \\
        0 & 0 & 0 & \bigg| & b_1 + b_2/7 - 20b_3/7 - 12b_4/7
    \end{pmatrix} 
$$
Thus, we have a solution to $A \mathbf{x} = \mathbf{b}$ if and only if 
$$
    b_1 + \frac{1}{7}b_2 - \frac{20}{7}b_3 - \frac{12}{7} b_4 = 0
$$
or in terms of the new notation 
$$
    \mathcal R(A) = \left\lbrace \mathbf{b} \mid b_1 + \frac{1}{7}b_2 - \frac{20}{7}b_3 - \frac{12}{7} b_4 = 0 \right\rbrace
$$

If we set 
$$
    B = \begin{pmatrix} 
            1 & 1/7 & -20/7 & -12/7 
        \end{pmatrix}
$$
then 
$$
    \mathcal R(A) = \mathcal Z(B).
$$
In other words, the set of $\mathbf{b}$ making $A\mathbf{x} = \mathbf{b}$ solvable is itself, in fact, the 
solution set of another system $B \mathbf{b} = \mathbf{0}$. 

We know how to give a parametric presentation of $\mathcal Z(B)$; we just eliminate the variables 
$$
    b_1 = -\frac{1}{7}b_2 + \frac{20}{7}b_3 + \frac{12}{7} b_4.
$$

So $b_2,b_3,b_4$ are free variables and $b_1$ is determined by from these by this equation. 

This is a general phenomenon. 

**Theorem**. Given a matrix $A$, there exists another matrix $B$ so that 
$$
    \mathcal R(A) = \mathcal Z(B).
$$ 
Moreover, one can find such a $B$ by applying Gaussian Elimination to $(A \mid b)$ and 
take $B$ to be the coefficient matrix for the system given by all the zero rows. 

**Proof**. We have built up enough technology to show this quickly. 

If $(A^\prime \mid b^\prime)$ is the resulting matrix in row echelon form, then 
- each $b_i^\prime$ is a linear combination of the original $b_j$
- and $b_i^\prime = 0$ must be satisfied for each zero row $\mathbf{R}_i^{A^\prime}$. 