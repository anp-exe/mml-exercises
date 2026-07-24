# MML Exercise Answers

Worked solutions to the **end-of-chapter exercises** in *Mathematics for Machine Learning* (Deisenroth, Faisal & Ong). The full book is freely available [here](https://mml-book.github.io/book/mml-book.pdf).

Each question is laid out the same way: a **Topics & Definitions** box, a plain-English explanation, the **worked steps** (with real matrices), then the **answer**. New to the notation? See the [list of symbols](#list-of-symbols) at the bottom of this page.

---

## Progress

| Chapter | Exercises answered |
|:------:|:------------------:|
| 2 · Linear Algebra | ✅ 2.1–2.20 complete |
| 3 · Analytic Geometry | ✅ 3.1–3.10 complete |
| 4 · Matrix Decompositions | ✅ 4.1–4.12 complete |
| 5 · Vector Calculus | ✅ 5.1–5.4, 5.5a |
| 6 · Probability & Distributions | ⬜ |
| 7 · Continuous Optimization | ⬜ |
| 8 · When Models Meet Data | ⬜ |
| 9 · Linear Regression | ⬜ |
| 10 · Dimensionality Reduction (PCA) | ⬜ |
| 11 · Density Estimation (GMM) | ⬜ |
| 12 · Classification (SVM) | ⬜ |

---

## Helpful resources

!!! tip "Stuck reducing a matrix to RREF?"
    This calculator shows every elimination step, which is great for checking your own work:
    [emathhelp RREF calculator](https://www.emathhelp.net/calculators/linear-algebra/reduced-row-echelon-form-rref-calculator/)

For building real intuition on vectors, transformations, and matrices, 3Blue1Brown's
[**Essence of Linear Algebra**](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)
video series is fantastic and highly recommended.

For linear mappings specifically, [**this video**](https://youtu.be/is1cg5yhdds) is a clear, helpful walkthrough.

Another [**helpful video**](https://youtu.be/3d6DsjIBzJ4) worth a watch.

For the calculus side of things (Chapter 5 onward), [**Paul's Online Math Notes**](https://tutorial.math.lamar.edu/) are a thorough, well-explained reference for Calculus I, II, and III.

---

## How this site is built

Static site generated with **MkDocs + Material**, math rendered with **KaTeX**.
See the `README.md` in the repo for how to run it locally and deploy to GitHub Pages.

!!! theory "Conventions"
    - Pastel aesthetic (lilac / sage / pink)
    - Each question: definitions box → explanation → worked steps → answer
    - Math written in LaTeX, rendered by KaTeX

---

## List of symbols

A quick reference for the notation used across these answers. Skim it whenever a symbol looks unfamiliar.

### Sets and spaces

| Symbol | Meaning |
|:------:|:--------|
| $\mathbb{R}$ | the real numbers |
| $\mathbb{R}^n$ | the space of real vectors with $n$ entries |
| $\mathbb{Z}_n$ | the integers modulo $n$: $\{[0],[1],\dots,[n-1]\}$ |
| $\in$ | "is an element of" |
| $\subseteq$ | "is a subset of" |
| $\{\,\cdot\mid\cdot\,\}$ | set-builder: $\{\,x \mid \text{condition}\,\}$ |
| $\varnothing$ | the empty set (no solutions) |

### Vectors and matrices

| Symbol | Meaning |
|:------:|:--------|
| $\mathbf{x},\ \mathbf{y}$ | vectors (bold lowercase) |
| $\mathbf{0}$ | the zero vector |
| $x_i$ | the $i$-th entry of $\mathbf{x}$ |
| $A,\ B$ | matrices (uppercase) |
| $A^\top,\ \mathbf{x}^\top$ | transpose (rows become columns) |
| $A^{-1}$ | matrix inverse ($AA^{-1} = I$) |
| $I$ | the identity matrix |
| $\det A$ | determinant of $A$ |
| $\operatorname{rank}(A),\ \operatorname{rk}(A)$ | rank: the number of pivots |

### Operations

| Symbol | Meaning |
|:------:|:--------|
| $\mathbf{x}^\top\mathbf{y}$ | dot product (standard inner product) |
| $\langle\mathbf{x},\mathbf{y}\rangle$ | inner product (possibly weighted, $\mathbf{x}^\top A\mathbf{y}$) |
| $\lVert\mathbf{x}\rVert$ | norm (length): $\sqrt{\langle\mathbf{x},\mathbf{x}\rangle}$ |
| $\star,\ \oplus,\ \otimes$ | custom operations defined within a problem |
| $\circ$ | composition of maps: $(g\circ f)(x) = g(f(x))$ |
| $\approx$ | approximately equal |
| $\neq$ | not equal |

### Maps and subspaces

| Symbol | Meaning |
|:------:|:--------|
| $\Phi,\ f,\ g$ | linear maps (homomorphisms) |
| $\mapsto$ | "maps to": $\mathbf{x}\mapsto\Phi(\mathbf{x})$ |
| $A_\Phi$ | the transformation matrix of $\Phi$ |
| $\ker(\Phi)$ | kernel: inputs sent to $\mathbf{0}$ |
| $\operatorname{Im}(\Phi)$ | image: all reachable outputs |
| $\dim(U)$ | dimension of a subspace |
| $\operatorname{span}[\cdots]$ | span: all linear combinations of the listed vectors |
| $U_1 \cap U_2$ | intersection: vectors lying in both subspaces |
| $U_1 + U_2$ | sum: all $\mathbf{u}_1 + \mathbf{u}_2$ |
| $\lambda$ | a scalar coordinate or an eigenvalue |

### Geometry

| Symbol | Meaning |
|:------:|:--------|
| $d(\mathbf{x},\mathbf{y})$ | distance: $\lVert\mathbf{x}-\mathbf{y}\rVert$ |
| $\theta$ | angle between two vectors |
| $\pi_U(\mathbf{x})$ | orthogonal projection of $\mathbf{x}$ onto the subspace $U$ |
