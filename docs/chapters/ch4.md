# Chapter 4 · Matrix Decompositions

End-of-chapter exercises. Each has a definitions box, explanation, worked steps, and the answer.

---

## 4.1 · Determinant via Laplace and Sarrus

Compute the determinant of
$$A = \begin{pmatrix}1&3&5\\2&4&6\\0&2&4\end{pmatrix}$$
using the Laplace expansion (along the first row) and Sarrus' rule.

!!! theory "Topics & Definitions"
    - **Laplace expansion** — pick any row or column; for each entry delete its row and column to form the minor, take that minor's determinant, multiply by the entry, attach a checkerboard sign, and sum: $\det(A) = \sum_{k=1}^{n} (-1)^{j+k}\, a_{jk}\, \det(A_{j,k})$.
    - **Checkerboard signs** — for a $3\times3$ they are $\begin{pmatrix}+&-&+\\-&+&-\\+&-&+\end{pmatrix}$. A zero entry contributes a zero term, so its minor never needs computing. Expand along the row or column with the most zeros; every line gives the same answer, so pick the laziest one.
    - **Sarrus' rule** — a $3\times3$-only shortcut: copy the first two columns to the right, add the three down-right ($\searrow$) diagonal products, and subtract the three up-right ($\nearrow$) ones. Does not generalise beyond $3\times3$.
    - **Zero determinant** — the columns are linearly dependent, the parallelepiped they span is squashed flat (zero volume), and $A$ is not invertible (singular).

Both methods must land on the same number, so computing it two ways is a built-in cross-check. Laplace along row 1 uses the signs $+, -, +$; Sarrus reads six diagonal products.

!!! steps "Method 1, Laplace along the first row"
    Row 1 is $(1, 3, 5)$ with signs $+, -, +$ from the checkerboard.

    **Entry $a_{11} = 1$, sign $+$.** Delete row 1 and column 1:
    $$\det\begin{pmatrix}4&6\\2&4\end{pmatrix} = 16 - 12 = 4.$$

    **Entry $a_{12} = 3$, sign $-$.** Delete row 1 and column 2:
    $$\det\begin{pmatrix}2&6\\0&4\end{pmatrix} = 8 - 0 = 8.$$

    **Entry $a_{13} = 5$, sign $+$.** Delete row 1 and column 3:
    $$\det\begin{pmatrix}2&4\\0&2\end{pmatrix} = 4 - 0 = 4.$$

    Assemble:
    $$\det(A) = +(1)(4) - (3)(8) + (5)(4) = 4 - 24 + 20 = 0.$$

!!! note "Common slip"
    The alternating $+, -, +$ on the first row is where most sign errors happen. Dropping the minus on the middle term would give $4 + 24 + 20 = 48$ instead of $0$.

!!! steps "Method 2, Sarrus' rule"
    Copy the first two columns to the right:
    $$\begin{array}{ccc|cc}1&3&5&1&3\\2&4&6&2&4\\0&2&4&0&2\end{array}$$

    Down-right diagonals ($\searrow$), added:
    $$1\cdot4\cdot4 = 16, \qquad 3\cdot6\cdot0 = 0, \qquad 5\cdot2\cdot2 = 20 \;\Longrightarrow\; 36.$$

    Up-right diagonals ($\nearrow$), subtracted:
    $$0\cdot4\cdot5 = 0, \qquad 2\cdot6\cdot1 = 12, \qquad 4\cdot2\cdot3 = 24 \;\Longrightarrow\; 36.$$

    $$\det(A) = 36 - 36 = 0.$$

!!! answer "Answer"
    $$\det(A) = 0.$$

    Both methods agree, a useful cross-check whenever two independent routes are available. A zero determinant means $A$ is **singular**: its columns are linearly dependent, the parallelepiped they span has collapsed to zero volume, and $A^{-1}$ does not exist. This exercise is quietly a "spot the singular matrix" question, not just an arithmetic drill.

---

## 4.2 · Computing a $5\times5$ determinant efficiently

Compute the determinant of
$$A = \begin{pmatrix}2&0&1&2&0\\2&-1&0&1&1\\0&1&2&1&2\\-2&0&2&-1&2\\2&0&0&1&1\end{pmatrix}$$
efficiently.

!!! theory "Topics & Definitions"
    - **"Efficiently" is the whole exercise** — a naive Laplace expansion of a $5\times5$ spawns five $4\times4$ minors, each spawning four $3\times3$s, that is $20$ sub-determinants. Done well, this needs the real computation of just one $4\times4$.
    - **Expand along the most zeros** — every zero entry gives a zero term, so its minor never needs building. Any row or column gives the same answer, so pick the laziest one.
    - **Identical rows or columns force $\det = 0$** — they are linearly dependent, so the spanned parallelepiped collapses to zero volume. Skip the expansion entirely. A row or column of all zeros does the same.
    - **Track signs as three factors** — when the entry multiplying a minor is itself negative, the double negative is an easy place to lose a sign. Keep $(\text{sign}) \times (\text{entry}) \times (\text{minor})$ as three separate pieces.

Before expanding anything, look at the matrix. Find the line with the most zeros to expand along, and watch for duplicate rows or columns that zero a minor for free. Here both tricks apply, so almost no arithmetic is needed.

!!! steps "Step 1, count the zeros"
    | Column | Entries | Zeros |
    |:------:|:-------:|:-----:|
    | 1 | $2, 2, 0, -2, 2$ | 1 |
    | 2 | $0, -1, 1, 0, 0$ | 3 ⭐ |
    | 3 | $1, 0, 2, 2, 0$ | 2 |
    | 4 | $2, 1, 1, -1, 1$ | 0 |
    | 5 | $0, 1, 2, 2, 1$ | 1 |

    **Column 2 wins.** Only two of its five entries are nonzero: $-1$ at row 2 and $1$ at row 3. Three terms die immediately, leaving just **two** $4\times4$ minors instead of five.

!!! steps "Step 2, the two surviving minors"
    **Entry $a_{22} = -1$**, sign $(-1)^{2+2} = +1$. Delete row 2 and column 2:
    $$M_1 = \begin{pmatrix}2&1&2&0\\0&2&1&2\\-2&2&-1&2\\2&0&1&1\end{pmatrix}, \qquad \det(M_1) = -6.$$

    **Entry $a_{32} = 1$**, sign $(-1)^{3+2} = -1$. Delete row 3 and column 2:
    $$M_2 = \begin{pmatrix}2&1&2&0\\2&0&1&1\\-2&2&-1&2\\2&0&1&1\end{pmatrix}.$$

!!! note "Free win, do not expand this one"
    **Rows 2 and 4 of $M_2$ are identical** ($2, 0, 1, 1$ both times). Identical rows force $\det(M_2) = 0$ with no computation at all. Spotting this saves an entire $4\times4$ expansion.

!!! steps "Step 3, assemble"
    $$\det(A) = \underbrace{(+1)(-1)(-6)}_{\text{entry } a_{22}} \;+\; \underbrace{(-1)(1)(0)}_{\text{entry } a_{32}} = 6 + 0 = 6.$$
    Note the first term: the entry is $-1$ and the minor is $-6$, so the two negatives cancel to give $+6$.

!!! answer "Answer"
    $$\det(A) = 6.$$

    **What made it efficient.** The naive route is $20$ sub-determinants. Here column 2's three zeros cut five minors down to two, $M_2$'s duplicate rows made it zero for free, and only one $4\times4$ ever needed real work. The exercise tests strategy, not arithmetic: scan for zeros and duplicate lines before computing anything, the single highest-leverage move in the whole determinants topic.

---

## 4.3 · Computing eigenspaces

Compute the eigenspaces of
$$\text{(a)}\quad A := \begin{pmatrix}1&0\\1&1\end{pmatrix}, \qquad \text{(b)}\quad B := \begin{pmatrix}-2&2\\2&1\end{pmatrix}.$$

!!! theory "Topics & Definitions"
    - **Eigenvalue equation** — $\lambda$ is an eigenvalue of $A$ if $Av = \lambda v$ for some nonzero $v$. Rearranged, $(A - \lambda I)v = 0$, which needs $A - \lambda I$ singular, so $\det(A - \lambda I) = 0$. That is the characteristic polynomial, and its roots are exactly the eigenvalues.
    - **Workflow** — form $A - \lambda I$ (subtract $\lambda$ down the diagonal), compute its determinant, set it to zero and solve for the eigenvalues, then for each $\lambda$ separately solve $(A - \lambda I)v = 0$ for its eigenspace. Each eigenvalue gets its own system and its own answer; they are never combined.
    - **Free variables are the point** — when solving $(A - \lambda I)v = 0$ the rows always go redundant (that is exactly why $\lambda$ was chosen), so a row reducing to $0 = 0$ constrains nothing and gets crossed out. The unconstrained variable spans the eigenspace. Careful: $0v_1 + 0v_2 = 0$ says nothing about $v_2$; multiplying by zero destroys the information, so it cannot "see" the variable at all.
    - **Scaling is free** — $(1,3)$, $(2,6)$, and $(-1,-3)$ all span the same line, so pick the cleanest integer representative.
    - **Two multiplicities** — the algebraic multiplicity is how many times $\lambda$ is a root; the geometric multiplicity is the dimension of its eigenspace. They need not match, and you have to solve the system to find out.

The recipe is the same for both matrices: build the characteristic polynomial, find its roots, then solve a separate singular system for each root. Part a lands on one repeated eigenvalue; part b on two distinct ones.

!!! steps "Part a, characteristic polynomial"
    $$A - \lambda I = \begin{pmatrix}1-\lambda & 0\\1 & 1-\lambda\end{pmatrix}.$$

    $$\det(A - \lambda I) = (1-\lambda)(1-\lambda) - (0)(1) = (1-\lambda)^2 = \lambda^2 - 2\lambda + 1.$$

    Setting to zero, $(\lambda - 1)^2 = 0 \Rightarrow \lambda = 1$: a single eigenvalue, but a repeated root, so algebraic multiplicity $2$.

!!! steps "Part a, eigenspace for $\lambda = 1$"
    Substitute $\lambda = 1$:
    $$A - I = \begin{pmatrix}0 & 0\\1 & 0\end{pmatrix}.$$
    Reading $(A - I)v = 0$ row by row: row 1 is $0v_1 + 0v_2 = 0$, no information, discard; row 2 is $v_1 = 0$. So $v_1 = 0$ and $v_2$ is free:
    $$v = \begin{pmatrix}0\\v_2\end{pmatrix} = v_2\begin{pmatrix}0\\1\end{pmatrix}.$$
    Check: $A\begin{pmatrix}0\\1\end{pmatrix} = \begin{pmatrix}0\\1\end{pmatrix} = 1\cdot\begin{pmatrix}0\\1\end{pmatrix}$. $\checkmark$

!!! steps "Part b, characteristic polynomial"
    $$B - \lambda I = \begin{pmatrix}-2-\lambda & 2\\2 & 1-\lambda\end{pmatrix}.$$

    $$\det(B - \lambda I) = (-2-\lambda)(1-\lambda) - (2)(2) = \lambda^2 + \lambda - 6.$$

    Factorising (two numbers multiplying to $-6$ and summing to $+1$, namely $-2$ and $3$):
    $$\lambda^2 + \lambda - 6 = (\lambda - 2)(\lambda + 3) = 0 \Rightarrow \lambda = 2 \ \text{and}\ \lambda = -3.$$
    Two distinct eigenvalues, so two separate eigenspaces.

!!! steps "Part b, eigenspace for $\lambda = 2$"
    $$B - 2I = \begin{pmatrix}-4 & 2\\2 & -1\end{pmatrix}.$$
    Row 1: $-4v_1 + 2v_2 = 0 \Rightarrow v_2 = 2v_1$. Row 2: $2v_1 - v_2 = 0 \Rightarrow v_2 = 2v_1$ (the same information, as expected). Taking $v_1 = 1$:
    $$E_2 = \operatorname{span}\left\{\begin{pmatrix}1\\2\end{pmatrix}\right\}.$$
    Check: $B\begin{pmatrix}1\\2\end{pmatrix} = \begin{pmatrix}2\\4\end{pmatrix} = 2\begin{pmatrix}1\\2\end{pmatrix}$. $\checkmark$

!!! steps "Part b, eigenspace for $\lambda = -3$"
    $$B + 3I = \begin{pmatrix}1 & 2\\2 & 4\end{pmatrix}.$$
    Row 1: $v_1 + 2v_2 = 0 \Rightarrow v_1 = -2v_2$. Row 2: $2v_1 + 4v_2 = 0 \Rightarrow v_1 = -2v_2$ (redundant, as expected). Taking $v_2 = 1$:
    $$E_{-3} = \operatorname{span}\left\{\begin{pmatrix}-2\\1\end{pmatrix}\right\}.$$
    Check: $B\begin{pmatrix}-2\\1\end{pmatrix} = \begin{pmatrix}6\\-3\end{pmatrix} = -3\begin{pmatrix}-2\\1\end{pmatrix}$. $\checkmark$

!!! answer "Answer"
    **a)** One eigenvalue $\lambda = 1$, with a one-dimensional eigenspace:
    $$E_1 = \operatorname{span}\left\{\begin{pmatrix}0\\1\end{pmatrix}\right\}.$$

    **b)** Two eigenvalues, each with a one-dimensional eigenspace:
    $$E_2 = \operatorname{span}\left\{\begin{pmatrix}1\\2\end{pmatrix}\right\}, \qquad E_{-3} = \operatorname{span}\left\{\begin{pmatrix}-2\\1\end{pmatrix}\right\}.$$

    **Part a is defective.** The eigenvalue $\lambda = 1$ has algebraic multiplicity $2$ but geometric multiplicity $1$: a $2\times2$ matrix yielding only one independent eigenvector direction. Geometrically $A$ is a shear, leaving the $y$-axis fixed but tilting everything else, so only one line survives unchanged. Such a matrix is not diagonalisable.

    **Part b's eigenvectors are orthogonal.** $(1,2)\cdot(-2,1) = -2 + 2 = 0$. This is not luck: $B$ is symmetric, and symmetric matrices always have orthogonal eigenvectors for distinct eigenvalues.

---

## 4.4 · Eigenspaces of a $4\times4$ (a defective matrix)

Compute all eigenspaces of
$$A = \begin{pmatrix}0&-1&1&1\\-1&1&-2&3\\2&-1&0&0\\1&-1&1&0\end{pmatrix}.$$

!!! theory "Topics & Definitions"
    - **Same method, just bigger** — form $A - \lambda I$ and compute $\det(A - \lambda I)$ (the characteristic polynomial), factorise and set to zero for the eigenvalues, then for **each** eigenvalue solve $(A - \lambda I)v = 0$ by row reduction for its eigenspace.
    - **Two free sanity checks** — before factorising, verify the coefficient of $\lambda^{n-1}$ equals $-\operatorname{tr}(A)$ and the constant term equals $\det(A)$. Here $\operatorname{tr}(A) = 1$ and $\det(A) = 2$, so the $\lambda^3$ coefficient must be $-1$ and the constant must be $2$. A mismatch means a slip upstream, catch it before wasting effort factorising.
    - **Reading an eigenspace off an RREF** — a column with a leading $1$ is a pivot, so that variable is pinned; a column with no leading $1$ is free and spans the eigenspace. A non-leading entry (a stray $-1$, say) does not make a column a pivot.
    - **Algebraic vs geometric multiplicity** — algebraic is how many times $\lambda$ is a root; geometric is the dimension of the eigenspace, i.e. the number of free variables. When geometric $<$ algebraic the matrix is **defective** and cannot be diagonalised.

The size jumps to $4\times4$ but nothing conceptual changes. The one thing to watch is the repeated root: an eigenvalue can appear twice in the polynomial yet still hand back only a single eigenvector direction.

!!! steps "Step 1, characteristic polynomial"
    Expanding $\det(A - \lambda I)$ by Laplace along column 4 (its zero entry kills one term, leaving three minors):
    $$p_A(\lambda) = \lambda^4 - \lambda^3 - 3\lambda^2 + \lambda + 2.$$
    Check: the $\lambda^3$ coefficient is $-1 = -\operatorname{tr}(A)$ $\checkmark$, and the constant is $2 = \det(A)$ $\checkmark$.

!!! steps "Step 2, factorise"
    By the rational root test the candidates are $\pm1, \pm2$. Testing $\lambda = 1$ gives zero, so $(\lambda - 1)$ is a factor; dividing out and repeating:
    $$p_A(\lambda) = (\lambda + 1)^2 (\lambda - 1)(\lambda - 2).$$
    Eigenvalues: $\lambda = -1$ (algebraic multiplicity $2$), $\lambda = 1$, $\lambda = 2$. Multiplicities sum to $4$ $\checkmark$.

!!! steps "Step 3, eigenspace for $\lambda = 2$"
    Row-reduce $A - 2I$; one free variable remains, giving
    $$E_2 = \operatorname{span}\left\{\begin{pmatrix}1\\0\\1\\1\end{pmatrix}\right\}.$$
    Check: $A(1,0,1,1)^\top = (2,0,2,2)^\top = 2(1,0,1,1)^\top$. $\checkmark$

!!! steps "Step 4, eigenspace for $\lambda = 1$"
    Row-reduce $A - I$; one free variable:
    $$E_1 = \operatorname{span}\left\{\begin{pmatrix}1\\1\\1\\1\end{pmatrix}\right\}.$$
    Check: $A(1,1,1,1)^\top = (1,1,1,1)^\top = 1\cdot(1,1,1,1)^\top$. $\checkmark$

!!! steps "Step 5, eigenspace for $\lambda = -1$"
    Row-reduce $A + I$. The RREF is
    $$\begin{pmatrix}1&0&0&0\\0&1&-1&0\\0&0&0&1\\0&0&0&0\end{pmatrix}.$$
    Pivots sit in columns 1, 2, 4, so only column 3 is free, a single free variable. Reading the rows: $v_1 = 0$, $v_2 = v_3$, $v_4 = 0$. Hence
    $$E_{-1} = \operatorname{span}\left\{\begin{pmatrix}0\\1\\1\\0\end{pmatrix}\right\}.$$
    Check: $A(0,1,1,0)^\top = (0,-1,-1,0)^\top = -1\cdot(0,1,1,0)^\top$. $\checkmark$ Despite $\lambda = -1$ having algebraic multiplicity $2$, its eigenspace is only $1$-dimensional.

!!! answer "Answer"
    $$E_{-1} = \operatorname{span}\left\{\begin{pmatrix}0\\1\\1\\0\end{pmatrix}\right\}, \quad E_{1} = \operatorname{span}\left\{\begin{pmatrix}1\\1\\1\\1\end{pmatrix}\right\}, \quad E_{2} = \operatorname{span}\left\{\begin{pmatrix}1\\0\\1\\1\end{pmatrix}\right\}.$$

    **This matrix is defective.** The eigenvalue $\lambda = -1$ has algebraic multiplicity $2$ but geometric multiplicity $1$. The geometric multiplicities sum to $1 + 1 + 1 = 3$, short of the matrix size $4$, so there are not enough independent eigenvectors to form a basis: $A$ is **not diagonalisable**.

---

## 4.5 · Diagonalizability vs invertibility

Diagonalizability of a matrix is unrelated to its invertibility. Determine for the following four matrices whether they are diagonalizable and/or invertible:
$$\begin{pmatrix}1&0\\0&1\end{pmatrix}, \quad \begin{pmatrix}1&0\\0&0\end{pmatrix}, \quad \begin{pmatrix}1&1\\0&1\end{pmatrix}, \quad \begin{pmatrix}0&1\\0&0\end{pmatrix}.$$

!!! theory "Topics & Definitions"
    - **The point** — diagonalizability and invertibility are independent. A matrix can have either, both, or neither, because they are checked by completely different criteria.
    - **Invertible** — asks whether the map loses information: invertible $\iff \det(A) \neq 0 \iff$ no eigenvalue equals $0$. A zero eigenvalue crushes a direction to nothing, which cannot be undone.
    - **Diagonalizable** — asks whether there are enough independent eigenvectors to span the space, i.e. for every eigenvalue the geometric multiplicity equals the algebraic multiplicity. When they fall short, the matrix is **defective** and not diagonalizable.
    - **Why they are unrelated** — invertibility asks "is any eigenvalue zero?"; diagonalizability asks "are there enough eigenvectors?". Different questions, so all four yes/no combinations can occur, which is exactly what these matrices show.

!!! note "Triangular shortcut"
    For a triangular matrix the eigenvalues are just the diagonal entries. All four matrices here are triangular, so their eigenvalues can be read straight off.

!!! steps "Matrix 1, the identity"
    $$\begin{pmatrix}1&0\\0&1\end{pmatrix}.$$
    Eigenvalues $1, 1$ (from the diagonal). Neither is zero, so $\det = 1 \neq 0$: **invertible**. Every vector satisfies $Iv = v$, so the whole plane is the eigenspace for $\lambda = 1$: geometric multiplicity $2$ matches algebraic multiplicity $2$, so **diagonalizable** (it is already diagonal).

!!! steps "Matrix 2, a projection"
    $$\begin{pmatrix}1&0\\0&0\end{pmatrix}.$$
    Eigenvalues $1, 0$. One eigenvalue is zero, so $\det = 0$: **not invertible**. Two distinct eigenvalues in a $2\times2$ always give two independent eigenvectors (here $(1,0)$ and $(0,1)$), which span the space, so **diagonalizable** (already diagonal).

!!! steps "Matrix 3, a shear"
    $$\begin{pmatrix}1&1\\0&1\end{pmatrix}.$$
    Eigenvalues $1, 1$. Neither is zero, so $\det = 1 \neq 0$: **invertible**. Solving $(A - I)v = 0$ gives only the single direction $(1,0)$: algebraic multiplicity $2$ but geometric multiplicity $1$. Not enough eigenvectors, so **not diagonalizable** (defective).

!!! steps "Matrix 4, a nilpotent shear"
    $$\begin{pmatrix}0&1\\0&0\end{pmatrix}.$$
    Eigenvalues $0, 0$. Zero is an eigenvalue, so $\det = 0$: **not invertible**. Solving $(A - 0I)v = 0$ gives only $(1,0)$: algebraic multiplicity $2$ but geometric multiplicity $1$, so **not diagonalizable** (defective).

!!! answer "Answer"
    | Matrix | Invertible | Diagonalizable |
    |:------:|:----------:|:--------------:|
    | $\begin{pmatrix}1&0\\0&1\end{pmatrix}$ | Yes | Yes |
    | $\begin{pmatrix}1&0\\0&0\end{pmatrix}$ | No | Yes |
    | $\begin{pmatrix}1&1\\0&1\end{pmatrix}$ | Yes | No |
    | $\begin{pmatrix}0&1\\0&0\end{pmatrix}$ | No | No |

    All four combinations appear, confirming the two properties are **completely independent**: invertibility depends on whether any eigenvalue is zero, diagonalizability on whether there are enough independent eigenvectors.

---

## 4.6 · Eigenspaces and diagonalizability

Compute the eigenspaces of the following transformation matrices and decide whether they are diagonalizable.

!!! theory "Topics & Definitions"
    - **Diagonalizability test** — an $n \times n$ matrix is diagonalizable if and only if it has $n$ linearly independent eigenvectors, enough to form a basis.
    - **The multiplicity condition** — equivalently, for **every** eigenvalue the geometric multiplicity (dimension of its eigenspace) must equal its algebraic multiplicity (how many times it is a root). A single mismatch makes the whole matrix **not diagonalizable** (defective).
    - **Symmetry is a red herring** — symmetric matrices are always diagonalizable, but the converse is false: plenty of non-symmetric matrices diagonalize fine. So $A^\top \neq A$ tells you nothing; the deciding factor is always the eigenvector count.
    - **A zero eigenvalue is fine** — $\det(A - \lambda I) = 0$ is exactly the condition that makes $\lambda$ an eigenvalue. If that happens at $\lambda = 0$ (a vanishing constant term), zero is simply an eigenvalue: the matrix is singular but may still diagonalize.
    - **Quick check** — add up the geometric multiplicities. If they sum to $n$, the matrix is diagonalizable; if they fall short, it is not.

### Part a

$$A = \begin{pmatrix}2&3&0\\1&4&3\\0&0&1\end{pmatrix}.$$

Find the eigenvalues, compute each eigenspace, then tally the geometric multiplicities. The repeated eigenvalue is where the surprise lives: it can be a double root yet contribute only a single eigenvector direction.

!!! steps "Step 1, characteristic polynomial"
    Expanding $\det(A - \lambda I)$:
    $$p_A(\lambda) = -(\lambda - 5)(\lambda - 1)^2.$$
    Eigenvalues: $\lambda = 5$ (algebraic multiplicity $1$) and $\lambda = 1$ (algebraic multiplicity $2$). Sanity check: sum of eigenvalues $5 + 1 + 1 = 7 = \operatorname{tr}(A)$ $\checkmark$, product $5\cdot1\cdot1 = 5 = \det(A)$ $\checkmark$.

!!! steps "Step 2, eigenspace for $\lambda = 5$"
    Row-reduce $A - 5I$; one free variable gives
    $$E_5 = \operatorname{span}\left\{\begin{pmatrix}1\\1\\0\end{pmatrix}\right\}.$$
    Geometric multiplicity $1$, matching its algebraic multiplicity.

!!! steps "Step 3, eigenspace for $\lambda = 1$"
    Row-reduce $A - I$. Despite $\lambda = 1$ being a repeated root, only one free variable remains:
    $$E_1 = \operatorname{span}\left\{\begin{pmatrix}-3\\1\\0\end{pmatrix}\right\}.$$
    Geometric multiplicity $1$, but algebraic multiplicity $2$: a mismatch.

!!! steps "Step 4, diagonalizable?"
    Count the independent eigenvectors:
    $$\underbrace{1}_{\lambda = 5} + \underbrace{1}_{\lambda = 1} = 2.$$
    A $3\times3$ matrix needs $3$ independent eigenvectors to be diagonalizable. Only $2$ exist, so $A$ is not diagonalizable. The shortfall is at $\lambda = 1$, whose eigenspace is one dimension smaller than its algebraic multiplicity.

!!! answer "Answer"
    $$E_5 = \operatorname{span}\left\{\begin{pmatrix}1\\1\\0\end{pmatrix}\right\}, \qquad E_1 = \operatorname{span}\left\{\begin{pmatrix}-3\\1\\0\end{pmatrix}\right\}.$$

    **Not diagonalizable.** The eigenvalue $\lambda = 1$ has algebraic multiplicity $2$ but geometric multiplicity $1$, so $A$ has only $2$ independent eigenvectors, one short of the $3$ needed for a $3\times3$. The matrix is defective.

### Part b

$$A = \begin{pmatrix}1&1&0&0\\0&0&0&0\\0&0&0&0\\0&0&0&0\end{pmatrix}.$$

Three all-zero rows make $A$ singular, so $\det(A) = 0$ and zero will be an eigenvalue. The interesting question is whether its eigenspace is big enough to make up the full multiplicity.

!!! steps "Step 1, characteristic polynomial"
    Only the top-left entry $1-\lambda$ survives the expansion, times a diagonal minor:
    $$p_A(\lambda) = (1-\lambda)(-\lambda)^3 = \lambda^3(1-\lambda) = \lambda^4 - \lambda^3.$$

!!! note "A vanishing constant term is a signal, not an error"
    When $\det(A - \lambda I)$ has no constant term, it means $\lambda = 0$ is a root, i.e. zero is an eigenvalue. That is different from "there are no eigenvalues." A zero eigenvalue is perfectly valid; it means the matrix crushes some direction to nothing, consistent with $\det(A) = 0$ (not invertible).

!!! steps "Step 2, solve"
    Factorise $\lambda^3(1 - \lambda) = 0$: the factor $\lambda^3$ gives $\lambda = 0$ and $1 - \lambda = 0$ gives $\lambda = 1$. Eigenvalues: $\lambda = 0$ (algebraic multiplicity $3$, from $\lambda^3$) and $\lambda = 1$ (algebraic multiplicity $1$). Four roots total, matching the $4\times4$ size.

!!! steps "Step 3, eigenspace for $\lambda = 0$"
    Solve $Av = 0$ (the null space of $A$). Only the first row constrains anything ($v_1 + v_2 = 0$), leaving three free variables:
    $$E_0 = \operatorname{span}\left\{\begin{pmatrix}-1\\1\\0\\0\end{pmatrix}, \begin{pmatrix}0\\0\\1\\0\end{pmatrix}, \begin{pmatrix}0\\0\\0\\1\end{pmatrix}\right\}.$$
    Geometric multiplicity $3$, matching the algebraic multiplicity.

!!! steps "Step 4, eigenspace for $\lambda = 1$"
    Solve $(A - I)v = 0$; one free variable:
    $$E_1 = \operatorname{span}\left\{\begin{pmatrix}1\\0\\0\\0\end{pmatrix}\right\}.$$

!!! answer "Answer"
    $$E_0 = \operatorname{span}\left\{\begin{pmatrix}-1\\1\\0\\0\end{pmatrix}, \begin{pmatrix}0\\0\\1\\0\end{pmatrix}, \begin{pmatrix}0\\0\\0\\1\end{pmatrix}\right\}, \qquad E_1 = \operatorname{span}\left\{\begin{pmatrix}1\\0\\0\\0\end{pmatrix}\right\}.$$

    **Diagonalizable.** The eigenvectors number $3 + 1 = 4$, enough for a $4\times4$, and both eigenvalues have geometric multiplicity equal to algebraic multiplicity. So $A$ is diagonalizable even though it is singular: diagonalizability and invertibility are independent, and this matrix has a zero eigenvalue yet still diagonalizes.

---

## 4.7 · Diagonal form and eigenbasis

Are the following matrices diagonalizable? If yes, determine their diagonal form and a basis with respect to which the transformation matrix is diagonal. If no, give reasons.

!!! theory "Topics & Definitions"
    - **Diagonalization** — $A$ is diagonalizable if there is a basis of eigenvectors. In that basis $A$ becomes a diagonal matrix $D$ of eigenvalues, and $A = PDP^{-1}$ where the **columns of $P$ are the eigenvectors**, ordered to match the eigenvalues in $D$. The eigenbasis is exactly those columns.
    - **The test** — an $n \times n$ matrix is diagonalizable iff it has $n$ linearly independent eigenvectors, equivalently every eigenvalue's geometric multiplicity equals its algebraic multiplicity.
    - **Real vs complex** — the characteristic polynomial may have no real roots. Over the reals such a matrix is **not diagonalizable** (no real eigenbasis). A negative discriminant is the signal, since it forces complex eigenvalues.
    - **Discriminant check for a $2\times2$** — for $\lambda^2 + b\lambda + c$ the roots are real only if $b^2 - 4c \geq 0$. If it is negative, the eigenvalues are complex and the matrix is not diagonalizable over $\mathbb{R}$.

### Part a

$$A = \begin{pmatrix}0&1\\-8&4\end{pmatrix}.$$

!!! steps "Part a, characteristic polynomial"
    Using the $2\times2$ form $\lambda^2 - \operatorname{tr}(A)\lambda + \det(A)$, with $\operatorname{tr}(A) = 4$ and $\det(A) = (0)(4) - (1)(-8) = 8$:
    $$p_A(\lambda) = \lambda^2 - 4\lambda + 8.$$

!!! steps "Part a, solve"
    The discriminant is $(-4)^2 - 4(8) = 16 - 32 = -16 < 0$. Applying the quadratic formula:
    $$\lambda = \frac{4 \pm \sqrt{-16}}{2} = 2 \pm 2i.$$
    The eigenvalues are complex ($2 + 2i$ and $2 - 2i$).

!!! answer "Answer"
    **Not diagonalizable over $\mathbb{R}$.** The characteristic polynomial $\lambda^2 - 4\lambda + 8$ has no real roots, its eigenvalues $2 \pm 2i$ are complex, so there is no real eigenbasis and no real diagonal form. (Over $\mathbb{C}$ it *is* diagonalizable, since the two complex eigenvalues are distinct, but with respect to a real basis it is not.)

### Part b

$$A = \begin{pmatrix}1&1&1\\1&1&1\\1&1&1\end{pmatrix}.$$

!!! steps "Part b, characteristic polynomial"
    Expanding $\det(A - \lambda I)$ for the all-ones matrix:
    $$p_A(\lambda) = \lambda^2(\lambda - 3) = 0.$$
    Check: $\operatorname{tr}(A) = 3$ matches the eigenvalue sum $0 + 0 + 3$ $\checkmark$, and $\det(A) = 0$ matches the product $\checkmark$. Eigenvalues: $\lambda = 0$ (algebraic multiplicity $2$) and $\lambda = 3$ (algebraic multiplicity $1$).

!!! steps "Part b, eigenspace for $\lambda = 0$"
    Solve $Av = 0$. Every row of $A$ is identical ($v_1 + v_2 + v_3 = 0$), leaving two free variables:
    $$E_0 = \operatorname{span}\left\{\begin{pmatrix}-1\\1\\0\end{pmatrix}, \begin{pmatrix}-1\\0\\1\end{pmatrix}\right\}.$$
    Geometric multiplicity $2$, matching the algebraic multiplicity.

!!! steps "Part b, eigenspace for $\lambda = 3$"
    Solve $(A - 3I)v = 0$; one free variable:
    $$E_3 = \operatorname{span}\left\{\begin{pmatrix}1\\1\\1\end{pmatrix}\right\}.$$

!!! answer "Answer"
    **Diagonalizable.** The eigenvectors number $2 + 1 = 3$, enough for a $3\times3$, and every eigenvalue's geometric multiplicity equals its algebraic multiplicity.

    Diagonal form:
    $$D = \begin{pmatrix}0&0&0\\0&0&0\\0&0&3\end{pmatrix}.$$

    Eigenbasis (columns of $P$, ordered to match $D$):
    $$\left\{\begin{pmatrix}-1\\1\\0\end{pmatrix}, \begin{pmatrix}-1\\0\\1\end{pmatrix}, \begin{pmatrix}1\\1\\1\end{pmatrix}\right\}.$$
    With respect to this basis the transformation is diagonal with entries $0, 0, 3$.
