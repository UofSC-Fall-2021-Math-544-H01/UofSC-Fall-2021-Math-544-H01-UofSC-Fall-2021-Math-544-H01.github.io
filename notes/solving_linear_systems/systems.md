---
layout: page
title: Systems
nav_order: 2
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
---

## Systems of linear equations 

With our knowledge of linear equations, the notion of a system is pretty quick to state. A *system of 
linear equations in the variables $x_1,\ldots,x_m$* is a (finite) set of linear equations in $x_i$'s. Let us 
use $n$ to denote the number of equations we have. Then, we are saying that, for any $1 \leq i \leq n$ and 
$1 \leq j \leq m$, there are $a_{ij}$ and $b_i$ and equations 

$$
    a_{11} x_1 + a_{12}x_2 + \cdots a_{1m} x_m = b_1 \\
    a_{21} x_1 + a_{22}x_2 + \cdots a_{2m} x_m = b_2 \\
    \vdots \\
    a_{n1} x_1 + a_{n2}x_2 + \cdots a_{nm} x_m = b_n \\
$$

We need two indices now: one to account for the number of equations and another for the number of unknowns. 

We were already introduced to an example
$$ 
 0 = \frac{1}{4} x - \frac{1}{3} y \\
 {} \\
 0 = - \frac{1}{2} x + \frac{1}{3} y
$$

In this case $n = m = 2$. For a system where $n = m$, we will call it *square*. 

We can generalize our method for computing solutions to the linear equations to handle systems in a 
straightforward manner. Let us see it in effect for the example above. 

First, we pick a nonzero coefficient, called a *pivot* in general. In this case lets take the $1/4$ on the $x$. 

Now we try to solve out 
$$
    0 = \frac{1}{4} x - \frac{1}{3} y
$$
for $x$. We get 
$$
    x = \frac{4}{3} y.
$$

Now we can substitute $x = 4y/3$ to eliminate $x$ from the next equation:
$$
    0 = -\frac{1}{2} \left( \frac{4}{3} y \right) + \frac{1}{3} y = - \frac{1}{3} y
$$
which we can solve for $y$ to get $y = 0$. 

Now we can substitute $y = 0$ back into $x = 4y/3$ and get $x = 0$. 

We can now answer the question in the original motivating example: the only steady state solution is where there 
are no aliens of either type. Sensible but perhaps not particularly interesting. 

From this, we can see that this algorithm for solving a system of linear equations just repeatedly applies the 
algorithm for solving a single linear equation until there are no more linear equations or we run into No Solution.

-----

### Algorithm for solving a system of linear equations:
We can write this algorithm for a general system that is simple to state but can be expensive to carry out. 

**Step 1** 
Identify a variable $x_i$ and an equation $l_j$ with $a_{ij} \neq 0$. 

**Step 2** 
Use $l_j$ to solve for $x_i$ in terms of the other variables. 

**Step 3** 
Substitute in your expression from step 2 for all occurrences of $x_i$. Simplify. If we end up with an 
equation of the form $0 = b$ with $b \neq 0$, stop and output "No Solution". 

Delete $l_j$ from your system. Return to step 1 with the new system. 

<!-- in pseudo-code. We write `algorithm_single_equation(l)` for the 
application of the [algorithm for a single linear equation]({% link notes/solving_linear_systems/linear_equations.md %}/#algorithm-for-solving-a-linear-equation) to a linear equation l.  -->

<!-- ```
variables = [x_1,...,x_m]
linear equations = [l_1,...,l_n]

while number of equations != 0:
    pick l in linear equations
    if algorithm_single_equation(l) == No Solution:
        return No Solution
    else: 
        if algorithm_single_equation(l)[i] != x_i:
            set x_i = algorithm_single_equation(l)[i]
        remove l from linear equations
        for each l' in linear equations: 
            substitute algorithm_single_equation(l) into l'

return [x_1,...,x_m]
``` -->

In words, we pick a nonzero linear equation. Either we eliminate a variable or we have a contradiction (where $0$ equals $\neq 0$). 
If we have a contradiction, we stop because we have no solution. Otherwise, we eliminate the chosen variable by rewriting it using 
the chosen equation. Then, we substitute back into all the remaining equations and repeat until we have no more equations left. 

-----

This algorithm is a bit more opaque than the one for a single equation. Ask yourself: is it clear that we always output either 
- No Solution
- A single solution
- Infinitely many solutions? 

What can it tell us about the structure of the solution set in general? 

It also is not the most efficient one. 

To gain better understanding and more power, we need some tools - 
[vectors]({% link notes/solving_linear_systems/vectors.md %}) and [matrices]({% link notes/solving_linear_systems/matrices.md %}). 

<!-- {{ page.path }} this gives the page path -->