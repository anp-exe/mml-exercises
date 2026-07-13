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
