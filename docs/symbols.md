# List of symbols

A quick reference for the notation used across these answers. Skim it whenever a symbol looks unfamiliar.

## Sets and spaces

| Symbol | Meaning |
|:------:|:--------|
| $\mathbb{R}$ | the real numbers |
| $\mathbb{R}^n$ | the space of real vectors with $n$ entries |
| $\mathbb{Z}_n$ | the integers modulo $n$: $\{[0],[1],\dots,[n-1]\}$ |
| $\in$ | "is an element of" |
| $\subseteq$ | "is a subset of" |
| $\{\,\cdot\mid\cdot\,\}$ | set-builder: $\{\,x \mid \text{condition}\,\}$ |
| $\varnothing$ | the empty set (no solutions) |

## Vectors and matrices

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

## Operations

| Symbol | Meaning |
|:------:|:--------|
| $\mathbf{x}^\top\mathbf{y}$ | dot product (standard inner product) |
| $\langle\mathbf{x},\mathbf{y}\rangle$ | inner product (possibly weighted, $\mathbf{x}^\top A\mathbf{y}$) |
| $\lVert\mathbf{x}\rVert$ | norm (length): $\sqrt{\langle\mathbf{x},\mathbf{x}\rangle}$ |
| $\star,\ \oplus,\ \otimes$ | custom operations defined within a problem |
| $\circ$ | composition of maps: $(g\circ f)(x) = g(f(x))$ |
| $\approx$ | approximately equal |
| $\neq$ | not equal |

## Maps and subspaces

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

## Geometry

| Symbol | Meaning |
|:------:|:--------|
| $d(\mathbf{x},\mathbf{y})$ | distance: $\lVert\mathbf{x}-\mathbf{y}\rVert$ |
| $\theta$ | angle between two vectors |
| $\pi_U(\mathbf{x})$ | orthogonal projection of $\mathbf{x}$ onto the subspace $U$ |
