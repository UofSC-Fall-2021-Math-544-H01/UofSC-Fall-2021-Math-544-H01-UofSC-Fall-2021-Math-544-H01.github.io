---
layout: page
title: Their Effect on Solutions
nav_order: 8
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
---

## Changing the system but not the solutions 

Our operations would be of little use if we did not understand how the solution sets of the systems 
changed under each transformation. 

Here, we are in the best of all possible worlds. The solutions _do not change_ under 
- scaling a row by a non-zero scalar
- exchanging two rows or 
- subtracting a scalar multiple of one row off a different one. 

Let's take each one at a time. 

### Exchanging rows

This is the easiest one to see. 

Since the linear equations involved do not change _at all_ when we swap rows,
the solutions don't either. 

We are just switching the order in which we are listing them. 

### Scaling a row 

Scaling a row by a _non-zero_ scalar doesn't change the set of solution. Let's 
start with a system $(A \mid b)$ and some scaling matrix $S(i,c)$. 

We want to compare the sets of solutions to $(A \mid b)$ and 
$S(i,c)(A \mid b)$. 

Assume we have a solution $(x\_1^\circ, \ldots, x\_n^\circ)$ to the system $(A \mid b)$.
(Here I write $x^\circ$  as decoration to indicate that we have a fixed vector of numbers 
that solves the system).  

We want to conclude it also a solution to the new system where we scale the 
i-th row by a number $c$, $S(i,c)(A \mid b)$. 

**What do we have to do to check we also solve the new system $S(i,c)(A \mid b)$?** 

Well, the only equation that changes from the old system $(A \mid b)$ is just the i-th one. 
We have the equality  
$$
	a_{i1}x_1^\circ + a_{i2}x_2^\circ + \cdots + a_{in}x_n^\circ = b_i 
$$
If we multiply both sides by $c$, then we preserve the equality so 
$$
	ca_{i1}x_1^\circ + ca_{i2}x_2^\circ + \cdots + ca_{in}x_n^\circ = cb_i 
$$
This is exactly the i-th equation for our new system. Thus, 
$$
	\mathbf{x}^\circ \in \mathcal Z(S(i,c) (A \mid b)).
$$

Great, we have checked that every solution to $(A \mid b)$ is also a solution to $S(i,c)(A \mid b)$.
In mathematical notation, we know that for any $c$
$$
	\mathcal Z(A \mid b) \subseteq \mathcal Z(S(i,c) (A \mid b)). 
$$

In the case that $c \neq 0$, we have 
$$
	\mathcal Z(S(i,c) (A \mid b)) \subseteq \mathcal Z(S(i,1/c) (S(i,c) A \mid b))) 
$$
As you will check on your homework, 
$$
	S(i,c_1) S(i,c_2) = S(i,c_1c_2) 
$$
So 
$$
	S(i,1/c) S(i,c) A = S(i,1) A = I A = A. 
$$
Thus, 
$$
	\mathcal Z(A \mid b) \subseteq \mathcal Z(S(i,c) A \mid b) \subseteq Z(A \mid b) 
$$
As we saw in the Math 300, for two sets $X$ and $Y$, if $X \subseteq Y$ and $Y \subseteq X$, then 
$X = Y$. 

So the solutions to $(A \mid b)$ are exactly the solutions to $S(i,c) (A \mid b)$. 

### Adding multiples of rows to other rows 

For the final operation, it is perhaps less obvious that we preserve the solution set 
of the linear system. 

We procede in the same way as with 
[scaling a row]({% link notes/solving_linear_systems/effect_on_solutions.md%}/#scaling-a-row).

Assume we have a solution $(x\_1^\circ, \ldots, x\_n^\circ)$ to the system $(A \mid b)$.

Then we know that for any $i,j$: 
$$
	a_{i1}x_1^\circ + \cdots + a_{in} x_n^\circ = b_i \\
	a_{j1}x_1^\circ + \cdots + a_{jn} x_n^\circ = b_j \\
$$
If we scale j-th row by $c$, we still have equality 
$$
	ca_{j1}x_1^\circ + \cdots + ca_{jn} x_n^\circ = cb_j
$$
as with scaling. Finally, when we add 
$$
	(a_{j1}x_1^\circ + \cdots + a_{jn} x_n^\circ) + (ca_{j1}x_1^\circ + \cdots + ca_{jn} x_n^\circ) = b_i + cb_j
$$
we know that we are subtracting the same numbers from each side of the equality. This 
preserves the equality. 
Writing 
$$
	(a_{j1}+ca_{i1})x_1^\circ + \dots + (a_{jn}+ca_{in})x_n^\circ = b_i + cb_j
$$
we recognize that the we have just operated on the rows of $(A \mid b)$ by sending 
$$
	\mathbf{R}_j \mapsto \mathbf{R}_j - c \mathbf{R}_i. 
$$

Thus, $(x\_1^\circ, \ldots, x\_n^\circ)$ is also a solution to the system $L(i,j,c)(A \mid b)$, ie 
$$
	\mathcal Z(A \mid b) \subseteq \mathcal Z(L(i,j,c)(A \mid b)). 
$$

Like with scaling a row, we want to _undo_ multiplication by $L(i,j,c)$. In 
[Worksheet 2]({% link worksheets/02.md %}), 
you will see that if $i \neq j$, then  
$$
	L(i,j,c) L(i,j,-c) = I 
$$

One we know this, we can immediately apply what we already know to see 
$$
	\mathcal Z(L(i,j,c)(A \mid b)) \subseteq \mathcal Z(L(i,j,-c)L(i,j,c)(A \mid b)) = \mathcal Z(A \mid b).
$$
Thus, if we subtract off any multiple of one row from a _different_ row then, we know 
$$
	\mathcal Z(A \mid b) = \mathcal Z(L(i,j,c)(A \mid b))
$$

We have established the following theorem.

-----

### Theorem on Row Operations and Solution Sets

Let $(A \mid b)$ be a linear system. Let $(A^\prime \mid b^\prime)$ be the linear system obtained 
from $(A \mid b)$ by a sequence of the following operations: 
- scaling a row by a non-zero scalar
- exchanging two rows or 
- subtracting a scalar multiple of one row off a different one. 

Then, the sets of solutions of $(A \mid b)$ and $(A^\prime \mid b^\prime)$ coincide. 

We will apply this theorem after we have established 
[Gaussian elimination]({% link notes/solving_linear_systems/gaussian_elimination.md %}) which 
fulfills the promise converting any system into (reduced) row echelon form. 

