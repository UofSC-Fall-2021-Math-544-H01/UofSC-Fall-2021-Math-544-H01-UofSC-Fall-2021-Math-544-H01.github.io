---
layout: page
title: Vector spaces
nav_order: 2
has_children: true
parent: Notes
reading_estimate: true
---

## Clearing the cruff 

At this point, we have constructed a number of objects that feel similar:
- The space $\mathbb{R}^n$. 
- The null space $\mathcal Z(A)$ of a matrix. 
- The range $\mathcal R(A)$ of a matrix. 

[Geometrically]({% link notes/solving_linear_systems/geometry_of_linear_systems.md %}), 
they all correspond to hyperplanes in $\mathbb{R}^n$ and they all share similar properties. 

As an example, we have already seen any 
[range can be expressed as a null space]({% link notes/solving_linear_systems/equations_for_solvable_systems.md %} #ranges-as-null-spaces ) 
and that any 
[null space can be expressed a range]({% link notes/solving_linear_systems/equations_for_solvable_systems.md %} #null-spaces-as-ranges). 

Similarly, the set of $t$ free variables found in solving $A \mathbf{x} = \mathbf{0}$ feel very much like vectors in $\mathbb{R}^t$. 
We can plug in any values for those free variables and get a solution. There is no constraint on them. Much like $\mathbb{R}^t$ is 
the set of $t$ values in $\mathbb{R}$ with no constraints on them. 

In mathematics, when confronted with the many similar-seeming objects that are not all exactly the same in our current framework, it 
makes sense to search for an abstraction that can unify all the objects as instances of a single idea. 

That is what [vector spaces]({% link notes/vector_spaces/def_egs.md %}) are. Almost everything we have seen is an element of a vector space. 