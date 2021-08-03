---
layout: page
title: Linear Systems
nav_order: 1
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
---

## Linear equations

A *linear equation in a set of variables $x_1,x_2,x_3,\ldots,x_m$* is a equation of the form
$$
    a_1 x_1 + a_2 x_2 + \cdots + a_m x_m = b 
$$
for constant numbers $a_1,\ldots,a_m, b$. 

So, for example, 
$$ 
 -x_1 + 2x_2 - 3x_3 + 4x_4 = 5
$$
would be a linear equation in 4 unknowns. 

Most equations you have seen are **not** linear. For example, 
$$
    xy = 1. 
$$
or 
$$
    e^{x_1} + x_2 + x_3 = -1.
$$

In general, linear equations are the simplest types of mathematical equations so we better be able 
to handle them quickly and efficiently. 

### Solving a single linear equation 

Say we wanted to solve the equation 
$$ 
    -x_1 + 2x_2 - 3x_3 + 4x_4 = 5
$$
How would we go about doing this? 

First, we need to be a bit more precise about what we mean to "solve the equation". What we want here 
is often called a *parametric" representation of the solution. We want to identify some free variables 
that can be used to determine all the solutions explicitly. 

As you might have done or seen  before, this can be accomplished by "solving out" a variable using 
the equation. We can rewrite the equation as 
$$
    x_1 = 2x_2 - 3x_3 + 4x_4 - 5
$$

Now, given any possible values of $(x_2,x_3,x_4)$, we can use the new form of the equation to find a 
value for $x_1$ so that we solve the equation. For example, if we take $(1,1,1)$, then plug in to get
$$
    x_1 = 2 \cdot 1 - 3 \cdot 1 + 4 \cdot 1 -5 = -2
$$
and $(-2,1,1,1)$ is a solution to the equation. 

Great! You might think we have mastered single linear equations. To find the solution to 
$$
    a_1 x_1 + \cdots + a_m x_m = b 
$$
in general, we pick some $a_i \neq 0$ and then we can solve for $x_i$ as 
$$
    x_i = b - \sum_{j \neq i} \frac{a_j}{a_i} x_j 
$$

We can try another example to test our understanding. How about solving
$$ 
    x_2 - x_4 = 2
$$

One possible point of confusion is: how many variables are we using? We only see 2 in the equation 
but the biggest index is a 4. So are we using 2 unknowns or 4 unknowns? We will often infer the number of 
unknowns in the linear equation (and system) from the context. The convention we will use will be 
this is an equation in 4 unknowns. But, do not be afraid to ask for clarification. 

Back to the example. Let us pick $x_4$ to solve out 
$$ 
    x_4 = x_2 - 2
$$
Then, our general (parametric) solution would look like $(x_1,x_2,x_3,x_2-2)$. 

We might be satisfied with our understanding but there is actually one case that breaks our algorithm. 

What happens if all $a_i = 0$ and $b \neq 0$, say $b = 1$? Then, we are looking at an immediate problem 
$$
    0 = 1
$$
is not satisfiable for any values of our unknowns. In this case, there are **no** solutions. 

This situation may seem contrived. Often in mathematics, a general understanding often hinges on properly 
understanding the edge cases of a problem. Linear algebra is no different. Encountering $$0 = 1$$ will 
be a natural possibility once we have developed enough tools. 

Before we turn to systems of linear equations, let's recap one important point: 

--------

### Observation:
For a linear equation, $a_1x_1 + \cdots a_mx_m = b$, we have three possibilities 
- there can be infinitely-many solutions if $m > 1$ and either not all $a_i$ are $0$ or $b = 0$, 
- there can be a unique solution if $m = 1$ and either not all $a_i$ are $0$ or $b = 0$ (e.g. $x = 1$), or
- there can be no solutions at all if all $a_i$ are $0$ and $b \neq 0$. 

--------

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

We can generalize our method for computing solutions to 