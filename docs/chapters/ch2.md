# Chapter 2 · Linear Algebra

End-of-chapter exercises. Each has a definitions box, explanation, worked steps, and the answer.

---

## 2.1 · Custom operation $a \star b = ab + a + b$ on $\mathbb{R}\setminus\{-1\}$

!!! theory "Topics & Definitions"
    - **Group** — a set with an operation obeying 4 axioms: closure, associativity, identity, inverses.
    - **Abelian group** — a group whose operation is also commutative ($a\star b = b\star a$).
    - **Identity $e$** — the element with $a\star e = a$.
    - **Inverse** — the element that undoes $a$, returning $e$.

The key move is factoring: $a \star b = (a+1)(b+1) - 1$. So the operation behaves like ordinary multiplication shifted by $1$, which makes every axiom easy. It is closed (never gives $-1$), associative, has identity $0$, every element has an inverse, and it is commutative.

For part b, solve $3 \star x \star x = 4(x+1)^2 - 1 = 15$.

!!! answer "Answer"
    $(\mathbb{R}\setminus\{-1\},\ \star)$ is an **Abelian group**. Identity $e = 0$, inverse $a^{-1} = \dfrac{-a}{a+1}$.

    **2.1b:** $x = 1$ or $x = -3$.

---

## 2.2 · Integers mod $n$ under $\oplus$

!!! theory "Topics & Definitions"
    - **Congruence class $[a]$** — all integers with the same remainder as $a$ mod $n$.
    - **Modular addition** — $[a] \oplus [b] = [a+b]$, then reduce mod $n$.
    - **Prime condition** — $(\mathbb{Z}_n\setminus\{0\}, \otimes)$ is a group only when $n$ is prime.

$\mathbb{Z}_n = \{[0],[1],\dots,[n-1]\}$ with $[a]\oplus[b] = [a+b]$ reduced mod $n$. It is a group because ordinary integer addition already is, and the classes inherit that.

!!! answer "Answer"
    $(\mathbb{Z}_n, \oplus)$ is an **Abelian group**. Identity $[0]$, inverse of $[a]$ is $[n-a]$.

    $(\mathbb{Z}_n\setminus\{0\}, \otimes)$ is a group **iff $n$ is prime**.

---

## 2.3 · Upper-unitriangular $3\times 3$ matrices under multiplication

!!! theory "Topics & Definitions"
    - **Matrix group** — a set of matrices closed under multiplication satisfying the 4 axioms.
    - **Upper unitriangular** — $1$s on the diagonal, $0$s below, free entries above.
    - **Non-commutative** — $AB \neq BA$ in general, so a group can be non-Abelian.

$G$ is all matrices $\begin{bmatrix}1&x&z\\0&1&y\\0&0&1\end{bmatrix}$. Multiplying two keeps the shape (closed), multiplication is associative, the identity is in $G$, and inverses stay in $G$. But the $(1,3)$ entry of a product depends on order, so it is not Abelian.

!!! answer "Answer"
    $(G, \cdot)$ is a **group**, but **not Abelian**.

---

## 2.4 · Matrix products (check dimensions first!)

!!! theory "Topics & Definitions"
    - **Dimension rule** — $AB$ is defined only if $A$'s columns $=$ $B$'s rows: $(m\times n)(n\times p)\to(m\times p)$.
    - **Entry rule** — entry $(i,j)$ = row $i$ of $A$ dotted with column $j$ of $B$.
    - **Non-commutative** — compare b and c: same matrices swapped, different results.

Part **a** is a $3\times 2$ times a $3\times 3$: inner dimensions $2$ and $3$ do not match, so it is **undefined**.

!!! answer "Answer"
    **a)** undefined (dimension mismatch)

    **b)** $\begin{bmatrix}4&3&5\\10&9&11\\16&15&17\end{bmatrix}$
    &nbsp;&nbsp; **c)** $\begin{bmatrix}5&7&9\\11&13&15\\8&10&12\end{bmatrix}$

    **d)** $\begin{bmatrix}14&6\\-21&2\end{bmatrix}$
    &nbsp;&nbsp; **e)** $\begin{bmatrix}12&3&-3&-12\\-3&1&2&6\\6&5&1&0\\13&12&3&2\end{bmatrix}$

---

## 2.5 · Find all solutions of $A\mathbf{x} = \mathbf{b}$

!!! theory "Topics & Definitions"
    - **Gaussian elimination** — row operations to reach echelon form.
    - **Contradiction row** — $0 = \text{nonzero}$ means inconsistent, no solution.
    - **Free variable** — a column with no pivot, giving infinitely many solutions.

!!! answer "Answer"
    **2.5a:** no solution, $S = \varnothing$ (a contradiction row appears).

    **2.5b:** infinitely many solutions, two free parameters.

---

## 2.6 · Solving $A\mathbf{x} = \mathbf{b}$ with Gaussian elimination

!!! theory "Topics & Definitions"
    - **RREF** — pivots are $1$, alone in their column, stepping down-right.
    - **Pivot vs free column** — pivot columns give basic variables; no-pivot columns give free variables.
    - **General solution** — one particular solution plus the free-variable directions.

Reducing $[A\mid \mathbf{b}]$ to RREF puts pivots in columns $2, 4, 5$; columns $1, 3, 6$ are free.

!!! steps "RREF of $[A \mid \mathbf{b}]$"
    $$\left[\begin{array}{cccccc|c}
    0&1&0&0&0&1&1\\
    0&0&0&1&0&1&-2\\
    0&0&0&0&1&-1&1
    \end{array}\right]$$

    Pivots in columns $2, 4, 5 \Rightarrow x_2, x_4, x_5$ basic; $x_1, x_3, x_6$ free.

!!! answer "Answer"
    $$\mathbf{x} = \begin{pmatrix}0\\1\\0\\-2\\1\\0\end{pmatrix}
    + x_1\begin{pmatrix}1\\0\\0\\0\\0\\0\end{pmatrix}
    + x_3\begin{pmatrix}0\\0\\1\\0\\0\\0\end{pmatrix}
    + x_6\begin{pmatrix}0\\-1\\0\\-1\\1\\1\end{pmatrix},\quad x_1,x_3,x_6\in\mathbb{R}$$

---

## 2.7 · Solving $A\mathbf{x} = 12\mathbf{x}$

!!! theory "Topics & Definitions"
    - **Eigenvalue / eigenvector** — $A\mathbf{x} = \lambda\mathbf{x}$: a vector $A$ only scales, never rotates; $\lambda$ is the scale factor.
    - **Rearrangement** — $A\mathbf{x} = \lambda\mathbf{x} \Rightarrow (A - \lambda I)\mathbf{x} = 0$, a homogeneous system.
    - **Eigenspace** — all eigenvectors for a given $\lambda$ (a line/plane through the origin).
    - **Constraint** — an extra equation like $\sum x_i = 1$ picks one point on that line.

!!! steps "$(A - 12I)\mathbf{x} = 0$ elimination"
    $$\begin{bmatrix}-6&4&3\\6&-12&9\\0&8&-12\end{bmatrix}
    \longrightarrow
    \begin{bmatrix}-6&4&3\\0&-8&12\\0&0&0\end{bmatrix}$$

    Zero row $\Rightarrow x_3$ free. Then $x_2 = \tfrac32 x_3,\ x_1 = \tfrac32 x_3 \Rightarrow \mathbf{x} = t(3,3,2)$.
    The constraint $3t + 3t + 2t = 1$ gives $t = \tfrac18$.

!!! answer "Answer"
    $$\mathbf{x} = \left(\tfrac38,\ \tfrac38,\ \tfrac14\right)$$

---

## 2.8 · Inverses

!!! theory "Topics & Definitions"
    - **Inverse $A^{-1}$** — the matrix with $A\,A^{-1} = I$.
    - **Determinant** — a number measuring how much $A$ scales space.
    - **Invertible iff $\det \neq 0$** — $\det = 0$ means $A$ squashes a dimension, so no inverse.
    - **Gauss–Jordan** — reduce $[A\mid I]$ until the left is $I$; the right becomes $A^{-1}$.

**Part a.** $\det = 0$ (row 1 + row 3 = $2\times$ row 2), so no inverse.

!!! steps "$[A \mid I] \to [I \mid A^{-1}]$"
    $$\left[\begin{array}{cccc|cccc}
    1&0&1&0&1&0&0&0\\
    0&1&1&0&0&1&0&0\\
    1&1&0&1&0&0&1&0\\
    1&1&1&0&0&0&0&1
    \end{array}\right]
    \longrightarrow
    \left[\begin{array}{cccc|cccc}
    1&0&0&0&0&-1&0&1\\
    0&1&0&0&-1&0&0&1\\
    0&0&1&0&1&1&0&-1\\
    0&0&0&1&1&1&1&-2
    \end{array}\right]$$

!!! answer "Answer"
    **a)** not invertible ($\det = 0$).

    **b)** $A^{-1} = \begin{bmatrix}0&-1&0&1\\-1&0&0&1\\1&1&0&-1\\1&1&1&-2\end{bmatrix}$

---

## 2.9 · Which sets are subspaces of $\mathbb{R}^3$?

!!! theory "Topics & Definitions"
    - **Subspace** — a subset containing $\mathbf{0}$, closed under addition and scaling.
    - **The 3 tests** — contains $\mathbf{0}$; closed under $+$; closed under scalar $\times$.
    - **Span** — all linear combinations of given vectors; always a subspace.
    - **The 3 killers** — a square term, an integer-only condition, or $=$ a nonzero constant.

- **a.** A span of two vectors $\Rightarrow$ subspace.
- **b.** Has $\lambda^2$ (never negative); scaling $(1,-1,0)$ by $-1$ escapes $\Rightarrow$ not.
- **c.** A plane; through the origin only when $\gamma = 0$.
- **d.** Integer middle coordinate; scaling $(0,1,0)$ by $0.5$ escapes $\Rightarrow$ not.

!!! answer "Answer"
    **a)** subspace &nbsp;·&nbsp; **b)** not &nbsp;·&nbsp; **c)** subspace iff $\gamma = 0$ &nbsp;·&nbsp; **d)** not

---

## 2.10 · Linear independence

!!! theory "Topics & Definitions"
    - **Linearly independent** — the only combination giving $\mathbf{0}$ is all-zero coefficients.
    - **Linearly dependent** — some vector is a combination of the others.
    - **Method** — vectors as columns, row-reduce, count pivots.
    - **Rule** — pivot in every column $\Rightarrow$ independent; a missing column pivot $\Rightarrow$ dependent.

!!! steps "Vectors as columns, then reduce"
    $$\text{a)}\ \begin{bmatrix}2&1&3\\-1&1&-3\\3&-2&8\end{bmatrix}
    \longrightarrow
    \begin{bmatrix}2&1&3\\0&3&-3\\0&0&0\end{bmatrix}$$

    a) only 2 pivots, a zero row $\Rightarrow$ **dependent**. &nbsp; b) 3 pivots (rank 3) $\Rightarrow$ **independent**.

!!! answer "Answer"
    **a)** linearly dependent, with $\mathbf{x}_3 = 2\mathbf{x}_1 - \mathbf{x}_2$.

    **b)** linearly independent (rank $3$).

---

## 2.11 · Write $\mathbf{y}$ as a linear combination

!!! theory "Topics & Definitions"
    - **Linear combination** — $\lambda_1\mathbf{v}_1 + \lambda_2\mathbf{v}_2 + \lambda_3\mathbf{v}_3$: scale each vector, then add.
    - **Set-up** — build $[\mathbf{x}_1\ \mathbf{x}_2\ \mathbf{x}_3 \mid \mathbf{y}]$, same as solving a system.
    - **Method** — reduce to RREF; the coefficients appear in the final column.

!!! steps "$[\mathbf{x}_1\ \mathbf{x}_2\ \mathbf{x}_3 \mid \mathbf{y}] \to$ RREF"
    $$\left[\begin{array}{ccc|c}
    1&1&2&1\\1&2&-1&-2\\1&3&1&5
    \end{array}\right]
    \longrightarrow
    \left[\begin{array}{ccc|c}
    1&0&0&-6\\0&1&0&3\\0&0&1&2
    \end{array}\right]$$

    Check: $-6(1) + 3(1) + 2(2) = 1$, matching $\mathbf{y}$.

!!! answer "Answer"
    $$\mathbf{y} = -6\,\mathbf{x}_1 + 3\,\mathbf{x}_2 + 2\,\mathbf{x}_3$$

---

## 2.12 · Basis of $U_1 \cap U_2$

!!! theory "Topics & Definitions"
    - **Intersection $U_1 \cap U_2$** — all vectors that lie in both subspaces at once.
    - **Key idea** — a vector is in the intersection when it is a combination of the $\mathbf{u}$'s *and* of the $\mathbf{w}$'s: $a_1\mathbf{u}_1 + a_2\mathbf{u}_2 + a_3\mathbf{u}_3 = b_1\mathbf{w}_1 + b_2\mathbf{w}_2 + b_3\mathbf{w}_3$.
    - **Set-up** — move everything to one side: $a_1\mathbf{u}_1+a_2\mathbf{u}_2+a_3\mathbf{u}_3 - b_1\mathbf{w}_1 - b_2\mathbf{w}_2 - b_3\mathbf{w}_3 = \mathbf{0}$, a homogeneous system with columns $[\mathbf{u}_1\ \mathbf{u}_2\ \mathbf{u}_3 \mid -\mathbf{w}_1\ -\mathbf{w}_2\ -\mathbf{w}_3]$.
    - **Free variable** — a column with no pivot; here $b_3$, which parameterises the (one-dimensional) intersection.

Stack the six vectors as columns of a $4\times 6$ matrix and row-reduce. Two $\mathbf{u}$ columns and two $\mathbf{w}$ columns take pivots, leaving $b_3$ free. Back-substituting recovers the $b$ coefficients, and feeding them into $b_1\mathbf{w}_1+b_2\mathbf{w}_2+b_3\mathbf{w}_3$ rebuilds the shared vector.

!!! steps "Reduce, then rebuild the intersection vector"
    Row echelon form of $[\mathbf{u}_1\ \mathbf{u}_2\ \mathbf{u}_3 \mid -\mathbf{w}_1\ -\mathbf{w}_2\ -\mathbf{w}_3]$:

    $$\left[\begin{array}{ccc|ccc}
    1&2&-1&-1&2&-3\\
    0&1&-\tfrac23&\tfrac13&\tfrac43&-3\\
    0&0&0&1&1&-\tfrac72\\
    0&0&0&0&1&-\tfrac72
    \end{array}\right]$$

    Column $b_3$ has no pivot, so set $b_3 = t$. Back-substitution gives
    $$b_2 = \tfrac72 t, \qquad b_1 = -b_2 + \tfrac72 t = 0.$$
    Choosing $t = 2$ to clear fractions: $b_1 = 0,\ b_2 = 7,\ b_3 = 2$.

    Rebuild the intersection vector from the $\mathbf{w}$ side:
    $$7\mathbf{w}_2 + 2\mathbf{w}_3 = 7\begin{pmatrix}2\\-2\\0\\0\end{pmatrix} + 2\begin{pmatrix}-3\\6\\-2\\-1\end{pmatrix} = \begin{pmatrix}14\\-14\\0\\0\end{pmatrix} + \begin{pmatrix}-6\\12\\-4\\-2\end{pmatrix} = \begin{pmatrix}8\\-2\\-4\\-2\end{pmatrix}.$$

    Dividing by $2$ gives the simplest representative $(4,-1,-2,-1)$.

!!! answer "Answer"
    $U_1 \cap U_2$ is one-dimensional, with basis
    $$\left\{\,(4,\ -1,\ -2,\ -1)\,\right\}.$$

---

## 2.13 · Subspaces as solution spaces $U_1 = \ker A_1,\ U_2 = \ker A_2$

!!! theory "Topics & Definitions"
    - **Solution space (null space)** — every $\mathbf{x}$ with $A\mathbf{x} = \mathbf{0}$; a subspace of the domain $\mathbb{R}^3$.
    - **Rank–nullity** — $\dim(\ker A) = n - \operatorname{rank}(A)$, where $n$ is the number of columns.
    - **Basis from free variables** — each column without a pivot gives one basis vector.
    - **Mind the definition** — here the $U$'s are *solution* spaces, so the dimension counts free variables, not pivots (contrast with 2.14).

Both $A_1$ and $A_2$ are $4\times 3$, so $\mathbf{x}\in\mathbb{R}^3$. Row-reducing each one gives rank $2$, leaving a single free variable, so both solution spaces are one-dimensional. Strikingly, the two matrices reduce to the *same* echelon form, so $U_1$ and $U_2$ turn out to be the identical line.

!!! steps "Reduce each $A_i$ and read the null space"
    $$A_1 \longrightarrow \begin{bmatrix}1&0&1\\0&1&1\\0&0&0\\0&0&0\end{bmatrix},
    \qquad
    A_2 \longrightarrow \begin{bmatrix}1&0&1\\0&1&1\\0&0&0\\0&0&0\end{bmatrix}$$

    Both give $x_1 = -x_3$ and $x_2 = -x_3$. Setting $x_3 = t$:
    $$\mathbf{x} = t\,(-1,\,-1,\,1).$$
    Same for both, so $U_1 = U_2$ and the intersection is that same line.

!!! answer "Answer"
    **a)** $\dim U_1 = \dim U_2 = 1$.

    **b)** Basis of $U_1$ = basis of $U_2$ = $\left\{\,(-1,\,-1,\,1)\,\right\}$.

    **c)** Since $U_1 = U_2$, the intersection is the same line: $\left\{\,(-1,\,-1,\,1)\,\right\}$.

---

## 2.14 · Subspaces as column spaces $U_1 = \operatorname{col} A_1,\ U_2 = \operatorname{col} A_2$

!!! theory "Topics & Definitions"
    - **Column space** — the span of a matrix's columns; here a subspace of $\mathbb{R}^4$.
    - **Dimension $=$ rank** — the number of pivot columns.
    - **Basis $=$ original pivot columns** — reduce to find *which* columns are pivots, then take those columns from the **original** matrix (row ops change the columns, so never read the basis off the RREF).
    - **Intersection** — solve $c_1\mathbf{v}_1 + c_2\mathbf{v}_2 = d_1\mathbf{w}_1 + d_2\mathbf{w}_2$, a homogeneous system in $(c_1,c_2,d_1,d_2)$.

Same two matrices as 2.13, but now the $U$'s are spanned by the columns. Each has rank $2$ with pivots in columns $1$ and $2$, so the first two columns of each original matrix form a basis. For the intersection, stack the two bases (negating $U_2$'s) and solve.

!!! steps "Intersection system $[\mathbf{v}_1\ \mathbf{v}_2 \mid -\mathbf{w}_1\ -\mathbf{w}_2]$"
    $$\left[\begin{array}{cc|cc}
    1&0&-3&3\\
    1&-2&-1&-2\\
    2&1&-7&5\\
    1&0&-3&1
    \end{array}\right]
    \longrightarrow
    \left[\begin{array}{cc|cc}
    1&0&-3&0\\
    0&1&-1&0\\
    0&0&0&1\\
    0&0&0&0
    \end{array}\right]$$

    Pivots in $c_1, c_2, d_2$; the $d_1$ column is free. Back-substitution gives $d_2 = 0$, $c_2 = d_1$, $c_1 = 3d_1$. Taking $d_1 = 1$:
    $$\mathbf{x} = 3\mathbf{v}_1 + \mathbf{v}_2 = 3\begin{pmatrix}1\\1\\2\\1\end{pmatrix} + \begin{pmatrix}0\\-2\\1\\0\end{pmatrix} = \begin{pmatrix}3\\1\\7\\3\end{pmatrix},$$
    which is exactly $\mathbf{w}_1$, confirming it lies in both spaces. By Grassmann, $\dim(U_1\cap U_2) = 2 + 2 - 3 = 1$.

!!! answer "Answer"
    **a)** $\dim U_1 = \dim U_2 = 2$.

    **b)** Basis of $U_1 = \left\{\,(1,1,2,1),\ (0,-2,1,0)\,\right\}$; &nbsp; basis of $U_2 = \left\{\,(3,1,7,3),\ (-3,2,-5,-1)\,\right\}$.

    **c)** Basis of $U_1 \cap U_2 = \left\{\,(3,\,1,\,7,\,3)\,\right\}$.

!!! note "Why 2.13 and 2.14 differ (the thing to actually remember)"
    Same matrices $A_1, A_2$, but the two problems ask about **opposite** subspaces, so both the dimension formula and the way you read off a basis flip:

    | | 2.13 · solution space | 2.14 · column space |
    |---|---|---|
    | **What $U$ is** | all $\mathbf{x}$ with $A\mathbf{x}=\mathbf{0}$ ($\ker A$) | the span of $A$'s columns ($\operatorname{col} A$) |
    | **Dimension** | $\dim = n - \operatorname{rank}(A)$ (free variables) | $\dim = \operatorname{rank}(A)$ (pivots) |
    | **Basis from** | solving the system, one vector per free variable | the **original** columns sitting in pivot positions |
    | **Here** | $3 - 2 = 1$ | $2$ |

    So the $\dim = n - \operatorname{rank}$ formula is a **null-space** fact. It is easy to reach for it in 2.14, but a column space is measured by the rank directly. Rank–nullity ties them together: $\operatorname{rank}(A) + \dim(\ker A) = n$, here $2 + 1 = 3$.

!!! note "The rank–nullity theorem, in plain words"
    Think of a matrix as a machine with one slot for each column. When you row-reduce it, every column ends up in one of two piles:

    - **Pivot columns** are the ones pulling their own weight, each adds a genuinely new direction the matrix can reach. How many there are is the **rank**.
    - **Non-pivot columns** are the leftovers, each one is just a mix of earlier columns and shows up as a free choice when you solve $A\mathbf{x}=\mathbf{0}$. How many there are is the size of the **solution space**.

    The theorem is simply the observation that every column lands in exactly one pile, so the two counts always add back up to the total number of columns:

    $$\underbrace{\operatorname{rank}(A)}_{\text{new directions}} + \underbrace{\dim(\ker A)}_{\text{free choices}} = \underbrace{n}_{\text{columns}}.$$

    For these $4\times 3$ matrices: $2$ pulling their weight $+\ 1$ leftover $=\ 3$ columns. Handy check: once you know the rank, the other number is free.

!!! note "What \"basis = the pivot columns\" really means"
    Row operations **change** the columns, so you can never copy the basis straight out of the RREF. What row reduction *does* preserve is the dependency pattern, telling you **which** columns are independent. So: reduce to spot the pivot positions (here columns $1$ and $2$), then go back and take those columns from the **original** matrix. For $A_1$ that is $(1,1,2,1)$ and $(0,-2,1,0)$, the untouched first two columns.

---

## 2.15 · Subspaces $F, G \subseteq \mathbb{R}^3$ and their intersection

!!! theory "Topics & Definitions"
    - **Subspace** — a subset that contains $\mathbf{0}$ and is closed under addition and scalar multiplication.
    - **Intersection $F \cap G$** — all vectors lying in both subspaces at once.
    - **Basis of a plane** — solve the defining equation for one variable, then split the free variables into separate vectors.
    - **Two routes to $F \cap G$** — substitute $G$'s general form into $F$'s equation (part b), or set a combination of $F$'s basis equal to a combination of $G$'s basis and solve (part c). Both give the same line.

$F = \{(x,y,z)\in\mathbb{R}^3 \mid x+y-z = 0\}$ is a plane through the origin. $G = \{(a-b,\ a+b,\ a-3b)\mid a,b\in\mathbb{R}\}$ is the span of two vectors. Both pass the three subspace tests: they contain the zero vector, and they are closed under addition and scaling (each condition is inherited from the linear form of the definition).

**Part a (subspaces).** For $F$: $0+0-0 = 0$ so $\mathbf{0}\in F$; adding two solutions of $x+y-z=0$ gives another solution; scaling by $c$ gives $c(x+y-z) = 0$. For $G$: choosing $a=b=0$ gives $\mathbf{0}\in G$; sums and scalar multiples keep the same $(a-b,\ a+b,\ a-3b)$ shape. So both are subspaces of $\mathbb{R}^3$.

!!! steps "Part b, intersection without a basis"
    A general vector in $G$ is $(a-b,\ a+b,\ a-3b)$. For it to lie in $F$ it must satisfy $x+y-z=0$:
    $$(a-b)+(a+b)-(a-3b) = a + 3b = 0 \;\Rightarrow\; a = -3b.$$
    Substituting $a=-3b$ back into $G$'s coordinates:
    $$x = -3b-b = -4b,\quad y = -3b+b = -2b,\quad z = -3b-3(-3b) = -6b.$$
    So $F\cap G = \{(-4b,-2b,-6b)\mid b\in\mathbb{R}\} = \{k(2,1,3)\mid k\in\mathbb{R}\}$.

!!! steps "Part c, intersection using bases"
    Basis for $F$: rewrite $x+y-z=0$ as $z=x+y$, so $(x,y,x+y) = x(1,0,1)+y(0,1,1)$, giving $B_F = \{(1,0,1),(0,1,1)\}$.
    Basis for $G$: separate the parameters, $a(1,1,1)+b(-1,1,-3)$, giving $B_G = \{(1,1,1),(-1,1,-3)\}$.
    Set a combination of $B_F$ equal to a combination of $B_G$:
    $$c_1(1,0,1)+c_2(0,1,1) = d_1(1,1,1)+d_2(-1,1,-3).$$
    Matching coordinates gives $c_1 = d_1-d_2$, $c_2 = d_1+d_2$, $c_1+c_2 = d_1-3d_2$. Substituting the first two into the third: $2d_1 = d_1 - 3d_2 \Rightarrow d_1 = -3d_2$. Let $d_2 = t$, so $d_1 = -3t$:
    $$-3t(1,1,1)+t(-1,1,-3) = (-4t,-2t,-6t) = k(2,1,3).$$
    This matches part b exactly.

!!! answer "Answer"
    Both $F$ and $G$ are subspaces of $\mathbb{R}^3$.

    $$F \cap G = \{\,k(2,1,3)\mid k\in\mathbb{R}\,\}$$

    (a one-dimensional line, obtained identically with or without bases).

---

## 2.16 · Are the following mappings linear?

!!! theory "Topics & Definitions"
    - **Linear mapping** — a map $\Phi$ that passes two tests for all inputs $f,g$ and scalars $c$.
    - **Additivity (plus test)** — $\Phi(f+g) = \Phi(f) + \Phi(g)$.
    - **Homogeneity (scalar test)** — $\Phi(c\cdot f) = c\cdot\Phi(f)$.
    - **To disprove linearity** — a single counterexample that breaks either test is enough.

A map is linear exactly when it respects addition and scaling. Integration and differentiation both do (they split across plus signs and let constants slide out), so parts a and b are linear. Cosine does not (it bends its input), so part c fails. Any fixed-matrix map is automatically linear, so parts d and e pass, including the rotation matrix in e where the sines and cosines are just constants.

!!! steps "Parts a & b, integration and differentiation"
    **a) Integration** $\Phi(f) = \int_a^b f(x)\,dx$.
    Additivity: $\int_a^b (f+g)\,dx = \int_a^b f\,dx + \int_a^b g\,dx = \Phi(f)+\Phi(g)$.
    Homogeneity: $\int_a^b c\,f\,dx = c\int_a^b f\,dx = c\,\Phi(f)$. Linear.

    **b) Differentiation** $\Phi(f) = f'$.
    Additivity: $(f+g)' = f' + g' = \Phi(f)+\Phi(g)$.
    Homogeneity: $(c\,f)' = c\,f' = c\,\Phi(f)$. Linear.

!!! steps "Part c, cosine (counterexample)"
    $\Phi(x) = \cos(x)$. Test additivity: $\Phi(x+y) = \cos(x+y)$, but $\Phi(x)+\Phi(y) = \cos(x)+\cos(y)$, and $\cos(x+y)\neq\cos(x)+\cos(y)$ in general.
    Concrete counterexample with $x=y=0$: $\Phi(0+0) = \cos 0 = 1$, while $\Phi(0)+\Phi(0) = 1+1 = 2$. Since $1\neq 2$, it is **not linear**.

!!! steps "Parts d & e, matrix maps"
    **d)** $\Phi(\mathbf{x}) = A\mathbf{x}$ with $A = \begin{bmatrix}1&2&3\\1&4&3\end{bmatrix}$.
    Additivity: $A(\mathbf{x}+\mathbf{y}) = A\mathbf{x}+A\mathbf{y}$. Homogeneity: $A(c\mathbf{x}) = c(A\mathbf{x})$. Linear.

    **e)** $\Phi(\mathbf{x}) = A\mathbf{x}$ with $A = \begin{bmatrix}\cos\theta&\sin\theta\\-\sin\theta&\cos\theta\end{bmatrix}$ for fixed $\theta$.
    The entries are constants, so this is still just matrix multiplication, and the same two properties hold. Linear (this is a rotation matrix).

!!! answer "Answer"
    - **a)** linear (integration)
    - **b)** linear (differentiation)
    - **c)** **not linear** ($\cos(x+y)\neq\cos x+\cos y$; e.g. $x=y=0$ gives $1\neq 2$)
    - **d)** linear (matrix map)
    - **e)** linear (rotation matrix)

!!! note "Linearity: two checkpoints worth memorizing"
    Turn the formal definition into two everyday tests:

    - **The Plus Test** — does splitting the input across a $+$ survive? $\Phi(f+g) = \Phi(f)+\Phi(g)$.
    - **The Multiplier Test** — can a constant slide out to the front? $\Phi(cf) = c\,\Phi(f)$.

    The real trick is *where the variable sits*. If it is trapped **inside** a curvy function like $\cos$, the map bends the input and both tests fail. If the variable only rides on the **outside** (a derivative, an integral, or multiplication by a fixed matrix) the tests pass. A rotation matrix still passes, because its sines and cosines are baked-in constants, not the input.

    Two things that trip people up here: the notation $L^1, C^1, C^0$ is just naming the *space of functions* in play (integrable, once-differentiable, continuous), so "$\Phi:C^1\to C^0,\ \Phi(f)=f'$" is simply differentiation. And integration and differentiation are themselves **linear operators**: a constant multiple slides straight through, which is a separate idea from the mechanical power-rule arithmetic you use to actually evaluate an integral.

---

## 2.17 · Transformation matrix, rank, kernel and image of $\Phi:\mathbb{R}^3\to\mathbb{R}^4$

!!! theory "Topics & Definitions"
    - **Transformation matrix $A_\Phi$** — read the coefficients of $x_1,x_2,x_3$ row by row; column $j$ holds the coefficients of $x_j$.
    - **Rank** — number of pivots after row reduction.
    - **Kernel $\ker(\Phi)$** — all inputs sent to $\mathbf{0}$; $\dim(\ker) = (\text{columns}) - \operatorname{rank}$.
    - **Image $\operatorname{Im}(\Phi)$** — all reachable outputs; $\dim(\operatorname{Im}) = \operatorname{rank}$, spanned by the original pivot columns.

Reading the four output rows gives the coefficient matrix $A_\Phi$. Row-reducing it produces a pivot in all three columns, so the rank is $3$. By rank–nullity the kernel is trivial ($3-3 = 0$), meaning only the zero vector maps to zero, and the image is three-dimensional, spanned by the three original columns.

!!! steps "Build $A_\Phi$ and row-reduce"
    Pull the coefficients out of $\Phi(x_1,x_2,x_3) = (3x_1+2x_2+x_3,\ x_1+x_2+x_3,\ x_1-3x_2,\ 2x_1+3x_2+x_3)$:
    $$A_\Phi = \begin{bmatrix}3&2&1\\1&1&1\\1&-3&0\\2&3&1\end{bmatrix}.$$
    Swap to get a leading $1$, then clear below:
    $$\begin{bmatrix}1&1&1\\3&2&1\\1&-3&0\\2&3&1\end{bmatrix}
    \longrightarrow
    \begin{bmatrix}1&1&1\\0&1&2\\0&0&1\\0&0&0\end{bmatrix}.$$
    Three pivots, so $\operatorname{rk}(A_\Phi) = 3$.

!!! answer "Answer"
    $$A_\Phi = \begin{bmatrix}3&2&1\\1&1&1\\1&-3&0\\2&3&1\end{bmatrix},\qquad \operatorname{rk}(A_\Phi) = 3.$$

    $\ker(\Phi) = \{\mathbf{0}\}$, so $\dim(\ker(\Phi)) = 0$.

    $\dim(\operatorname{Im}(\Phi)) = 3$, with
    $$\operatorname{Im}(\Phi) = \operatorname{span}\left\{\begin{pmatrix}3\\1\\1\\2\end{pmatrix},\begin{pmatrix}2\\1\\-3\\3\end{pmatrix},\begin{pmatrix}1\\1\\0\\1\end{pmatrix}\right\}.$$

!!! note "Transformation matrix, kernel, image: what they actually are"
    - **Transformation matrix** — the map's **action machine**: feed in $\mathbf{x}$, get $\Phi(\mathbf{x})$. It is *not* an inverse or "undo" matrix. You build it by pulling each variable's coefficients into a column, one output row at a time.
    - **Kernel** — the "drops to zero" club: the inputs the map sends to $\mathbf{0}$. Full rank means only $\mathbf{0}$ qualifies, so $\dim(\ker)=0$. Rank–nullity hands it to you for free: $(\text{columns}) - \operatorname{rank}$.
    - **Image** — the full list of outputs the machine can actually produce. Its dimension always equals the **rank**, and it is spanned by the **original** pivot columns.

---

## 2.18 · Automorphisms: kernels and images of $f$ and $g$

!!! theory "Topics & Definitions"
    - **Homomorphism** — a structure-preserving map between vector spaces; equivalently, a linear map (it preserves addition and scalar multiplication).
    - **Endomorphism** — a homomorphism from a space to itself, $\Phi: V \to V$.
    - **Automorphism** — a bijective endomorphism: an invertible linear map $V \to V$ whose inverse is also linear.
    - **Kernel** — $\ker(f) = \{v : f(v) = \mathbf{0}\}$. **Image** — $\operatorname{Im}(g) = \{g(v) : v \in V\}$.
    - **Key fact used here** — $f$ and $g$ are automorphisms with $f \circ g = \mathrm{id}$, so both are bijections; a bijection sends only $\mathbf{0}$ to $\mathbf{0}$ and is onto.

Because $f \circ g = \mathrm{id}_E$, both $f$ and $g$ are invertible (automorphisms). Bijectivity is what makes all three claims fall out: an injective map has trivial kernel, and a surjective map has full image.

!!! steps "The three claims"
    **1. $\ker(f) = \ker(g \circ f)$.**
    If $f(v) = \mathbf{0}$ then $(g\circ f)(v) = g(\mathbf{0}) = \mathbf{0}$, so $\ker(f) \subseteq \ker(g\circ f)$. Conversely, if $(g\circ f)(v) = \mathbf{0}$, apply $g^{-1}$: $f(v) = g^{-1}(\mathbf{0}) = \mathbf{0}$, so $\ker(g\circ f) \subseteq \ker(f)$. Hence equal.

    **2. $\operatorname{Im}(g) = \operatorname{Im}(g \circ f)$.**
    Clearly $\operatorname{Im}(g\circ f) \subseteq \operatorname{Im}(g)$. For the reverse, take any $g(w) \in \operatorname{Im}(g)$. Since $f$ is surjective, $w = f(u)$ for some $u$, so $g(w) = (g\circ f)(u) \in \operatorname{Im}(g\circ f)$. Hence equal.

    **3. $\ker(f) \cap \operatorname{Im}(g) = \{\mathbf{0}\}$.**
    $f$ is an automorphism, so $\ker(f) = \{\mathbf{0}\}$. The intersection of $\{\mathbf{0}\}$ with any set is $\{\mathbf{0}\}$.

!!! answer "Answer"
    All three hold: $\ker(f) = \ker(g\circ f)$, $\operatorname{Im}(g) = \operatorname{Im}(g\circ f)$, and $\ker(f)\cap\operatorname{Im}(g) = \{\mathbf{0}\}$, each following from $f$ and $g$ being automorphisms (bijective linear maps).

---

## 2.19 · Endomorphism on $\mathbb{R}^3$: kernel, image, and a basis change

!!! theory "Topics & Definitions"
    - **Endomorphism** — a linear map from a space to itself, here $\Phi:\mathbb{R}^3\to\mathbb{R}^3$.
    - **Kernel / Image** — inputs sent to $\mathbf{0}$ / all reachable outputs.
    - **Invertibility test** — $\det A_\Phi \neq 0$ means full rank, trivial kernel, and image equal to all of $\mathbb{R}^3$.
    - **Basis change of a map** — $\tilde{A}_\Phi = B^{-1} A_\Phi B$, where $B$ has the new basis vectors as its columns.

The transformation matrix is $A_\Phi = \begin{bmatrix}1&1&0\\1&-1&0\\1&1&1\end{bmatrix}$. Its determinant is $-2$, which is nonzero, so $\Phi$ is invertible: the kernel is just the zero vector and the image is all of $\mathbb{R}^3$. Part b re-expresses the same map in the new basis $B$ using the similarity formula $B^{-1}A_\Phi B$.

!!! steps "Part a, kernel and image"
    $\det A_\Phi = -2 \neq 0$, so $\operatorname{rk}(A_\Phi) = 3$.
    $$\ker(\Phi) = \{\mathbf{0}\}, \qquad \dim(\ker(\Phi)) = 0.$$
    $$\operatorname{Im}(\Phi) = \mathbb{R}^3, \qquad \dim(\operatorname{Im}(\Phi)) = 3.$$

!!! steps "Part b, basis change to $B$"
    Put the new basis vectors as columns: $B = \begin{bmatrix}1&1&1\\1&2&0\\1&1&0\end{bmatrix}$.
    Then
    $$\tilde{A}_\Phi = B^{-1} A_\Phi B = \begin{bmatrix}6&9&1\\-3&-5&0\\-1&-1&0\end{bmatrix}.$$

!!! answer "Answer"
    **a)** $\ker(\Phi) = \{\mathbf{0}\}$ (dim 0), $\operatorname{Im}(\Phi) = \mathbb{R}^3$ (dim 3).

    **b)** $\displaystyle \tilde{A}_\Phi = \begin{bmatrix}6&9&1\\-3&-5&0\\-1&-1&0\end{bmatrix}.$

---

## 2.20 · Basis changes and a homomorphism $\mathbb{R}^2 \to \mathbb{R}^3$

!!! theory "Topics & Definitions"
    - **Ordered basis** — a basis with a fixed order, so coordinates are well defined.
    - **Change-of-basis matrix** — converts a coordinate vector from one basis to another; its columns are the old basis vectors written in the new basis.
    - **Transformation matrix w.r.t. bases $B, C$** — its $j$-th column is $\Phi(b_j)$ written in coordinates of $C$.
    - **Similarity for different in/out bases** — if input coords change by $P_1$ and output coords by $P_2$, then $A' = P_2\, A_\Phi\, P_1$.
    - **Basis test** — a set of $n$ vectors in $\mathbb{R}^n$ is a basis iff the matrix with them as columns has nonzero determinant.

The vectors $b_1,b_2$ and $b_1',b_2'$ each form a basis of $\mathbb{R}^2$ (nonzero determinants). $P_1$ rewrites $B'$-coordinates as $B$-coordinates. The three $c$ vectors form a basis of $\mathbb{R}^3$, and $P_2$ converts $C$-coordinates to the standard basis. The homomorphism $\Phi$ is pinned down by its action on $b_1+b_2$ and $b_1-b_2$; solving recovers $\Phi(b_1)$ and $\Phi(b_2)$, which build $A_\Phi$. Combining the change-of-basis matrices gives $A'$, and part f chases one vector through both routes as a check.

!!! steps "Parts a & b, bases and $P_1$"
    $\det[b_1\ b_2] = \det\begin{bmatrix}2&-1\\1&-1\end{bmatrix} = -1 \neq 0$, and $\det[b_1'\ b_2'] = \det\begin{bmatrix}2&1\\-2&1\end{bmatrix} = 4 \neq 0$. Both are bases.
    $P_1$ changes coordinates from $B'$ to $B$: $[x]_B = P_1 [x]_{B'}$, so $P_1 = [b_1\ b_2]^{-1}[b_1'\ b_2']$:
    $$P_1 = \begin{bmatrix}4&0\\6&-1\end{bmatrix}.$$

!!! steps "Part c, the basis $C$ and $P_2$"
    $C = [c_1\ c_2\ c_3] = \begin{bmatrix}1&0&1\\2&-1&0\\-1&2&-1\end{bmatrix}$.
    (i) $\det C = 4 \neq 0$, so $C$ is a basis of $\mathbb{R}^3$.
    (ii) $C'$ is the standard basis. Since $v = C[v]_C = [v]_{C'}$, the change from $C$ to $C'$ is just $P_2 = C$.

!!! steps "Part d, transformation matrix $A_\Phi$ w.r.t. $B$ and $C$"
    Given $\Phi(b_1+b_2) = c_2 + c_3$ and $\Phi(b_1-b_2) = 2c_1 - c_2 + 3c_3$. In $C$-coordinates these are $(0,1,1)$ and $(2,-1,3)$. Solving:
    $$\Phi(b_1) = \tfrac12\big[(0,1,1)+(2,-1,3)\big] = (1,0,2)_C, \quad \Phi(b_2) = \tfrac12\big[(0,1,1)-(2,-1,3)\big] = (-1,1,-1)_C.$$
    The columns of $A_\Phi$ are these coordinate vectors:
    $$A_\Phi = \begin{bmatrix}1&-1\\0&1\\2&-1\end{bmatrix}.$$

!!! steps "Part e, $A'$ w.r.t. $B'$ and $C'$"
    Input coords change by $P_1$ ($B' \to B$) and output coords by $P_2$ ($C \to C'$), so
    $$A' = P_2\, A_\Phi\, P_1 = \begin{bmatrix}0&2\\-10&3\\12&-4\end{bmatrix}.$$

!!! steps "Part f, chasing $x$ with coords $[2,3]^\top$ in $B'$"
    (i) $[x]_B = P_1[x]_{B'} = \begin{bmatrix}4&0\\6&-1\end{bmatrix}\begin{bmatrix}2\\3\end{bmatrix} = (8,9)$.
    (ii) $[\Phi(x)]_C = A_\Phi[x]_B = (-1,9,7)$.
    (iii) In the standard basis, $\Phi(x) = C[\Phi(x)]_C = (6,-11,12)$.
    (iv) Directly, $A'[x]_{B'} = (6,-11,12)$, which matches (iii). Check confirmed.

!!! answer "Answer"
    **a)** Both $B$ and $B'$ are bases ($\det = -1$ and $4$).

    **b)** $P_1 = \begin{bmatrix}4&0\\6&-1\end{bmatrix}$.

    **c)** $C$ is a basis ($\det C = 4$); $P_2 = C = \begin{bmatrix}1&0&1\\2&-1&0\\-1&2&-1\end{bmatrix}$.

    **d)** $A_\Phi = \begin{bmatrix}1&-1\\0&1\\2&-1\end{bmatrix}$.

    **e)** $A' = \begin{bmatrix}0&2\\-10&3\\12&-4\end{bmatrix}$.

    **f)** $[x]_B = (8,9)$; $[\Phi(x)]_C = (-1,9,7)$; $\Phi(x) = (6,-11,12)$ in the standard basis, confirmed both ways.

!!! note "The standard basis is secretly the identity"
    When a question asks for coordinates or a matrix "relative to the standard basis $C'$" without ever defining $C'$, that is because the standard basis change-of-basis matrix is just the identity $I = \begin{bmatrix}1&0&0\\0&1&0\\0&0&1\end{bmatrix}$. So any $I^{-1}$ hiding in the chain collapses to $I$, and there is no matrix to invert at that step. Ordinary coordinates *are* the standard-basis coordinates.

!!! note "Reading a change-of-basis chain (right to left)"
    Compose from the inside out: $A' = P_2\, A_\Phi\, P_1$ reads as "convert the input basis with $P_1$, apply the map with $A_\Phi$, then convert the output basis with $P_2$." The inner dimensions dovetail, $(3\times 3)(3\times 2)(2\times 2)$, which is the fast sanity check that the pieces are in the right order.

    - The rule $(\text{destination})^{-1}(\text{start})$ still holds; it just vanishes when the destination is the standard basis, since that inverse is $I$.
    - **Always verify at the end.** Computing $A'\,[x]_{B'}$ directly should land on the *exact* same vector as the long route (change basis, apply the map, change basis back). If they disagree, re-check the arithmetic one entry at a time, because a single sign slip in a dot product, for example $(-4)(2)+(3)(3) = +1$, not $-2$, shifts the whole output vector even when the method is flawless.
