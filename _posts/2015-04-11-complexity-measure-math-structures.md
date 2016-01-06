---
layout: post
title: Complexity Measure of Mathematical Structures
---

Max Tegmark wrote a excellent paper in 2007 titled [The Mathematical Universe](http://arxiv.org/pdf/0704.0646.pdf). In it was an Appendix that introduced a definition for Mathematical Structures and provided simple examples of representations for finite structures using this definition. Under this framework he then provided a particular way of encoding the complexity of each finite mathematical structure that exists as a real number. I would like to explore the idea of infinite mathematical structures while summarizing some of Tegmark's ideas.
<!--more-->
\\(
\newcommand{\relun}[1]{
\boxed{
\begin{matrix}
#1
\end{matrix}
}
} 
\newcommand{\relvec}[2]{
\boxed{
\begin{matrix}
#1 \\\
#2 
\end{matrix}
}
}
\newcommand{\relthr}[3]{
\boxed{
\begin{matrix}
#1 \\\
#2 \\\
#3
\end{matrix}
}
}
\newcommand{\relthrthr}[9]{
\boxed{
\begin{matrix}
#1 & #2 & #3 \\\
#4 & #5 & #6 \\\
#7 & #8 & #9
\end{matrix}
}
}
\newcommand{\relmtrx}[4]{
\boxed{
\begin{matrix}
#1 & #2 \\\
#3 & #4
\end{matrix}
}
}
\\)

## Mathematical Structures

Thinking very abstractly, a mathematical structure can be defined as a set $S$ of entities and relations $R_1, R_2, \ldots$ between those entities. The set of entities contained in the structure is the union of a finite number of subsets $S = S_1 \cup S_2 \cup ... \cup S_n$, while the relations between these sets are functions that act on these subsets. Specifically they are mappings from some collection of sets to a single set as $$S_{i_1} \times S_{i_2} \times \ldots \times S_{i_k} \mapsto S_j$$.

A typical mathematical structure has a countably infinite number of relations that can be reduced to a finite set of *generating relations* and the rule of composition that can generate every other relation recursively. Moreover, there is evidently infinitely many equivalent ways to define a mathematical structure, with the simpliest one often being the shortest one.

### Examples

#### Boolean Algebra

[Boolean Algebra](http://en.wikipedia.org/wiki/Boolean_algebra) is a mathematical structure involving exactly two entities: `true` and `false`, and a set of relations. It is important to note that the names given to the two entities of Boolean Algebra are irrelevant to the structure itself. The enitites $cat$ and $dog$ are entirely equivalent, despite being less descriptive. For abstraction purposes, let us denote all entities using integers. The order associated with integers has no significance in this case. Thus, $0$ and $1$ represent `false` and `true` respectively.

All of Boolean Algebra is respresented as follows,

$$ S = \relvec01 \quad R_1 = \relun0 \quad R_2 = \relun1 $$

$$ R_3 = \relvec10 \quad R_4 = \relmtrx0001 \quad R_5 = \relmtrx0111 \quad R_6 = \relmtrx1101 \quad R_7 = \relmtrx0110 \quad R_8 = \relmtrx1110 $$

The relations here are represented as multiplication tables of sorts. For example, $R_4$ represents the `AND` relation and takes 2 inputs and generates $1$ or `true` only if both of the inputs are $1$. $R_1$ and $R_2$ represent the `false` and `true` relations directly taking in no arguments. The relations represent in order `false`, `true`, `NOT`, `AND`, `OR`, `IMPLIES`,`XOR`, and `NAND`. Those who have studied Boolean algebra know that many of these relations are actually expressible in terms of each other. This means that our representation above is too verbose and is not the simpliest way of representing all of Boolean Algebra.

If fact every relation conceivable in Boolean Algebra can generated from $R_8$ alone. Re-labeling $R_8$ for just $R$ for it's heighted importance, it can be seen that all relations are reducible to combinations of just R. Let $X$ and $Y$ be elements of $S$:

\\begin{align}
R_1 &= R(R(X,R(X,X)),R(X,R(X,X))) \\\
R_2 &= R(X,R(X,X)) \\\
R_3(X) &= R(X,X) \\\
R_4(X,Y) &= R(R(X,Y),R(X,Y)) \\\
R_5(X,Y) &= R(R(X,X),R(Y,Y)) \\\
R_6(X,Y) &= R(X,R(Y,Y)) \\\
R_7(X,Y) &= R(R(X,R(X,Y)),R(Y,R(X,Y))) \\\
R_8(X,Y) &= R(X,Y)
\\end{align}

Effectly, boolean algebra is reduced to one set $S$ and one relation $R$.

#### Multiplicative Group $C_3$

The multiplicative group of integers modulo 3 is a mathematical structure that can be quickly encapsulated by this notation.

$$ S = \relthr012 \quad R_1 = \relun0 \quad R_2 = \relthr021 \quad R_3 = \relthrthr012120201$$

In this cause the only enitites are $0,1,2$ and the relations are typically called `IDENTITY`, `INVERSE` and `PRODUCT`.

Again, each relation in this simple group can be reduced down to one generating relation: 

$$ R = \relthrthr021102210 $$

Letting $a$ and $b$ be elements of $S$, the relations $C_3$ can be reduced as follows:

\\begin{align}
e = R_1 &= R(a,a) \\\
a^{-1} = R_2 &= R(R(a,a),a) \\\
ab = R_3 &= R(a, R(R(b,b),b))
\\end{align}

## Encoding Mathematical Structures

By constructing all of our representations of mathematical structures in this way, we eliminate all of the terminology and verbal definitions. Instead the mathematical structure is represented in a more abstract form that can be used for all finite mathematical structures. 

Therefore, it is pretty straight forward to come up with an encoding scheme $\gamma$ to encode the representation of a finite mathematical structure $\phi$ as finite chain of integers. 

### Quick Notation

Let a string of integers that is denoted $c$ be reprentative of: 

$$ c = \bc{k_1, k_2, \ldots, k_n} $$

Where the $k_i \in \mathbb{Z}$ are just integers. Let the union of two chains of integers $c_1$ and $c_2$ from end to end be $c_1 \circ c_2$. It is important to note that $c_1 \circ c_2 \neq c_2 \circ c_1$. Let the repeated union of strings be denoted as:

$$ \coprod_{i=1}^n c_i = c_1 \circ c_2 \circ \ldots \circ c_n $$

### Tegmark's Encoding

Now just like structure definitions, there is no unique encoding scheme. One possible scheme suggested by Tegmark was:

$$ \gamma(\phi) = \bc{\# \text{ of sets}} \circ \bc{\# \text{ of relations}} \circ \coprod_{i=1}^{\# S_{\phi}} \gamma_S (S_i) \circ \coprod_{i=1}^{\# R_{\phi}} \gamma_R (R_i) $$

Where $$\# S_{\phi}$$ is the number of sets belonging to the $\phi$ and $$\# R_{\phi}$$ is similarily the number of relations belonging to $\phi$. Moreover, $\gamma_S$ is the encoding scheme for a set $S$ given simply by:

$$ \gamma_S(S) = \bc{\# \text{ members of set } S} $$

and $\gamma_R$ is the encoding for a given relation given by:

$$ \gamma_R(R) = \bc{\# \text{ of args of } R} \circ \coprod_{i=1}^{\# \text{args}} \bc{\text{type of arg } i} \circ \bc{\text{type of output of } R} \circ \bc{\text{value array of } R} $$

Where here, the type of an argument (arg) of $R$ is the integer associated with the set that supplies possible values for that argument. Also, the value array of $R$ is the concatenated chain of intgers that are in the boxes used above.

#### Examples

Using this construction of $\gamma$, here are a couple of encodings for simple finite mathematical structures.

| Mathematical Structure $\phi$ | Encoding $\gamma(\phi)$ |
|:--------------------------:|:--------------------------:|
| The empty set              | 100                        |
| The set of 5 elements      | 105                        |
| The trivial group $C_1$    | 11120000                   |
| The polygon $P_3$          | 113100120                  |
| The group $C_2$            | 11220000110                |
| Boolean algebra            | 11220001110                |
| The group $C_3$            | 1132000012120201           |

Now that we have a method for encoding every finite mathematical structure as a chain of integers, we can measure how complex that mathematical structure really is. The general idea is that simpler structures like the empty set have shorter encodings with entries of smaller size. Tegmark suggests simply adding up the entries of the encoding with logarithmic weighting. He calls $H(c)$ the complexity of encoding $c$.

$$ H(c) = \sum\limits_{i=1}^{n} \log_2 (2 + k_i) $$

The addition of 2 here is necessary to ensure the encodings containing many zeros $\ldots00000\ldots$ are properly measured. Using this complexity measure $H$ with some examples gives:

| Mathematical Structure $\phi$ | Complexity $H(c)$ |
|:--------------------------:|:--------------------------:|
| The empty set              | 3.58496250072              |
| The set of 5 elements      | 5.39231742278              |
| The trivial group $C_1$    | 10.7548875022              |
| The polygon $P_3$          | 13.6617780978              |
| The group $C_2$            | 15.3398500029              |
| Boolean algebra            | 15.9248125036              |
| The group $C_3$            | 24.2467405985              |

Here is some python code used to calculate the complexity of an encoding:

{% highlight python %}
from math import log

def tegmark_complexity(encoding):
    complexity = 0
    for entry in encoding:
        complexity += log(2 + entry,2)
    return complexity
{% endhighlight %}

## Complexity of $H(c)$

One important point to make at this point is that the encoding scheme suggested by Tegmark isn't well equipped for infinite mathematical structures. In his paper he mentions,

<div class="message">
  ...the encoding scheme above must be replaced by one that defines the relations not by explicit tabulation, but by providing an algorithm or computer program that implements them.
</div>

In terms of the complexity of a mathematical structure, there doesn't necessarily need to be a reversable encoding to measure complexity. In the future I'll write a post about this. Nonetheless I want to ask a rather interesting question.

The complexity metric suggested by Tegmark is just an example. You could construct many other ones that all accomplish the task of enumerating the complexity of all finite mathematical structures. By the algorithm behind it relies on the infinite mathematical structure containing everything from sets such as the real numbers, to relations like logarithms, addition, multiplication, etc. All of such sub-structures are infinite in many ways. 

My question is:

<div class="message">
  Does there exist and finite mathematical structure $\phi^*$ that has a relation capable of producing a complexity $H$ for every other finite mathematical structure? And if so, what is the complexity of this special structure $H(\phi^*)$?
</div>

Quite simply, it is simple to prove that there does not exist a finite mathematical structure that can generate a measurement of complexity of all finite mathematical structures because there are an infinite number of finite mathematical structures. This would be mean the set $S$ associated with $\phi^*$ would require a member for each unique complexity. However, it is still possible to have a relation that has two arguments encoding $c_1$ and encoding $c_2$, and returns the more complex encoding. This could be used to compare and rank all finite mathematical structures. However, for the same reason, this would enforce $S$ to be infinite and thus the mathematical structure $$\phi^*$$ does not exist. Bummer.

Nonetheless, this might still be possible for infinite mathematical structures. I do not know at the moment.