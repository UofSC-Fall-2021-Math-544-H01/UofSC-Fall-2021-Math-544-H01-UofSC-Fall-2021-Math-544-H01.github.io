---
layout: page
title: Geometry of linear systems 
nav_order: 14
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
work_in_progress: false 
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## Systems and intersections of null spaces

In 2d or 3d, plotting the solution set of a function can provide geometric insight 
that complements our skill with symbolic manipulation. 

Let's look at what graphing a single linear equation looks. 

### Two dimensions 

The setting here is probably quite familiar from a previous class. Each linear 
equation is two variables represents a line in the plane. 

For example suppose we have the linear equation 
$$
    x + y = 1
$$

Then the set 
$$
    \lbrace (x,y) \mid x + y = 1 \rbrace 
$$
is a line with slope $-1$ and $y$-intercept $(0,1)$. If we plot it, we get
<center>
<img src="/assets/images/svg/geo_ex_1.svg" title="A line with slope -1 and 
y intercept 1">
</center>

Now let's look at the system 
$$
    \begin{aligned}
        x + y & = 1 \\
        x - y & = 0
    \end{aligned}
$$
Then the solution set of the system 
$$
    \lbrace (x,y) \mid x + y = 1 \text{ and } x - y = 0 \rbrace 
$$
is the _intersection_ of the lines for each equation. In our example, the solution 
set is represented by the dot at $(1/2,1/2)$
<center>
<img src="/assets/images/svg/geo_ex_2.svg" title="Intersection of two lines">
</center>

Let's see the 
[dichotomy of solutions]({% link notes/solving_linear_systems/solving_echelon_systems.md %}#dichotomy-of-solutions)
at play geometrically in our 2d/two variable setting. 

Let's assume none of our linear equations have zero coefficients. 

- With a single linear, we have infinitely many solutions. Each point on the line is a solution to the equation. 

- With two linear equations in the system, there are two possibilities. First, the lines can intersect a single 
point like in the example above. Correspondingly there is a unique solution to the system. This is 
generic. If we draw two lines at random, then they will intersect. 

The other possibility is that the two lines are parallel. For example, 
<center>
<img src="/assets/images/svg/geo_ex_3.svg" title="Parallel lines don't intersect">
</center>
This is a system with no solution - unless the lines are equal. If the lines are equal, there are infinitely many 
solutions.

- With three or more linear equations in the system, then generically all three lines will not intersect in a point. 
<center>
<img src="/assets/images/svg/geo_ex_4.svg" title="Generically three lines in the plane don't intersect at a single point">
</center>
The corresponding system then has no solution. 

But for some special collections of three or more lines, it is possible for them all to intersect at a single point or even a 
single line. 

For example, if they are all lines through the origin, then the origin would be a common point to all the lines. 
The line passes through the origin if and only if the corresponding linear equation is homogenenous. This geometric 
picture reflects the fact that $\mathbf{x} = \mathbf{0}$ always solves the homogeneous system $A \mathbf{x} = \mathbf{0}$.

### General n

We can carry our intuition from two variables to $n$ variables even if we cannot visualize the resulting shapes. 

Given a linear equation 
$$
    a_1x_1 + \cdots + a_n x_n = b
$$
the solution set 
$$
    \lbrace \mathbf{x} \in \mathbf{R}^n \mid a_1x_1 + \cdots + a_nx_n = b \rbrace
$$
is the analog of a line for $n=2$ or a plane for $n=3$. We call it a _hyperplane_. 

Solving a system $(A \mid b)$ is equivalent to asking what $\mathbf{x}$'s lie in the intersections of all the 
hyperplanes simultaneously. 
$$
    \mathcal Z(A \mid b) = \bigcap_{i=1}^m \mathcal Z(\mathbf{R}^A_i \mid b_i).
$$

Each time we impose a new linear equation in our system we can:
- cut down the number of free variables by $1$ or 
- not change the set of solution. 

In the former case, we could end up with $-1$ free variables corresponds to no solution. 

In the second case, we know that any solution to the new linear equation was already a solution to the existing 
system. There is some redundancy in our system of equations. 