---
layout: page
title: Linear Transformations
nav_order: 3
has_children: true
parent: Notes
reading_estimate: true
---

## Linear Transformations

We [already]({% link notes/vector_spaces/intro.md %}) discusses how to abstract 
the our concrete examples of vectors as lists of numbers into the general 
notion of a vector space. 

We saw that almost every object we have touched could be put in its own 
vector space and then studied with the tools of linear algebra. 

Next, we abstract matrices. The key properties of matrices are:
- Multiplication by a matrix commutes with scaling
$$
    A(cx) = cA(x)
$$
- Multiplication by a matrix commutes with addition of vectors
$$
    A(x + y) = A(x) + A(y)
$$

We will use there two properties as the specification for the notion of 
a _linear transformation of vectors spaces_. We will see how to 
recover matrices from linear transformations between finite dimensional 
vector spaces by expressing them in bases. 