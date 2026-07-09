# Chapter 3 · Analytic Geometry

End-of-chapter exercises. Each has a definitions box, explanation, worked steps, and the answer.

---

## 3.1 · Show that $\langle\cdot,\cdot\rangle$ is an inner product

!!! theory "Topics & Definitions"
    - **Inner product** — a map $\langle\cdot,\cdot\rangle$ taking two vectors to a number, passing three tests for all $\mathbf{x},\mathbf{y},\mathbf{z}$ and scalars.
    - **Bilinear** — linear in each slot separately (constants and sums pass straight through).
    - **Symmetric** — order does not matter: $\langle\mathbf{x},\mathbf{y}\rangle = \langle\mathbf{y},\mathbf{x}\rangle$.
    - **Positive definite** — $\langle\mathbf{x},\mathbf{x}\rangle > 0$ for every $\mathbf{x}\neq\mathbf{0}$ (and $0$ only for $\mathbf{0}$).
    - **Matrix shortcut** — any $\langle\mathbf{x},\mathbf{y}\rangle = \mathbf{x}^\top A\,\mathbf{y}$ is automatically bilinear; it is symmetric exactly when $A = A^\top$, and positive definite exactly when $A$ is (leading minors all positive).

The form $\langle\mathbf{x},\mathbf{y}\rangle = x_1y_1 - (x_1y_2 + x_2y_1) + 2x_2y_2$ is a matrix form in disguise. Pulling the coefficients into a grid gives $A = \begin{bmatrix}1&-1\\-1&2\end{bmatrix}$, so $\langle\mathbf{x},\mathbf{y}\rangle = \mathbf{x}^\top A\,\mathbf{y}$. Because it is built as $\mathbf{x}^\top A\mathbf{y}$ it is bilinear for free, and the two remaining checks are just facts about $A$.

!!! steps "Check the three properties"
    **Matrix form.** $\mathbf{x}^\top A\mathbf{y} = (x_1 - x_2)y_1 + (-x_1 + 2x_2)y_2 = x_1y_1 - x_1y_2 - x_2y_1 + 2x_2y_2$, matching the given form.

    **Symmetric.** $A = \begin{bmatrix}1&-1\\-1&2\end{bmatrix} = A^\top$, so $\langle\mathbf{x},\mathbf{y}\rangle = \langle\mathbf{y},\mathbf{x}\rangle$.

    **Positive definite.** Leading principal minors of $A$: the top-left entry $1 > 0$, and $\det A = (1)(2) - (-1)(-1) = 1 > 0$. Both positive, so $A$ is positive definite. Equivalently, completing the square,
    $$\langle\mathbf{x},\mathbf{x}\rangle = x_1^2 - 2x_1x_2 + 2x_2^2 = (x_1 - x_2)^2 + x_2^2 \ge 0,$$
    which is $0$ only when $x_1 = x_2 = 0$.

!!! answer "Answer"
    All three properties hold, so $\langle\cdot,\cdot\rangle$ **is an inner product** on $\mathbb{R}^2$ (with matrix $A = \begin{bmatrix}1&-1\\-1&2\end{bmatrix}$).

---

## 3.2 · Is $\langle\mathbf{x},\mathbf{y}\rangle = \mathbf{x}^\top A\,\mathbf{y}$ an inner product?

!!! theory "Topics & Definitions"
    - **Symmetry is required** — every inner product must satisfy $\langle\mathbf{x},\mathbf{y}\rangle = \langle\mathbf{y},\mathbf{x}\rangle$.
    - **Matrix test** — for $\mathbf{x}^\top A\mathbf{y}$, symmetry holds for all vectors **iff** $A = A^\top$.
    - **One counterexample is enough** — to disprove, find a single pair where $\langle\mathbf{x},\mathbf{y}\rangle \neq \langle\mathbf{y},\mathbf{x}\rangle$.

Here $A = \begin{bmatrix}2&0\\1&2\end{bmatrix}$, and $A^\top = \begin{bmatrix}2&1\\0&2\end{bmatrix} \neq A$. Since $A$ is not symmetric, the form should fail the symmetry test, and a single well-chosen pair exposes it.

!!! steps "Counterexample with $\mathbf{x} = (2,0)^\top$, $\mathbf{y} = (0,2)^\top$"
    $$\langle\mathbf{x},\mathbf{y}\rangle = \mathbf{x}^\top A\mathbf{y} = \begin{bmatrix}2&0\end{bmatrix}\begin{bmatrix}2&0\\1&2\end{bmatrix}\begin{bmatrix}0\\2\end{bmatrix} = \begin{bmatrix}2&0\end{bmatrix}\begin{bmatrix}0\\4\end{bmatrix} = 0.$$
    $$\langle\mathbf{y},\mathbf{x}\rangle = \mathbf{y}^\top A\mathbf{x} = \begin{bmatrix}0&2\end{bmatrix}\begin{bmatrix}2&0\\1&2\end{bmatrix}\begin{bmatrix}2\\0\end{bmatrix} = \begin{bmatrix}0&2\end{bmatrix}\begin{bmatrix}4\\2\end{bmatrix} = 4.$$
    Since $0 \neq 4$, the form is not symmetric.

!!! answer "Answer"
    **Not an inner product.** With $\mathbf{x} = (2,0)^\top,\ \mathbf{y} = (0,2)^\top$ we get $\langle\mathbf{x},\mathbf{y}\rangle = 0$ but $\langle\mathbf{y},\mathbf{x}\rangle = 4$, so symmetry fails (because $A \neq A^\top$).

---

## 3.3 · Distance between two vectors

!!! theory "Topics & Definitions"
    - **Induced norm** — an inner product gives a length: $\lVert\mathbf{v}\rVert = \sqrt{\langle\mathbf{v},\mathbf{v}\rangle}$.
    - **Distance** — the length of the difference vector: $d(\mathbf{x},\mathbf{y}) = \lVert\mathbf{x}-\mathbf{y}\rVert = \sqrt{\langle\mathbf{x}-\mathbf{y},\ \mathbf{x}-\mathbf{y}\rangle}$.
    - **Method** — subtract first to get the arrow $\mathbf{x}-\mathbf{y}$, feed that single vector into the inner product, then square-root.
    - **Which inner product matters** — a different inner product (a different matrix $A$) measures a different distance for the same two points.

Distance is just the length of the arrow joining the points. So compute $\mathbf{x}-\mathbf{y}$ once, then take the inner product of that difference with itself and square-root it. With $\mathbf{x} = (1,2,3)^\top$ and $\mathbf{y} = (-1,-1,0)^\top$, the difference is $\mathbf{x}-\mathbf{y} = (2,3,3)^\top$ for both parts; only the inner product changes.

!!! steps "Part a, dot product $\langle\mathbf{x},\mathbf{y}\rangle = \mathbf{x}^\top\mathbf{y}$"
    $$\mathbf{x}-\mathbf{y} = (2,3,3)^\top, \qquad \langle\mathbf{x}-\mathbf{y},\mathbf{x}-\mathbf{y}\rangle = 2^2 + 3^2 + 3^2 = 22.$$
    $$d = \sqrt{22} \approx 4.69.$$

!!! steps "Part b, weighted product $\langle\mathbf{x},\mathbf{y}\rangle = \mathbf{x}^\top A\mathbf{y}$"
    With $A = \begin{bmatrix}2&1&0\\1&3&-1\\0&-1&2\end{bmatrix}$ and $\mathbf{d} = \mathbf{x}-\mathbf{y} = (2,3,3)^\top$, first apply $A$:
    $$A\mathbf{d} = \begin{bmatrix}2&1&0\\1&3&-1\\0&-1&2\end{bmatrix}\begin{bmatrix}2\\3\\3\end{bmatrix} = \begin{bmatrix}7\\8\\3\end{bmatrix},\qquad \mathbf{d}^\top A\mathbf{d} = 2(7)+3(8)+3(3) = 47.$$
    $$d = \sqrt{47} \approx 6.86.$$

!!! answer "Answer"
    **a)** $d = \sqrt{22} \approx 4.69$. &nbsp;&nbsp; **b)** $d = \sqrt{47} \approx 6.86$.

---

## 3.4 · Angle between two vectors

!!! theory "Topics & Definitions"
    - **Angle formula** — $\cos\theta = \dfrac{\langle\mathbf{x},\mathbf{y}\rangle}{\lVert\mathbf{x}\rVert\,\lVert\mathbf{y}\rVert}$, then $\theta = \arccos(\cdots)$.
    - **Work it in pieces** — compute the inner product on top first, then each magnitude $\lVert\mathbf{x}\rVert = \sqrt{\langle\mathbf{x},\mathbf{x}\rangle}$, then combine.
    - **Sign of the cosine** — a negative value means an obtuse angle (more than $90^\circ$).
    - **Different inner product, different angle** — swapping the dot product for $\mathbf{x}^\top B\mathbf{y}$ reshapes what "angle" means.

Build the ratio one piece at a time: the inner product in the numerator, the two lengths in the denominator, then plug into $\arccos$. Here $\mathbf{x} = (1,2)^\top$ and $\mathbf{y} = (-1,-1)^\top$.

!!! steps "Part a, dot product $\langle\mathbf{x},\mathbf{y}\rangle = \mathbf{x}^\top\mathbf{y}$"
    Inner product: $\langle\mathbf{x},\mathbf{y}\rangle = (1)(-1) + (2)(-1) = -3$.
    Magnitudes: $\lVert\mathbf{x}\rVert = \sqrt{1^2+2^2} = \sqrt{5}$, $\lVert\mathbf{y}\rVert = \sqrt{(-1)^2+(-1)^2} = \sqrt{2}$.
    Combine:
    $$\cos\theta = \frac{-3}{\sqrt{5}\,\sqrt{2}} = \frac{-3}{\sqrt{10}} \approx -0.9487 \;\Rightarrow\; \theta \approx 161.57^\circ \approx 2.82\ \text{rad}.$$

!!! steps "Part b, weighted product $\langle\mathbf{x},\mathbf{y}\rangle = \mathbf{x}^\top B\mathbf{y}$"
    With $B = \begin{bmatrix}2&1\\1&3\end{bmatrix}$, take it a piece at a time.
    Inner product: $B\mathbf{y} = \begin{bmatrix}2&1\\1&3\end{bmatrix}\begin{bmatrix}-1\\-1\end{bmatrix} = \begin{bmatrix}-3\\-4\end{bmatrix}$, so $\langle\mathbf{x},\mathbf{y}\rangle = \mathbf{x}^\top B\mathbf{y} = (1)(-3)+(2)(-4) = -11$.
    Magnitudes: $\lVert\mathbf{x}\rVert_B = \sqrt{\mathbf{x}^\top B\mathbf{x}} = \sqrt{18}$, $\lVert\mathbf{y}\rVert_B = \sqrt{\mathbf{y}^\top B\mathbf{y}} = \sqrt{7}$.
    Combine:
    $$\cos\theta = \frac{-11}{\sqrt{18}\,\sqrt{7}} = \frac{-11}{\sqrt{126}} \approx -0.9800 \;\Rightarrow\; \theta \approx 168.51^\circ \approx 2.94\ \text{rad}.$$

!!! answer "Answer"
    **a)** $\theta \approx 161.57^\circ \approx 2.82$ rad. &nbsp;&nbsp; **b)** $\theta \approx 168.51^\circ \approx 2.94$ rad.

    Both angles are obtuse (negative cosine); the weighted inner product in b pushes the angle slightly wider.
