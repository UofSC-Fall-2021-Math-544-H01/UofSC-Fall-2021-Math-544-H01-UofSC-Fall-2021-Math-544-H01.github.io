---
layout: page
title: Geometry of linear systems 
nav_order: 14
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
work_in_progress: true 
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
is the _intersection_ of the lines for each equation. 

