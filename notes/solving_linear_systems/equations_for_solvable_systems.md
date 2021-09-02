---
layout: page
title: Equations for solvability
nav_order: 12
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
work_in_progress: true
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
It, itself, is the solution set of a different linear system!

### Equations on the inhomogeneous term

