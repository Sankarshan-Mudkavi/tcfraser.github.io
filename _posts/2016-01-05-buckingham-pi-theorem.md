---
layout: post
title: Buckingham Pi Theorem
---

In order to determine the physical equation for a given system there are numerous things one can do. One method using the the [Buckingham-$\pi$ Theorem](https://en.wikipedia.org/wiki/Buckingham_%CF%80_theorem) 
allows one to determine all of the possible *simple* physical equations of the system up to a constant factor that rarely matters. It is extremely beneficial to a physicists arsenal.

<!--more-->

## Physical System

A physical system can be reduced to $n$ dimensional variables (physical variables) such as energy, mass, velocity, density, etc. and $k$ physical dimensions such as time, mass, length, charge, etc. along with an assortment of mathematical equations that relate the $n$ variables together.

## Determining the Mathematical Equations

Determining what equations govern a physical system is tricky. To a crude approximation, that's what physics *is*. I see three distinct ways of determining or at least modelling the physical system.

#### 1. Experiments
Do many experiments on a system and vary the parameters of the system to determine how one physical variable depends on another. The aggregate of these experiments reveals the form of the desired mathematical equations.

*Requirements:* money, time, plots and error bars

#### 2. Logic & Fancy Maths
Use logic and intuition to choose a set of axioms to deduce the nature of the theory from first principles. Some of these axioms include
    - space is isotropic
    - time is homogeneous
    - space is homogeneous
    - CPT symmetry

*Requirements:* intelligence, mathematics, pages of theorems

#### 3. Buckingham-Pi Theorem
Using simple foundations of linear-algebra, the Buckingham-Pi theorem determines all of the possible unique relations between the $n$ variables.

*Requirements:* guessing variables, matrix kernels

None of these methods are at all equivalent. Each one has it's domain of use. Nonetheless, Buckingham-Pi is doable in your head or on the back of an envelope.

## Buckingham-Pi Formalism
Let $S = \bc{q_i}$ be the set of all physical variables. Each $q_i$ has physical dimensions associated with it. Typically these are taken to be the ones found in [this list](https://en.wikipedia.org/wiki/List_of_physical_quantities). Lets call this infinite set of dimensional combinations $D$. The set $D$ forms an [abelian group](https://en.wikipedia.org/wiki/Abelian_group) and satisfies the usually properties of closure, associativity, existence of indentity/inverse, and commutivity. Since the irreducible elements of $D$, namely $\bc{u_j} = $ $ \bc{T, L, M, C, \ldots}$ are finite, this group is isomorphic to a vector space over the rational numbers $D \sim \mathbb{Q}$. This is realized when the element $d \in D$ such that $d = \prod_j u_j^{a_j}$ can be mapped to $\vec{a} = [a_1, \ldots, a_n]$. Note: The reason for the rationality of each $a_j$ will become clear soon enough.

Now each potential physical equation that models the system must be dimensionally homogeneous. This means that each equation is equivalent to a function $f$ where $\bs{f} = 1$ where the square brackets indicate the dimensional nature of $f$. The Buckingham-Pi theorem applies to all functions $f$ that are dimensionless combinations of elements of $S$. Since the dimensions of elements of $S$ map to elements of $D$ (not one-to-one) this problem becomes finding linear combinations of $\vec{a}_i$ such that the result is the zero vector $\vec{0}$. 

$$ c_1\vec{a}_1 + \ldots + c_n\vec{a}_n = \vec{0}$$

Where $f$ is admitted by $k = \prod_{j=1}^n q_j^{c_j}$ where $k$ is an arbitrary an undetermined constant. This problem is quivalent to exploring the nullspace or kernel of a matrix $A$ where

$$ A_{ij} = \text{$i$-th component of $\vec{a}_j$} $$

Note that $A$ has $m$ rows where $m$ is the number of elements of $\bc{u_j}$ (the number of irreducible dimensions in the system) and has $n$ columns where $n$ is the number of physical variables that belong to the system.

By the [Rank-Nullity Theorem](https://en.wikipedia.org/wiki/Rank%E2%80%93nullity_theorem) the dimension of the space of the solutions $f$ is the dimension of the nullspace of $A$. 

## Examples

The format of each of these examples follows a few simple steps:
    
1. Guess which variables might influence the system.
2. Indentify the coefficients for the dimensions of variables in 1.
3. Construct $A$.
4. Find a basis for the the kernel of $A$.
5. Explore the resultant physics.

#### Period of Simple Pendulum

A pendulum has a number of physical variables that could be related: length of the pendulum $\ell$, the mass of the weight $m$, the strength of gravity $g$ and period of oscillation $t$.

Note that the dimensions of these variables is as follows.

\\begin{align} 
\bs{\ell} &= L &= L^1M^0T^0 \mapsto \br{1, 0, 0} \\\
\bs{m} &= M &= L^0M^1T^0 \mapsto \br{0, 1, 0} \\\
\bs{g} &= \f{L}{T^2} &= L^1M^0T^{-2} \mapsto \br{1, 0, -2} \\\
\bs{t} &= T &= L^0M^0T^1 \mapsto \br{0, 0, 1} \\\
\\end{align}

This produces the matrix:

$$ A = \nmtrx{1 & 0 & 1 & 0 \\\\ 0 & 1 & 0 & 0 \\\\ 0 & 0 & -2 & 1} \mapsto_{\text{RREF}} \nmtrx{1 & 0 & 0 & \f{1}{2} \\\\ 0 & 1 & 0 & 0 \\\\ 0 & 0 & 1 & -\f{1}{2}} $$

Which has basis for a nullspace given by:

$$ \vec{a} = \nmtrx{1\\\\ 0\\\\ -1\\\\ -2} $$

Therefore, the Buckingham-Pi theorem gives us a form for the only dimensionally homogeneous function (up to constant on $\vec{a}$):

$$ k = \ell^1 m^0 g^{-1} t^{-2} $$

Simplfing and rearranging for $t$ yields:

$$ t \propto \sqrt{\f{\ell}{g}} $$

Note that the period of the pendulum does not depend on the mass on the end of the pendulum. This is suprising as the pendulum would not function if it were massless. Furthermore, this result is justified from the perspective of the Rank-Nullity theorem.

In reality, the actual equation derived via a small angle approximation is given by:

$$ t = 2\pi\sqrt{\f{\ell}{g}} $$


#### Force of Drag

The force of drag acting on an object travelling through a medium has associated variables: mass of the object $m$, density of the fluid/medium $\rho$, the speed of the object $v$, the characteristic area of the object as seen by the fluid $A$ and the force of drag itself $F$.

Note that the dimensions of these variables is as follows.

\\begin{align} 
\bs{\rho} &= \f{M}{L^3} &= L^{-3}M^1T^0 \mapsto \br{-3, 1, 0} \\\
\bs{m} &= M &= L^0M^1T^0 \mapsto \br{0, 1, 0} \\\
\bs{v} &= \f{L}{T} &= L^1M^0T^{-1} \mapsto \br{1, 0, -1} \\\
\bs{A} &= L^2 &= L^2M^0T^0 \mapsto \br{2, 0, 0} \\\
\bs{F} &= \f{ML}{T^2} &= L^1M^1T^{-2} \mapsto \br{1, 1, -2} \\\
\\end{align}

This produces the matrix:

$$ A = \nmtrx{-3 & 0 & 1 & 2 & 1 \\\\ 1 & 1 & 0 & 0 & 1 \\\\ 0 & 0 & -1 & 0 & -2} \mapsto_{\text{RREF}} \nmtrx{1 & 0 & 0 & -\f23 & \f13 \\\\ 0 & 1 & 0 & \f23 & \f23 \\\\ 0 & 0 & 1 & 0 & 2} $$

Which has basis for a nullspace given by:

$$ \vec{a}_1 = \nmtrx{\f13\\\\ \f23\\\\ 2\\\\ 0 \\\\-1}, \vec{a}_2 = \nmtrx{\f23\\\\ -\f23\\\\ 0\\\\ 1 \\\\0} $$

In order to get a meaningful equation for the force of drag, one with note that the product of $f_1$ and $f_2$ or the addition of $\vec{a}_1 + \vec{a}_2$ will get the desired equation.

$$ \vec{a}_1 + \vec{a}_2 = \nmtrx{1\\\\ 0\\\\ 2\\\\ 1 \\\\-1} $$

$$ k = \rho^1 m^0 v^2 A^1 F^{-1} $$

Simplfing and rearranging for $F$ yields:

$$ F \propto \rho v^2 A $$

Note that the actual formula for drag is given by:

$$ F = k \rho v^2 A $$

where $k$ is determined by the geometrical properties of the moving object.