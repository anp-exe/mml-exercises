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
