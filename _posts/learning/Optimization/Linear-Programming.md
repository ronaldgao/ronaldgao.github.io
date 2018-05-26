---
layout: post
title: "Linear-Programming"
modified:
categories: learning
excerpt:
tags: []
image:
  feature:
date: 2018-05-21T15:39:55-04:00
modified: 2016-06-01T14:19:19-04:00
---

# Materials
- [https://github.com/ronaldgao1234/Optimization](https://github.com/ronaldgao1234/Optimization)
- This is covered in Chapter 15 of Introduction to Optimization(Chong, Zak)

## Brief History
*Image of LP prob being subset of general constrained optimization problems*
Goal: find a point that minimizes the objectives function and at the same time satisfies the constraints
In LP, the problem is linear

**Feasible Point:** Any point that satisfies the constraints

All you gotta do is find __basic feasible solutions_

**Brute-force approach:** comparing the finite number of basic feasible solutions and finding one that minimizes or maximizes the objectives function.
- why brute force sucks
- heuristic
- Simplex method by Dantzig is declared one of the 10 algo's with greatest influence on the development of
science and engineering!
- Simplex has exponential -worst-case-complexity
- interior-point-methods Karmarkar development of many other nonsimplex methods

**Lemma:** If A has rank \\(n<m\\), then rank \\(rank(A^TA) = n\\) &nbsp;&&nbsp;  \\(A^TA > 0\\)
https://faculty.math.illinois.edu/~llpku/2007fall415/hw1031.pdf hopefully
**Theorem:** The unique global minimizer is \\(x^* = (A^TA)^{-1}A^Tb\\)

Pf in notes

Some graph here:

```python
print("Hello World!")
```

## Quick Review
### 1. _Vector_

Here some common forms:
\\[\alpha\in\mathbb{R}^n\\]
\\[ \alpha =
\begin{pmatrix}
  a_1 \\\
  a_2 \\\
  .   \\\
  .   \\\
  .   \\\
  a_n
\end{pmatrix}
\\]

Transpose of the vector:
\\[
\alpha^T = ( \alpha_1, \alpha_2, .., \alpha_n)
\\]

**Propositions:**
1. A set of vectors is linearly dependent if one vector is the linear combination of the remaining vectors
2. Span of \\(\alpha_1, \alpha_2, ... , \alpha_k\\) is a subspace \\(\subseteq\mathbb{R}^n\\), given by \\(span(\alpha_1,\alpha_2,...,\alpha_k):=\{\sum_{i=1}^{k}\beta_i\alpha_i : \beta_i\in\mathbb{R}\}\\)

### 2. _Inner Product_
\\(x,y\in\mathbb{R^n}\\)
\\[<x,y> = \sum_{i=1}^{k}x_iy_i = x^Ty\\]
**Euclidean norm**:
\\[||x|| = \sqrt{<x,x>}=\sqrt{x^Tx}=\sqrt{\sum_{i=1}^nx_i^2}\\]
**Cauchy-Schwartz Inequality:**
\\[|<x,y>| \leq||x||\cdot||y||\\]
Intuitive Proof:
Basically the dot product(the standard inner product that we're going to be using) is just the (1st vec length * cos(angle between both vec's) * 2nd vec length).

Then, cosine's max is just 1 so you get the second inequality.
Here's a good explanation: [https://math.oregonstate.edu/home/programs/undergrad/CalculusQuestStudyGuides/vcalc/dotprod/dotprod.html](https://math.oregonstate.edu/home/programs/undergrad/CalculusQuestStudyGuides/vcalc/dotprod/dotprod.html)
\\[|<x,y>|=(||x||\cdot|cos\theta|)\cdot ||y||\leq||x||\cdot|y||\\]
### 3. _Matrix_
\\[A\in\mathbb{R^{m \times n}}\\]
\\[A=\begin{bmatrix}
a_{11} & a_{12} & . & a_{1n} \\\
a_{21} & . & . & .\\\
. & . & . & .\\\
.  & . & . & .\\\
a_{m1} & . & . & a_{m\times n}\\\
\end{bmatrix} = [a_1,a_2,...,a_n]
\tag1\\]
We definitely will use the 2nd form of (1) a lot

**Propositions:**
\\(rank(A) = k \leftrightarrow dim(span[a_1,a_2,...,a_n]) = k\\)

### 4. _Eigenvalues and Eigenvectors_
  1. If \\(Av = \lambda v\\), then \\(\lambda\\) is the eigenvalue of A, and v is the eigenvector
  2. \\(\lambda\\) is the root of the charateristic polynomial \\(det(\lambda I - A)\\)
  3. All eigenvalues of A are real if \\(A^T = A\\) (symmetric)

Lastly,
Quadratic form: (Given \\(Q^T = Q: x^TQx = \sum^n_{i=1}\sum^n_{j=1}q_{ij}x_ix_j\\))
1. Q is positive definite if \\(x^TQx > 0\\) &nbsp; \\(\forall x\neq0\\)
2. Q is semi-positive definite if \\(x^TQx \geq 0\\), &nbsp; \\(\forall x\in\mathbb{R^n}\\)
