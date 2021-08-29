---
layout: page
title: Gaussian Elimination
nav_order: 9
has_children: false
has_toc: false
parent: Solving Linear Systems
grand_parent: Notes
work_in_progress: false 
---

{% if page.work_in_progress %}
    WORK IN PROGRESS
{% endif %}

## An algorithm for row echelon form

Now, we turn to explicitly describing the steps from a general matrix $A$ 
to one in (reduced) row echelon form using our three classes of  
[row operations]({% link notes/solving_linear_systems/row_operations.md %}). 

Thanks to the 
[Theorem on Row Operations and Solution Sets]({% link notes/solving_linear_systems/effect_on_solutions.md %}#Theorem-on-Row-Operations-and-Solution-Sets) 
we know that the set of solutions to the system remains unchanged when moving 
$A$ to the matrix in (reduced) row echelon form. From this we can conclude 
**if we want to know the solution to a general system, it suffices to convert it 
to (reduced) row echelon form and the solve that system**.  
Solving (reduced) row echelon systems is easier than general systems. 

Let's describe one by one the steps.

### Step 0

Write the system as an augmented matrix $(A \mid b)$.

### Step 1 (Permutations)

Exchange the rows of $(A \mid b)$ until all $0$ rows are at the bottom.

Then permute the rows so that the column index of the pivots is a non-increasing 
function of the row index of the pivot. In equations, we want 
$$
    \operatorname{Pivot}(\mathbf{R}_i) \leq \operatorname{Pivot}(\mathbf{R}_j)
$$
if $i \leq j$. 

### Step 2 (Linear combinations)

Reading left to right, find the first column $\mathbb{C}_j$ such that 
- there is a pivot $a_{ij}$ from row $\mathbf{R}_i$ in $\mathbb{C}_j$ and 
- there is some some $a_{sj} \neq 0 $ with $s > i$, ie below $a_{ij}$.

If there are none, you are done. 

Otherwise, let $\mathbf{R}_p$ be the row with the smallest $p$ of all the rows 
that have their pivots in $\mathbf{C}_j$. 

For all $t \geq s$ replace the row $\mathbf{R}\_t$ of $(A \mid b)$ with 
$$
    \mathbf{R}_t - \frac{a_{tj}}{a_{pj}} \mathbf{R}_p
$$
Note that this does nothing if $a_{tj} = 0$. If $a_{tj} \neq 0$, then it will 
be zeroed out. 

Return to [Step 1](#Step-1). 

-----

Let's see this in effect in an example 
$$
    5 x_1 - 3 x_2 + x_3 + x_4 = 3 \\
    x_1 + x_2 - x_3 + x_4 = 0 \\
    -2x_1 - x_2 + 2x_3 + x_4 = 1
$$
to illustrate the algorithm. 

<details>
	<summary>Click to see the calculations</summary>

We do Step 0 first 
$$
    (A \mid b) = 
    \begin{pmatrix} 
        5 & -3 & 1 & 1 &\bigg| & 3 \\
        1 & 1 & -1 & 1 &\bigg| & 0 \\
        -2 & -1 & 2 & 1 &\bigg| & 1 \\
    \end{pmatrix} 
$$

For Step 1, we have no zero rows and the pivots of all the rows are in the 
first column so we don't need to exchange rows. 

Our first column with a pivot and nonzero entries below the pivot is 
$a_{1,1} = 5$ and both $a_{1,2}$ and $a_{1,3}$ are nonzero. So we subtract 
$$
    \begin{pmatrix} 
        1 & 1 & -1 & 1 &\bigg| & 0 
    \end{pmatrix} - \frac{1}{5} 
    \begin{pmatrix} 
        5 & -3 & 1 & 1 &\bigg| & 3 \\ 
    \end{pmatrix} = 
    \begin{pmatrix} 
        0 & 8/5 & -6/5 & 4/5 &\bigg| & -3/5 
    \end{pmatrix}
$$
and 
$$
    \begin{pmatrix} 
        -2 & -1 & 2 & 1 &\bigg| & 1
    \end{pmatrix} + \frac{2}{5} 
    \begin{pmatrix} 
        5 & -3 & 1 & 1 &\bigg| & 3 \\ 
    \end{pmatrix} = 
    \begin{pmatrix} 
        0 & -11/5 & 12/5 & 7/5 &\bigg| & 11/5 
    \end{pmatrix}
$$

Our new augmented matrix is 
$$
    (A \mid b) = 
    \begin{pmatrix} 
        5 & -3 & 1 & 1 &\bigg| & 3 \\
        0 & 8/5 & -6/5 & 4/5 &\bigg| & -3/5 \\
        0 & -11/5 & 12/5 & 7/5 &\bigg| & 11/5 \\
    \end{pmatrix} 
$$

We return to Step 1 with our new $(A \mid b)$. Again 
there are no zero rows and the column indices of the pivots never 
jump up as we read down the rows. So we move to Step 2. 

Now the first column with a pivot and a nonzero entry below that pivot 
is the second one. The pivot is $a_{2,2} = 8/5$ and the only nonzero 
entry below it is $a_{2,3} = -11/5$. We replace the third row with 
$$
    \begin{pmatrix} 
        0 & -11/5 & 12/5 & 7/5 &\bigg| & 11/5
    \end{pmatrix} + \frac{11}{8} 
    \begin{pmatrix} 
        0 & 8/5 & -6/5 & 4/5 &\bigg| & -3/5 \\ 
    \end{pmatrix} = 
    \begin{pmatrix} 
        0 & 0 & 33/40 & 5/2 &\bigg| & 11/5
    \end{pmatrix}
$$

Our new augmented matrix is 
$$
    (A \mid b) = 
    \begin{pmatrix}
        5 & -3 & 1 & 1 &\bigg| & 3 \\
        0 & 8/5 & -6/5 & 4/5 &\bigg| & -3/5 \\
        0 & 0 & 33/40 & 5/2 &\bigg| & 11/5
    \end{pmatrix} 
$$
The pivots are now strictly increasing in the column index as we 
read down the rows and there are still no nonzero columns so nothing needs to 
be permuted. 

For Step 2, we see that all pivots have $0$ below them so we are done.

</details>

Next, we want a proof that this algorithm actually outputs an matrix is row 
echelon form.

**Theorem**. The [algorithm from row echelon form](#An-algorithm-for-row-echelon-form) 
outputs a matrix in row echelon form. 

**Proof**. Since we pass through Step 1 before we exit, we know two things:
- all zero rows are at the bottom and 
- the column indices of the pivots never decrease as we increase the row index. 

To get to row echelon form, we need know that the column index strictly increases 
as we increase the row index. 

When we exit the algorithm, we know that if a column has a pivot, then all entries 
below the pivot must be $0$. Thus, we cannot have another pivot in that column. Since 
we know that column index of the pivot cannot decrease and cannot remain the same, 
it must increase as we increase the row index. 

## An algorithm for reduced row echelon form

We can tweak our [algorithm from row echelon form](#An-algorithm-for-row-echelon-form) 
slightly to get an algorithm that produces a matrix in reduced row echelon form. 

## Step 0 

Same as before.

## Step 1

Also the same.

## Step 1.5 

Scale all the rows so that all pivots have value $1$

## Step 2

Reading left to right, find the first column $\mathbb{C}_j$ such that 
- there is a pivot $a_{pj}$ from row $\mathbf{R}_p$ in $\mathbb{C}_j$ and 
- there is some some $a_{sj} \neq 0 $ with $s \neq p$, ie anywhere in the column 
not just below.

If there are none, you are done. 

Otherwise, let $\mathbf{R}_p$ be the row with the smallest $p$ of all the rows 
that have their pivots in $\mathbf{C}_j$. 

For all $t \neq s$ replace the row $\mathbf{R}\_t$ of $(A \mid b)$ with 
$$
    \mathbf{R}_t - \frac{a_{tj}}{a_{pj}} \mathbf{R}_p
$$


