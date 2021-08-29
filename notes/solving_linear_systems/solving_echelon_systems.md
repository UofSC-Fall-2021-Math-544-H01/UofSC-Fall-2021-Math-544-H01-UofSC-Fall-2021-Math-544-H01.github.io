---
layout: page
title: Solving Echelon Systems
nav_order: 10
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
work_in_progress: true 
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Solving systems in row echelon form

It turns out understanding solutions of systems $[A \mid b]$ where 
$A$ is in row echelon form is quite simple. 

To get an sense of the situation, lets look at some examples. 

Consider 
$$
    [A \mid b] = 
    \begin{pmatrix}
        1 & -2 & 1 &\bigg| & 1 \\
        0 & 2 & 1 &\bigg| & 1 
    \end{pmatrix}
$$
This corresponds to the system
$$
    x - 2y + z = 1 \\
    2y + z = 2
$$
Reading bottom to top, we can eliminate variables by
* by solving for the variable in the pivot position and 
* substituting back into the system that solution. 

In this example, we would solve
$$
    2y + z = 2 
$$
for $y$. This yields 
$$
    y = \frac{z}{2} - 1
$$
Subsituting back in gives 
$$
    x - 2\left(\frac{z}{2} -1\right) + z = x - z + 2 = 1
$$
or 
$$
    x - z = -1.
$$
Notice that this is still in row echelon form but now has 
one few unknown and one fewer equation. 

To efficiently express the solution, we can write $x$ in 
terms of $z$ also. 
$$
    x = z-1. 
$$
We can conclude that, for any choice of the value $z$, the triple 
$$
    \left(z-1, \frac{z}{2}-1, z \right)
$$
is a solution to our system. Moreover, any solution is of this form.

We have completely captured all solutions of the system in terms 
of the free parameter $z$. This is an example of a _parametric solution_ 
to the linear system.  

### Edge cases (but not really) 

It would seem that we have generally described an algorithm for 
solving any system in echelon form. But, like in the case of 
[a single equation]({%link notes/solving_linear_systems/linear_equations.md %}#solving-a-single-linear-equation),
we are ignoring an important (but seemingly silly) case: 

**What if there is no pivot in a given row?**

We end up trying to solve an equation like 
$$
    0 = b_i 
$$
which will only work if $b_i = 0$ is actually a true statement!

For example, we won't be able to solve 
$$
    [A \mid b] = 
    \begin{pmatrix}
        1 & -2 &\bigg| & 1 \\
        0 & 2 &\bigg| & 1 \\
        0 & 0 &\bigg| & 1 
    \end{pmatrix}
$$
since the last row asks to us solve $0=1$ (not happening).  

### Bound vs free variables in a row echelon system 

Whether a variable corresponding column has a pivot turns out to be 
quite important for describing and understanding the solution of a system. 

Consequently, we provide some names. If the column corresponding to the 
variable's index has a pivot, we say the variable is _bound_. Otherwise, 
we say that the variable is _free_. 

### Algorithm for solving systems in reduced row echelon form  

For a system in reduced row echelon form, computations simply even more. 

### Step 1

If there is a row of the form $0 = b$ where $b \neq 0$, output No Solution.

### Step 2 

For the last nonzero row, solve for the bound variable $x_i$ in that row in terms 
of the free variable. 

### Step 3

Substitute the expression from Step 2 back in to the eliminate the bound variable $x_i$ 
from the system. Eliminate the corresponding row and column from the pivot. 

Go back to to Step 2. 

When the algorithm terminates (assuming it does not terminate with "No Solution"), 
we will have generated expressions of the form 
$$
    x_j = \sum_{\text{ free variables }} c_i x_i 
$$
for all bound variables $x_j$ of the system. 

Thus, we know how to solve any system in row echelon form (the algorithm is easier to 
run if the system is already in reduced row echelon form). 

But thanks to the magic of the 
[Theorem on row operations and solution sets]({% link notes/solving_linear_systems/effect_on_solutions.md%}#Theorem-on-Row-Operations-and-Solution-Sets)
and [Gaussian Elimination]({% link notes/solving_linear_systems/gaussian_elimination.md %}) we 
also know that given any system of linear equations $(A \mid b)$ we can apply row 
operations to it and produce a new system in row echelon form that possesses exactly the 
same set of solutions. 

Thus, any fact we know holds for solutions to row echelon systems _automatically holds_ 
for all linear systems. 

### Dichotomy of solutions

For solutions to reduced row echelon systems, there is a dichotomy that mirrors 
the case of 
[a single linear equation]({%link notes/solving_linear_systems/linear_equations.md %}#dichotomy-of-solutions). 

-----

**Theorem**: Let $[ A \mid b ]$ be a linear system in row echelon form. The 
system has a solution if and only if whenever there is a zero row, the 
corresponding entry of $\mathbf{b}$ is also $0$. 

Moreover, if there is a solution, then there is a unique solution if and only 
if there are no free variables. Otherwise, there are infinitely many solutions. 

-----

To understand the the proof of this theorem, we will poke at the algorithm above a bit. 
