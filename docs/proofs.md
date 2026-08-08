# Proofs

A consolidated collection of the proof-based exercises, gathered here for quick revision. Each of these also lives in its own chapter; this page just puts them side by side so you can review the arguments in one place.

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

!!! note "The four group axioms, and what makes a group Abelian"
    A **group** is a set $G$ with one operation $\star$ that obeys four rules. Checking a group means checking these one by one; here every check rides on the factoring $a\star b = (a+1)(b+1) - 1$, which turns $\star$ into ordinary multiplication shifted by $1$.

    1. **Closure** — combining any two members lands you back inside the set. For $\star$: $(a+1)(b+1)-1$ equals $-1$ only if $(a+1)(b+1)=0$, which cannot happen when $a,b\neq -1$. So the result is never the forbidden $-1$, and you stay in $\mathbb{R}\setminus\{-1\}$.
    2. **Associativity** — regrouping does not change the result: $(a\star b)\star c = a\star(b\star c)$. This is inherited from ordinary multiplication of the shifted factors, which is associative.
    3. **Identity** — one special element $e$ leaves everything unchanged: $a\star e = a$ for all $a$. Here $e = 0$, since $(a+1)(0+1)-1 = a$.
    4. **Inverses** — every $a$ has a partner $a^{-1}$ that undoes it, returning the identity: $a\star a^{-1} = e$. Here $a^{-1} = \dfrac{-a}{a+1}$, and it is never $-1$, so it lives in the set too.

    Those four make $G$ a group. It is also **Abelian** (commutative) if one bonus rule holds: $a\star b = b\star a$ for *all* $a,b$. Since $\star$ is built from ordinary multiplication, and multiplication does not care about order, $\star$ commutes, so this is an **Abelian group**. (A group can pass the four axioms yet fail this test, like the matrix group in 2.3, that is a non-Abelian group.)

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

## 3.7 · Projections and their complements

Let $V$ be a vector space and $\pi$ an endomorphism of $V$.

**(a)** Prove that $\pi$ is a projection if and only if $\operatorname{id}_V - \pi$ is a projection, where $\operatorname{id}_V$ is the identity endomorphism on $V$.

**(b)** Assuming $\pi$ is a projection, compute $\operatorname{Im}(\operatorname{id}_V - \pi)$ and $\ker(\operatorname{id}_V - \pi)$ in terms of $\operatorname{Im}(\pi)$ and $\ker(\pi)$.

!!! theory "Topics & Definitions"
    - **Projection $=$ idempotent** — an endomorphism $\pi$ is a projection exactly when $\pi^2 = \pi$. Once you have landed in the target subspace, projecting again does not move you. This single equation drives the whole exercise.
    - **The identity behaves like $1$** — composing with $\operatorname{id}_V$ changes nothing: $\operatorname{id}\circ\pi = \pi$ and $\pi\circ\operatorname{id} = \pi$. This is what lets $(\operatorname{id} - \pi)^2$ expand exactly like ordinary algebra.
    - **What $\operatorname{id} - \pi$ does** — feed it $v$ and you get $v - \pi(v)$: the vector minus its projection, the same **residual** used to compute distances in the earlier exercises.
    - **Proving a set equality** — to show $A = B$, prove both inclusions $A \subseteq B$ and $B \subseteq A$.

Part a is pure algebra: expand $(\operatorname{id} - \pi)^2$ and watch the condition $\pi^2 = \pi$ appear. Part b then chases elements through $\operatorname{id} - \pi$, using $\pi^2 = \pi$ where needed, to show the image and kernel simply swap.

!!! steps "Part a, expand $(\operatorname{id} - \pi)^2$"
    Write $\operatorname{id}$ for $\operatorname{id}_V$. Expanding the composition:

    $$(\operatorname{id} - \pi)^2 = \operatorname{id}\circ\operatorname{id} - \operatorname{id}\circ\pi - \pi\circ\operatorname{id} + \pi\circ\pi = \operatorname{id} - 2\pi + \pi^2.$$

    The two middle terms each collapse to $\pi$, since composing with the identity does nothing.

!!! steps "Part a, chain of equivalences"
    $\operatorname{id} - \pi$ is a projection precisely when it is idempotent:

    $$\begin{aligned}(\operatorname{id} - \pi)^2 = \operatorname{id} - \pi &\iff \operatorname{id} - 2\pi + \pi^2 = \operatorname{id} - \pi\\ &\iff -2\pi + \pi^2 = -\pi\\ &\iff \pi^2 = \pi.\end{aligned}$$

    Every step is reversible (subtract $\operatorname{id}$, then add $2\pi$, to both sides), so the biconditional holds in both directions at once. $\blacksquare$

!!! note "Why both directions come free"
    Because the chain uses $\iff$ rather than $\implies$, reading it top-to-bottom proves one direction and bottom-to-top proves the other. No separate argument is needed.

!!! steps "Part b, $\ker(\operatorname{id} - \pi) = \operatorname{Im}(\pi)$"
    Work directly from the definition of the kernel:

    $$v \in \ker(\operatorname{id}-\pi) \iff (\operatorname{id}-\pi)(v) = 0 \iff v - \pi(v) = 0 \iff v = \pi(v).$$

    The statement $v = \pi(v)$ says that $v$ is an output of $\pi$, which is exactly what it means for $v$ to lie in $\operatorname{Im}(\pi)$. Every step is an equivalence, so

    $$\ker(\operatorname{id}-\pi) = \operatorname{Im}(\pi).$$

    Note this direction does not even require idempotency.

!!! steps "Part b, $\operatorname{Im}(\operatorname{id} - \pi) = \ker(\pi)$"
    **($\subseteq$)** Let $w \in \operatorname{Im}(\operatorname{id} - \pi)$, so $w = v - \pi(v)$ for some $v$. Apply $\pi$:

    $$\pi(w) = \pi(v) - \pi^2(v) = \pi(v) - \pi(v) = 0,$$

    using $\pi^2 = \pi$. So $w \in \ker(\pi)$.

    **($\supseteq$)** Let $w \in \ker(\pi)$, so $\pi(w) = 0$. Then

    $$(\operatorname{id}-\pi)(w) = w - \pi(w) = w - 0 = w,$$

    so $w$ is its own image under $\operatorname{id} - \pi$, hence $w \in \operatorname{Im}(\operatorname{id}-\pi)$.

    Both inclusions hold, so $\operatorname{Im}(\operatorname{id}-\pi) = \ker(\pi)$. $\blacksquare$

!!! answer "Answer"
    **a)** $\pi$ is a projection $\iff \pi^2 = \pi \iff (\operatorname{id}_V - \pi)^2 = \operatorname{id}_V - \pi \iff \operatorname{id}_V - \pi$ is a projection.

    **b)** The image and kernel swap:

    $$\operatorname{Im}(\operatorname{id}_V - \pi) = \ker(\pi), \qquad \ker(\operatorname{id}_V - \pi) = \operatorname{Im}(\pi).$$

    **Intuition.** A projection splits the space as $V = \operatorname{Im}(\pi) \oplus \ker(\pi)$, acting as the identity on the first part and as zero on the second. The complementary map $\operatorname{id}_V - \pi$ keeps the residual instead, so it kills exactly what $\pi$ keeps and keeps exactly what $\pi$ kills. Their images and kernels therefore trade places.

---

## 4.11 · $A^\top A$ and $AA^\top$ share nonzero eigenvalues

Show that for any $A \in \mathbb{R}^{m\times n}$, the matrices $A^\top A$ and $AA^\top$ have the same nonzero eigenvalues.

!!! theory "Topics & Definitions"
    - **Why it matters** — this justifies the SVD shortcut: since $A^\top A$ and $AA^\top$ share nonzero eigenvalues, the singular values $\sqrt{\lambda}$ are the same whichever product you use, so you can diagonalize the smaller one.
    - **The key idea** — if $x$ is an eigenvector of $A^\top A$, then $Ax$ is an eigenvector of $AA^\top$ with the same eigenvalue. Multiplying by $A$ transfers the eigenvalue between the products; $A$ itself is only the bridge.
    - **Why "nonzero" matters** — the argument needs $Ax \neq 0$ to give a genuine eigenvector, which is only guaranteed when $\lambda \neq 0$.

!!! steps "Proof"
    Let $\lambda \neq 0$ be an eigenvalue of $A^\top A$ with eigenvector $x \neq 0$:

    $$A^\top A\, x = \lambda x.$$

    Multiply on the left by $A$:

    $$A A^\top A\, x = \lambda A x.$$

    Regroup using associativity:

    $$(AA^\top)(Ax) = \lambda (Ax).$$

    This has the form of an eigenvalue equation for $AA^\top$, with eigenvector $Ax$ and eigenvalue $\lambda$.

    **Check $Ax \neq 0$:** if $Ax = 0$, then $A^\top A\, x = A^\top(Ax) = 0 = \lambda x$, forcing $\lambda = 0$ (since $x \neq 0$), contradicting $\lambda \neq 0$. So $Ax$ is a genuine eigenvector. The reverse direction is identical, swapping $A$ and $A^\top$ (start from $AA^\top y = \lambda y$ and multiply by $A^\top$).

!!! answer "Conclusion"
    Every nonzero eigenvalue of $A^\top A$ is a nonzero eigenvalue of $AA^\top$, and vice versa, so the two matrices share exactly the same nonzero eigenvalues. $\blacksquare$

    (They may differ in their *zero* eigenvalues: the larger matrix simply has extra zeros to fill its extra dimensions, which is why singular values come only from the nonzero eigenvalues.)

---

## 4.12 · The largest singular value is the maximum stretch

Show that for $x \neq 0$,

$$\max_{x} \frac{\lVert Ax\rVert_2}{\lVert x\rVert_2} = \sigma_1,$$

where $\sigma_1$ is the largest singular value of $A \in \mathbb{R}^{m\times n}$.

!!! theory "Topics & Definitions"
    - **The stretch factor** — $\lVert Ax\rVert / \lVert x\rVert$ measures how much $A$ lengthens $x$. This theorem says the most $A$ can stretch any vector is exactly $\sigma_1$, giving the largest singular value a concrete meaning: the matrix's maximum amplification.
    - **Orthogonal matrices preserve length** — $\lVert Uz\rVert = \lVert z\rVert$ and $\lVert Vz\rVert = \lVert z\rVert$, which lets you strip $U$ and $V$ from $A = U\Sigma V^\top$ and reduce the problem to the diagonal $\Sigma$.
    - **$\sigma_1$ is the largest** — so every $\sigma_i^2 \le \sigma_1^2$, which bounds the sum.
    - **Proving a maximum** — needs two parts: an upper bound (nothing exceeds $\sigma_1$) and attainment (some vector reaches it).

!!! steps "Step 1, reduce to the diagonal matrix"
    Write $A = U\Sigma V^\top$. For $x \neq 0$, set $y = V^\top x$; since $V$ is orthogonal, $\lVert y\rVert = \lVert x\rVert$. Using that $U$ preserves length:

    $$\lVert Ax\rVert = \lVert U\Sigma V^\top x\rVert = \lVert \Sigma V^\top x\rVert = \lVert \Sigma y\rVert.$$

    So $\dfrac{\lVert Ax\rVert}{\lVert x\rVert} = \dfrac{\lVert \Sigma y\rVert}{\lVert y\rVert}$.

!!! steps "Step 2, upper bound"
    Since $\Sigma$ is diagonal, $\Sigma y = (\sigma_1 y_1, \sigma_2 y_2, \dots)$, so

    $$\lVert \Sigma y\rVert^2 = \sum_i \sigma_i^2 y_i^2 \le \sigma_1^2 \sum_i y_i^2 = \sigma_1^2 \lVert y\rVert^2$$

    (each $\sigma_i^2$ replaced by the larger $\sigma_1^2$). Taking square roots:

    $$\frac{\lVert Ax\rVert}{\lVert x\rVert} \le \sigma_1 \quad\text{for all } x.$$

!!! steps "Step 3, the bound is attained"
    Choose $x = v_1$, the first right-singular vector. Then $y = V^\top v_1 = e_1 = (1,0,\dots,0)$, so

    $$\lVert \Sigma y\rVert = \sigma_1, \qquad \lVert y\rVert = 1, \qquad \frac{\lVert Av_1\rVert}{\lVert v_1\rVert} = \sigma_1.$$

    Some vector reaches $\sigma_1$, so the bound is tight.

!!! answer "Conclusion"
    The ratio is bounded above by $\sigma_1$ for every $x$ and equals $\sigma_1$ when $x = v_1$, so

    $$\max_{x \neq 0} \frac{\lVert Ax\rVert_2}{\lVert x\rVert_2} = \sigma_1. \qquad \blacksquare$$

    The maximum stretch of $A$ is its largest singular value, achieved along the first right-singular vector $v_1$.

---
