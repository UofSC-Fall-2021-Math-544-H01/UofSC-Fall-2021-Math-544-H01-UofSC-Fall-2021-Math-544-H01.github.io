---
layout: page
title: Solving Echelon Systems
nav_order: 7
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
---

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

### Algorithm for solving systems in reduced row echelon form  

For a system in reduced row echelon form, computations simply even more. 

We can provide an algorithm different from the previous
[algorithm]({%link notes/solving_linear_systems/systems.md %}#algorithm-for-solving-a-system-of-linear-equation).
It is still in pseudo-code but is closer to something that might run. 

```python
# m x n matrix in row echelon form written here as a list of its row vectors
A = [R_1,...,R_m]
# length n vector of variables 
X = [x_1,...,x_n]
# length m vector 
b = [b_1,...,b_m] 

# if some row of A is zero but the corresponding entry of b is not, 
# we don't have a solution
for 1 <= j <= m: 
    if R_j == 0 and b_j != 0:
        return "No Solution"

# a list of the free variables
free_variables = []  

# for each column containing not containing 
# a pivot of a row, we have a free variable
for 1 <= j <= n:
    if C_j contains a pivot: 
        continue 
    else:
        append j to free variables

# for each free variable, we want to know which row contains 
# the corresponding pivot; notice this works since there is only 
# one nonzero entry in a column with a pivot when in reduced 
# row echelon form
def find_the_row (j):
    for 1 <= i <= m:
        if C_j[i] != 0:
            return i

# the non-free variables are the variables that are not free
non-free_variables = [j for 1 <= j <= n and j not in free_variables]

# now we rewrite the non-free variables in terms of the free ones
for j in non-free_variables: 
    i = find_the_row(j)
    # note we skip over the j-th entry in R_i here
    x_j = b_j - R_i[1]*x_1 - R_i[2]*x_2 - ... - R_i[j-1]*x_{j-1} - R_i[j+1]*x_{j+1} - ... - R_i[n]*x_n  

return [x_1,...,x_m]
```

The output of this is either the statement we have no solution or it rewrites 
the other variables in terms of free variables. 

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

Let's detail why this theorem is true with a proof. 

**Proof**: We will use induction on the number of equations in the system. Our 
base case will be one equation. This is essentially what we saw 
[previously]({%link notes/solving_linear_systems/linear_equations.md %}#solving-a-single-linear-equation).

We have an equation 
$$
    a_1 x_1 + \cdots + a_n x_n = b
$$
and either all the $a_i = 0$ or not. 

In the case all the $a_i = 0$, this becomes 
$$
    0 = b
$$
which only has a solution if and only if $b = 0$.

Assume some $a_i$ is non-zero. Let us use $i_0$ to denote the index 
of the pivot. Then, we can rewrite 
$$
    x_{i_0} = \frac{1}{a_{i_0}} \left( b - a_{i_0+1}x_{i_0+1} + \cdots a_{n}x_{n} \right)
$$

Now, assume the number of free variables is $0$. Remember the free variables 
are all the variables except for the ones with a pivot in its column. 
Thus, if we have none, then we must have a pivot and we can only have 
that variable. Thus, our solution set looks like
$$
    x_1 = b
$$
and we only have one. 

If we have free variables, then either we can have a pivot or not. 

If not 
and since we have assumed we have a solution, any values for the variables 
is a solution. We therefore have infinitely many. 

If we have a pivot, then we have to have at least two variables total and 
we can choose any value we wish for the free variables and plug in to  
$$
    x_{i_0} = \frac{1}{a_{i_0}} \left( b - a_{i_0+1}x_{i_0+1} + \cdots a_{n}x_{n} \right)
$$
to determine the appropriate value of $x_{i_0}$ to get a solution. 

We have checked that the theorem is true in our base case. Next we verify 
the induction step. Assume we know the theorem holds for any $m \times n$ 
system. We want to check it holds for any $(m+1) \times n$ system. 

Let $[A \mid b]$ denote a $(m+1) \times n$ system. Either the last row 
$\mathbf{R}\_{m+1}$ is $\mathbf{0}$ or not. If so, then either $b\_{m+1}$ is $0$ or 
not. 

For any system with $\mathbf{R}\_{m+1} = \mathbf{0}$ and $b\_{m+1} \neq 0$, 
the theorem holds since we cannot have a solution to $0 = b_{m+1}$. 

Otherwise, if $\mathbf{R}\_{m+1} = \mathbf{0}$ and $b\_{m+1} = 0$, then any
solution to $[A \mid b]$ is a solution to the $m \times n$ system 
$$
    a_{11} x_1 + \cdots + a_{1n} x_n = b_1 \\
    \vdots \\
    a_{m1} x_1 + \cdots + a_{mn} x_n = b_m
$$
and vice versa. The system 
$$
    a_{11} x_1 + \cdots + a_{1n} x_n = b_1 \\
    \vdots \\
    a_{m1} x_1 + \cdots + a_{mn} x_n = b_m
$$
is also in row echelon form. Therefore, we can apply the induction hypothesis 
and conclude theorem holds for $[A \mid b]$. 

In the final case, $\mathbf{R}\_{m+1} \neq \mathbf{0}$. Thus, we have a pivot. 
Let's write its index as $i\_0$. We can rewrite 
$$
    x_{i_0} = \frac{1}{a_{i_0}} \left( b_{m+1} - a_{(m+1)(i_0+1)}x_{i_0+1} + \cdots + a_{mn}x_{n} \right)
$$
Let $[ \widetilde{A} \mid \widetilde{b} ]$ be the $m \times n$ system obtained by 
- substituting in $\frac{1}{a_{i_0}} \left( b_{m+1} - a_{(m+1)(i_0+1)}x_{i_0+1} + \cdots + a_{mn}x_{n} \right)$ 
for $x_{i_0}$,
- moving all constants to the right of the equal sign, and 
- deleting the $i_0$ column. 

As we assumed that $[A \mid b]$ is in row echelon form, we know all the pivots of the 
rows $1 \leq j \leq m$ are strictly $< i_0$. Thus, this simplification does not affect any of 
the pivots and $[\widetilde{A} \mid \widetilde{b} ]$ remains in row echelon form. 

Any solution to $[\widetilde{A} \mid \widetilde{b} ]$ can be promoted to a solution to 
$[A \mid b]$ by setting 
$$
    x_{i_0} = \frac{1}{a_{i_0}} \left( b_{m+1} - a_{(m+1)(i_0+1)}x_{i_0+1} + \cdots + a_{mn}x_{n} \right)
$$
Conversely, given a solution to $[A \mid b]$, we know that 
$$
    x_{i_0} = \frac{1}{a_{i_0}} \left( b_{m+1} - a_{(m+1)(i_0+1)}x_{i_0+1} + \cdots + a_{mn}x_{n} \right)
$$
must hold. So we can eliminate $x_{i_0}$ and get a solution to $[\widetilde{A} \mid \widetilde{b}]$. 

From the induction hypothesis, we know the theorem holds for $[\widetilde{A} \mid \widetilde{b}]$.  

-----

**Theorem**: Let $[ A \mid b ]$ be a linear system in reduced row echelon form. The 
system has a solution if and only if whenever there is a zero row, the 
corresponding entry of $\mathbf{b}$ is also $0$. 

Moreover, if there is a solution, then there is a unique solution if and only 
if there are no free variables. Otherwise, there are infinitely many solutions. 

-----

Let's detail why this theorem is true with a proof. 

**Proof**: We need to make some observations on the structure of reduced 
row echelon systems. 

Remember that the free variables, by definition, are indexed by the columns 
containing no pivots. 

The non-free variables will only appear in a single equation. Why? Since 
we are in reduced row echelon form, if there is a pivot in a column, it 
is the only non-zero entry. 

Let $x_t$ be a non-free variable. Let $(i_t,t)$ be the entry in $A$ for 
the corresponding pivot. We can set 
$$
    x_t = b_{i_t} - \sum_{s \neq t } a_{i_t s}x_s
$$
and eliminate the row $\mathbf{R}_{i_t}$ from the system. 

The new system has one fewer row and one fewer column. Proceeding a finite number 
of steps, we end up with a system with no pivots and where only the free 
variables are left as variables. 

Solutions of this 
new system are in bijection with solutions of the original system $[A \mid b]$. 
Indeed, given a solution to $[A \mid b]$, I know I must have 
$$
    x_t = b_{i_t} - \sum_{s \neq t } a_{i_t s}x_s
$$
for each non-free $t$. Thus, we can plug in and eliminate. Ultimately resulting in 
a solution to the final system with no pivots. 

The only way we solve a system with a zero coefficient matrix is if all $b_i = 0$. 
If all the $b_i$ are $0$, then any value for the free variables solves it. 
We can take any values for the free variables and, for each non-free $t$, set
$$
    x_t = b_{i_t} - \sum_{s \neq t } a_{i_t s}x_s.
$$
This gives us a solution to the original system.

Now let's turn to the theorem. If some $\mathbf{R}\_i = \mathbf{0}$ but 
$b_i \neq 0$, then we cannot have a solution to $0 = b_i$. 

The other direction uses our observations. If all the 

