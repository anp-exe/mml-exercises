# Chapter 5 · Vector Calculus

End-of-chapter exercises. Each has a definitions box, explanation, worked steps, and the answer.

---

## 5.1 · Differentiating a product with nested functions

*Calculus I · differentiation rules*

Compute the derivative $f'(x)$ for
$$f(x) = \log(x^4)\sin(x^3).$$

!!! theory "Topics & Definitions"
    Read the structure of the expression *before* differentiating. Ask, in order:

    | What you see | Rule to use | Form |
    |:-------------|:------------|:-----|
    | Two things **multiplied** | product rule | $(uv)' = u'v + uv'$ |
    | Two things **divided** | quotient rule | $\left(\tfrac{u}{v}\right)' = \tfrac{u'v - uv'}{v^2}$ |
    | A function **inside** another | chain rule | $\big(g(h(x))\big)' = g'(h(x))\cdot h'(x)$ |
    | Terms **added or subtracted** | differentiate each separately | $(u+v)' = u' + v'$ |

    Here $\log(x^4)\sin(x^3)$ is two things *multiplied*, so the product rule applies at the top level. Each factor then has something *inside* it ($x^4$ in the log, $x^3$ in the sin), so the chain rule applies within each factor. Rules nest: identify the outermost structure first, then work inward.

    A handy log simplification: $\log(x^n) = n\log(x)$, so $\log(x^4) = 4\log(x)$ and its derivative is immediately $4/x$. The chain rule gives the same thing: $\tfrac{1}{x^4}\cdot 4x^3 = \tfrac{4x^3}{x^4} = \tfrac{4}{x}$.

!!! note "The two most common slips"
    **Do not multiply the derivatives.** The product rule is $u'v + uv'$, two terms *added*, not $u'v'$.

    **The inner derivative goes outside.** For $\sin(x^3)$ the chain rule gives $\cos(x^3)\cdot 3x^2$: the $3x^2$ multiplies from outside, and the inside of the cosine stays $x^3$. Writing $\cos(3x^2)$ is wrong, the inside never changes.

!!! steps "Step 1, identify the structure"
    The expression is a product of two factors:
    $$u = \log(x^4), \qquad v = \sin(x^3).$$
    So the top-level rule is the product rule, $f' = u'v + uv'$, and each factor then needs the chain rule.

!!! steps "Step 2, differentiate $u = \log(x^4)$"
    Chain rule: $\tfrac{d}{dx}\log(\text{inside}) = \tfrac{1}{\text{inside}}\cdot(\text{inside})'$.
    $$u' = \frac{1}{x^4}\cdot 4x^3 = \frac{4x^3}{x^4} = \frac{4}{x}.$$
    The $4x^3$ lands on the numerator, then $x^3/x^4$ simplifies to $1/x$.

!!! steps "Step 3, differentiate $v = \sin(x^3)$"
    Chain rule: $\tfrac{d}{dx}\sin(\text{inside}) = \cos(\text{inside})\cdot(\text{inside})'$.
    $$v' = \cos(x^3)\cdot 3x^2 = 3x^2\cos(x^3).$$
    The inside of the cosine stays $x^3$; the $3x^2$ multiplies from outside.

!!! steps "Step 4, assemble with the product rule"
    $$f' = u'v + uv' = \frac{4}{x}\sin(x^3) + \log(x^4)\cdot 3x^2\cos(x^3).$$

!!! answer "Answer"
    $$f'(x) = \frac{4\sin(x^3)}{x} + 3x^2\log(x^4)\cos(x^3).$$

    Two terms, added, one from differentiating each factor while holding the other fixed. Both terms needed the chain rule internally, which is why the exercise combines the two rules.

---

## 5.2 · Derivative of the logistic sigmoid

*Calculus I · differentiation rules*

Compute the derivative $f'(x)$ of the logistic sigmoid
$$f(x) = \frac{1}{1 + \exp(-x)}.$$

!!! theory "Topics & Definitions"
    - **Structure first** — this is one thing divided by another, so the quotient rule applies: $\left(\tfrac{u}{v}\right)' = \tfrac{u'v - uv'}{v^2}$.
    - **Constant numerator** — here $u = 1$ and $v = 1 + \exp(-x)$. Since $u' = 0$, the first term of the quotient rule vanishes entirely and only $-uv'/v^2$ survives. Spotting that early saves work.
    - **The denominator needs the chain rule** — $\tfrac{d}{dx}\exp(\text{inside}) = \exp(\text{inside})\cdot(\text{inside})'$. With inside $-x$ (derivative $-1$), $\tfrac{d}{dx}\exp(-x) = -\exp(-x)$.
    - **Alternative route** — rewriting $f(x) = (1 + \exp(-x))^{-1}$ turns this into a pure chain-rule exercise (outer $(\cdot)^{-1}$, inner $1 + \exp(-x)$) and gives the same answer.

!!! note "Common slip"
    In $v^2$, square the **whole denominator** $v = 1 + \exp(-x)$, not its derivative. Writing $(-\exp(-x))^2$ squares $v'$ by mistake.

!!! steps "Step 1, identify $u$ and $v$"
    $$u = 1, \qquad v = 1 + \exp(-x),$$
    so $u' = 0$ and, by the chain rule, $v' = -\exp(-x)$.

!!! steps "Step 2, apply the quotient rule"
    $$f'(x) = \frac{u'v - uv'}{v^2} = \frac{0\cdot(1+\exp(-x)) - 1\cdot(-\exp(-x))}{(1+\exp(-x))^2}.$$
    The first term is zero, and the double negative in the second becomes positive:
    $$f'(x) = \frac{\exp(-x)}{(1+\exp(-x))^2}.$$

!!! answer "Answer"
    $$f'(x) = \frac{\exp(-x)}{\left(1+\exp(-x)\right)^2}.$$

    **A useful rearrangement.** This is equivalent to
    $$f'(x) = f(x)\big(1 - f(x)\big),$$
    expressing the derivative purely in terms of the sigmoid's own output.

!!! note "Where this shows up: backpropagation"
    When a sigmoid is used as a neuron's activation, training the network needs its derivative at every step. Backpropagation works backwards through the layers multiplying by local derivatives (the chain rule again), and the sigmoid's local derivative is exactly $f(x)\big(1 - f(x)\big)$. Because the forward pass already stored the output $f(x)$, the gradient costs just one subtraction and one multiplication, with no new $\exp$ to evaluate. That reuse is a big part of why the sigmoid was such a popular activation.

---

## 5.3 · Derivative of the Gaussian

*Calculus I · differentiation rules*

Compute the derivative $f'(x)$ of
$$f(x) = \exp\!\left(-\frac{1}{2\sigma^2}(x-\mu)^2\right),$$
where $\mu, \sigma$ are constants.

!!! theory "Topics & Definitions"
    - **What is constant here** — we differentiate with respect to $x$, so everything that is not $x$ is held fixed. Both $\mu$ (the mean) and $\sigma$ (the standard deviation) are fixed, so $\tfrac{1}{2\sigma^2}$ is just a constant multiplier and $\tfrac{d}{dx}(-\mu) = 0$.
    - **The chain rule applies twice** — the outermost function is $\exp(\cdot)$; inside it is $-\tfrac{1}{2\sigma^2}(x-\mu)^2$; inside *that* is $(x-\mu)$. Each layer contributes a factor.
    - **Key pattern** — $\tfrac{d}{dx}\exp(g(x)) = g'(x)\exp(g(x))$: the exponential is reproduced unchanged, multiplied by the derivative of its exponent. The exponent itself never changes.

!!! note "A fraction does not automatically mean the quotient rule"
    The quotient rule applies to $\tfrac{u}{v}$ where **both** parts are functions of $x$. Here $2\sigma^2$ contains no $x$ at all, so $-\tfrac{1}{2\sigma^2}(x-\mu)^2$ is simply *(constant) $\times$ (function)*: differentiate the function and carry the constant along. Likewise, when multiplying a fraction by a term, only the numerator is affected:
    $$-\frac{1}{2\sigma^2}\times 2(x-\mu) = \frac{-2(x-\mu)}{2\sigma^2},$$
    the denominator is untouched, because the second factor has denominator $1$.

!!! steps "Step 1, differentiate the exponent"
    Let $g(x) = -\dfrac{1}{2\sigma^2}(x-\mu)^2$. The constant $-\tfrac{1}{2\sigma^2}$ comes along for the ride; apply the power rule to $(x-\mu)^2$:
    $$\frac{d}{dx}(x-\mu)^2 = 2(x-\mu)\cdot\frac{d}{dx}(x-\mu) = 2(x-\mu)\cdot 1 = 2(x-\mu).$$
    The innermost chain-rule factor is $1$ (since $\mu$ is constant), so it is invisible here, but it is still a chain-rule step, and it is $1$, not $0$.

!!! steps "Step 2, combine the constant"
    $$g'(x) = -\frac{1}{2\sigma^2}\times 2(x-\mu) = \frac{-2(x-\mu)}{2\sigma^2} = -\frac{x-\mu}{\sigma^2}.$$
    Only the $2$s cancel; the $\sigma^2$ stays in the denominator and the minus sign survives.

!!! steps "Step 3, apply the outer chain rule"
    $$f'(x) = g'(x)\,\exp(g(x)),$$
    substituting $g'(x)$ from Step 2 and leaving the exponent unchanged.

!!! answer "Answer"
    $$f'(x) = -\frac{x-\mu}{\sigma^2}\exp\!\left(-\frac{1}{2\sigma^2}(x-\mu)^2\right).$$

    **Sanity check on the shape.** The derivative is zero exactly when $x = \mu$, the peak of the bell curve where the slope is flat. For $x > \mu$ the factor $-(x-\mu)$ is negative, so the curve is descending; for $x < \mu$ it is positive, so the curve is ascending. This matches the familiar Gaussian shape.

---

## 5.4 · Taylor polynomials of $\sin(x) + \cos(x)$

*Calculus II · Taylor series*

Compute the Taylor polynomials $T_n$ for $n = 0, \dots, 5$ of
$$f(x) = \sin(x) + \cos(x)$$
at $x_0 = 0$.

!!! theory "Topics & Definitions"
    - **The Taylor polynomial** — of degree $n$ about $x_0$ is $T_n(x) = \sum_{k=0}^{n} \dfrac{f^{(k)}(x_0)}{k!}\,(x-x_0)^k$. At $x_0 = 0$ (a Maclaurin polynomial) this simplifies to $\sum \tfrac{f^{(k)}(0)}{k!}x^k$, since $(x-0)^k = x^k$.
    - **Sine and cosine derivatives cycle with period four** — $\sin \to \cos \to -\sin \to -\cos \to \sin \to \dots$. Once you have four derivatives, the pattern repeats, which makes this much shorter than it looks.
    - **Lower-order polynomials are truncations** — $T_3$ is just $T_5$ with the last two terms removed, so computing $T_5$ gives you all of them at once.

!!! note "Read $f^{(k)}(x_0)$ carefully"
    $f^{(k)}(x_0)$ means "the $k$-th derivative, **evaluated at** $x_0$", not the derivative multiplied by $x_0$. Even when $x_0 = 0$ these values are generally nonzero: here $f(0) = \sin 0 + \cos 0 = 1$. Order of operations matters: differentiate first, substitute afterwards.

!!! steps "Step 1, the derivatives and their values at $0$"
    | $k$ | $f^{(k)}(x)$ | $f^{(k)}(0)$ |
    |:---:|:------------:|:------------:|
    | 0 | $\sin x + \cos x$ | $1$ |
    | 1 | $\cos x - \sin x$ | $1$ |
    | 2 | $-\sin x - \cos x$ | $-1$ |
    | 3 | $-\cos x + \sin x$ | $-1$ |
    | 4 | $\sin x + \cos x$ | $1$ |
    | 5 | $\cos x - \sin x$ | $1$ |

    At $k = 4$ the function returns to itself, confirming the period-four cycle. The values at $0$ follow the repeating pattern $1, 1, -1, -1, 1, 1, \dots$.

!!! steps "Step 2, assemble the coefficients"
    Divide each value by $k!$:
    $$\frac{1}{0!} = 1,\quad \frac{1}{1!} = 1,\quad \frac{-1}{2!} = -\frac12,\quad \frac{-1}{3!} = -\frac16,\quad \frac{1}{4!} = \frac{1}{24},\quad \frac{1}{5!} = \frac{1}{120}.$$

!!! answer "Answer"
    $$\begin{aligned}
    T_0(x) &= 1\\
    T_1(x) &= 1 + x\\
    T_2(x) &= 1 + x - \tfrac{1}{2}x^2\\
    T_3(x) &= 1 + x - \tfrac{1}{2}x^2 - \tfrac{1}{6}x^3\\
    T_4(x) &= 1 + x - \tfrac{1}{2}x^2 - \tfrac{1}{6}x^3 + \tfrac{1}{24}x^4\\
    T_5(x) &= 1 + x - \tfrac{1}{2}x^2 - \tfrac{1}{6}x^3 + \tfrac{1}{24}x^4 + \tfrac{1}{120}x^5
    \end{aligned}$$

    The sign pattern $+\,+\,-\,-\,+\,+$ mirrors the four-step derivative cycle and is a useful check that the derivatives were tracked correctly.

---

## 5.5 · Jacobian dimensions

*Calculus III · multivariable derivatives*

Consider the functions
$$\begin{aligned}
f_1(\boldsymbol{x}) &= \sin(x_1)\cos(x_2), && \boldsymbol{x} \in \mathbb{R}^2\\
f_2(\boldsymbol{x}, \boldsymbol{y}) &= \boldsymbol{x}^\top \boldsymbol{y}, && \boldsymbol{x}, \boldsymbol{y} \in \mathbb{R}^n\\
f_3(x) &= x x^\top, && x \in \mathbb{R}
\end{aligned}$$

**Part a**

What are the dimensions of $\partial f_i / \partial \boldsymbol{x}$?

!!! theory "Topics & Definitions"
    - **The dimension rule** — for $f : \mathbb{R}^n \to \mathbb{R}^m$, the Jacobian $\partial f/\partial \boldsymbol{x}$ has dimension $m \times n$, that is (output dimension) $\times$ (input dimension). Each **row** is one output component, each **column** one input variable. This part can be answered purely by reading the domain and codomain, no differentiation required.
    - **Scalar-valued means a row** — a scalar-valued function ($m = 1$) always has a Jacobian that is a single **row** vector, with one entry per input variable. All three functions here are scalar-valued, so all three Jacobians are rows.

!!! note "Read the space each variable lives in"
    In $f_3$, $x \in \mathbb{R}$ is a **scalar**, not a vector, so $xx^\top$ is simply $x^2$ (a scalar) and the Jacobian is $1\times1$. If $x$ were a column vector in $\mathbb{R}^n$, then $xx^\top$ would be an $n\times n$ matrix and the derivative a very different object. The dimension annotation is doing real work here.

!!! steps "Reading off each function"
    | Function | Input space | Output space | Jacobian dimension |
    |:---------|:-----------:|:------------:|:------------------:|
    | $f_1$ | $\mathbb{R}^2$ | $\mathbb{R}$ | $1 \times 2$ |
    | $f_2$ (w.r.t. $\boldsymbol{x}$) | $\mathbb{R}^n$ | $\mathbb{R}$ | $1 \times n$ |
    | $f_3$ | $\mathbb{R}$ | $\mathbb{R}$ | $1 \times 1$ |

!!! answer "Answer"
    $$\frac{\partial f_1}{\partial \boldsymbol{x}} \in \mathbb{R}^{1\times 2}, \qquad \frac{\partial f_2}{\partial \boldsymbol{x}} \in \mathbb{R}^{1\times n}, \qquad \frac{\partial f_3}{\partial x} \in \mathbb{R}^{1\times 1}.$$

    All three are row vectors, since every function here maps into $\mathbb{R}$, a useful structural check before computing anything.

**Part b**

Compute the Jacobians.

!!! theory "Topics & Definitions"
    - **What a Jacobian is** — all the partial derivatives of a function collected into a matrix, $\left(\tfrac{\partial f}{\partial \boldsymbol{x}}\right)_{ij} = \tfrac{\partial f_i}{\partial x_j}$. Rows are output components, columns are input variables, so entry $(i,j)$ answers "how does output $i$ respond to input $j$?".
    - **Why it exists** — for a single-variable function the derivative is one number (the slope); for several variables you need the rate of change in *every* input direction, and the Jacobian packages them all into one object so it acts as "the derivative" of a vector-valued function.
    - **Scalar-valued collapses to a row** — all three functions here are scalar-valued, so each Jacobian is $\tfrac{\partial f}{\partial \boldsymbol{x}} = \begin{pmatrix}\tfrac{\partial f}{\partial x_1} & \cdots & \tfrac{\partial f}{\partial x_n}\end{pmatrix}$. Once the partials are computed, arranging them in a row *is* the Jacobian.

!!! note "Dot products expand nicely"
    Writing $\boldsymbol{x}^\top\boldsymbol{y} = x_1y_1 + x_2y_2 + \dots + x_ny_n$ makes the differentiation transparent: differentiating with respect to $x_i$, every term without $x_i$ is constant and vanishes, leaving $y_i$.

!!! steps "Jacobian of $f_1$"
    Two partial derivatives, one per input variable, each holding the other constant:
    $$\frac{\partial f_1}{\partial x_1} = \cos(x_1)\cos(x_2), \qquad \frac{\partial f_1}{\partial x_2} = -\sin(x_1)\sin(x_2).$$
    Arranged as a row:
    $$\frac{\partial f_1}{\partial \boldsymbol{x}} = \begin{pmatrix}\cos(x_1)\cos(x_2) & -\sin(x_1)\sin(x_2)\end{pmatrix}.$$
    This is $1\times2$, matching part a.

!!! steps "Jacobian of $f_2$"
    Expand the dot product:
    $$\boldsymbol{x}^\top\boldsymbol{y} = x_1y_1 + x_2y_2 + \dots + x_ny_n.$$
    Differentiating with respect to $x_1$, the terms $x_2y_2, \dots, x_ny_n$ contain no $x_1$ and vanish; the surviving $x_1y_1$ has $y_1$ as a constant multiplier, giving $y_1$. The same for each $x_i$ gives $y_i$. Collecting all $n$ partials:
    $$\frac{\partial f_2}{\partial \boldsymbol{x}} = \begin{pmatrix}y_1 & y_2 & \cdots & y_n\end{pmatrix} = \boldsymbol{y}^\top.$$
    This is $1\times n$, matching part a.

!!! steps "Jacobian of $f_3$"
    Since $x \in \mathbb{R}$ is a scalar, $xx^\top = x^2$, so by the power rule
    $$\frac{\partial f_3}{\partial x} = 2x.$$
    This is $1\times1$, matching part a.

!!! answer "Answer"
    $$\frac{\partial f_1}{\partial \boldsymbol{x}} = \begin{pmatrix}\cos(x_1)\cos(x_2) & -\sin(x_1)\sin(x_2)\end{pmatrix},$$

    $$\frac{\partial f_2}{\partial \boldsymbol{x}} = \boldsymbol{y}^\top, \qquad \frac{\partial f_3}{\partial x} = 2x.$$

    Each result has the dimension predicted in part a, a useful structural check. All three are row vectors because all three functions map into $\mathbb{R}$.

---

## 5.6 · Chain rule with nested functions, and a gradient with respect to a matrix

*Calculus III · multivariable derivatives*

Differentiate $f$ with respect to $t$ and $g$ with respect to $X$, where
$$f(t) = \sin\!\big(\log(t^\top t)\big), \qquad t \in \mathbb{R}^D,$$

$$g(X) = \operatorname{tr}(AXB), \qquad A \in \mathbb{R}^{D\times E},\ X \in \mathbb{R}^{E\times F},\ B \in \mathbb{R}^{F\times D}.$$

**Part a**

!!! theory "Topics & Definitions"
    - **The chain rule** — for nested functions, $\tfrac{d}{dx}g\big(h(x)\big) = g'\big(h(x)\big)\cdot h'(x)$: differentiate the outer function, leave its inside unchanged, then multiply by the derivative of the inside.
    - **Why three times here** — $f(t) = \sin(\log(t^\top t))$ nests three functions, so the chain rule applies three times. The most common slip is letting a lower layer's derivative creep into a higher layer's brackets: the inside of a function never changes when you differentiate it, only new factors appear on the outside.
    - **Differentiating $t^\top t$** — write it in components, $t^\top t = t_1^2 + \dots + t_D^2$. Each partial is a power rule, $\tfrac{\partial}{\partial t_i}(t_1^2 + \dots + t_D^2) = 2t_i$, so collecting all $D$ as a row gives $\tfrac{\partial}{\partial t}(t^\top t) = \begin{pmatrix}2t_1 & \cdots & 2t_D\end{pmatrix} = 2t^\top$.

!!! note "Think of it as peeling layers"
    Picture the expression as an onion with three layers:

    | Layer | What it is |
    |:-----:|:-----------|
    | Outer | $\sin(\,\cdot\,)$ |
    | Middle | $\log(\,\cdot\,)$ |
    | Inner | $t^\top t$ |

    Peel from the outside in: at each layer, differentiate only that layer and leave everything inside it untouched, producing one factor per layer. Then multiply the factors together, and that multiplication *is* the chain rule at work.

!!! steps "Layer 1, peel the sine"
    Differentiate $\sin(\,\cdot\,)$ into $\cos(\,\cdot\,)$, keeping the inside exactly as it was:
    $$\cos\!\big(\log(t^\top t)\big).$$
    The $\log(t^\top t)$ is carried across untouched; nothing from the inner layers has appeared yet.

!!! steps "Layer 2, peel the logarithm"
    The derivative of $\log(u)$ is $\tfrac{1}{u}$, so this layer contributes
    $$\frac{1}{t^\top t}.$$
    Again the inside $t^\top t$ stays as it is.

!!! steps "Layer 3, peel the dot product"
    From the working above, the innermost layer contributes
    $$2t^\top.$$

!!! steps "Multiply the layers together"
    The chain rule joins the three factors by multiplication:
    $$f'(t) = \underbrace{\cos\!\big(\log(t^\top t)\big)}_{\text{layer 1}} \cdot \underbrace{\frac{1}{t^\top t}}_{\text{layer 2}} \cdot \underbrace{2t^\top}_{\text{layer 3}}.$$

!!! answer "Part a answer"
    $$\frac{df}{dt} = \frac{2t^\top \cos\!\big(\log(t^\top t)\big)}{t^\top t} \;\in\; \mathbb{R}^{1\times D}.$$
    Three nested functions, three chain-rule factors, all multiplied. The result is a row vector because $f$ is scalar-valued and $t$ is a vector.

**Part b**

!!! theory "Topics & Definitions"
    - **The trace** — $\operatorname{tr}(M) = M_{11} + M_{22} + \dots + M_{nn}$, the sum of the diagonal entries. To differentiate $\operatorname{tr}(AXB)$ we need its diagonal entries in terms of the entries of $X$.
    - **Dimensions force a square product** — the trace needs a square matrix, and $(D\times E)(E\times F)(F\times D) = D\times D$ $\checkmark$: inner dimensions cancel and both outer ones are $D$. The annotations are what make the trace well defined.
    - **Concrete small matrices** — with general $D,E,F$ the expansion is a triple sum; setting $D=E=F=2$ makes everything $2\times2$ and the trace expands into just eight visible terms, with the same structure as the general case.
    - **Shape of the gradient** — differentiating a *scalar* with respect to a *matrix* gives a gradient in the same shape as $X$ (not a Jacobian row): each partial sits in the position of the entry it came from.

!!! steps "Step 1, set up $2\times2$ matrices"
    Take $D=E=F=2$:
    $$A = \begin{pmatrix}a_{11}&a_{12}\\a_{21}&a_{22}\end{pmatrix}, \quad X = \begin{pmatrix}x_{11}&x_{12}\\x_{21}&x_{22}\end{pmatrix}, \quad B = \begin{pmatrix}b_{11}&b_{12}\\b_{21}&b_{22}\end{pmatrix}.$$
    The product $AXB$ is $2\times2$, so its trace is $(AXB)_{11} + (AXB)_{22}$.

!!! steps "Step 2, expand the trace"
    Multiplying out and summing the two diagonal entries gives eight terms:
    $$\begin{aligned}
    \operatorname{tr}(AXB) =\ & b_{11}a_{11}x_{11} + b_{11}a_{12}x_{21} + b_{12}a_{21}x_{11} + b_{12}a_{22}x_{21}\\
    +\ & b_{21}a_{11}x_{12} + b_{21}a_{12}x_{22} + b_{22}a_{21}x_{12} + b_{22}a_{22}x_{22}.
    \end{aligned}$$
    Every term is linear in exactly one entry of $X$, with a coefficient built from one $a$ and one $b$. That linearity is what makes the differentiation straightforward.

!!! steps "Step 3, take the partial derivatives"
    For each entry of $X$, keep only the terms containing it; the rest are constant and vanish, leaving the coefficient beside it:
    $$\frac{\partial g}{\partial x_{11}} = b_{11}a_{11} + b_{12}a_{21}, \qquad \frac{\partial g}{\partial x_{12}} = b_{21}a_{11} + b_{22}a_{21},$$

    $$\frac{\partial g}{\partial x_{21}} = b_{11}a_{12} + b_{12}a_{22}, \qquad \frac{\partial g}{\partial x_{22}} = b_{21}a_{12} + b_{22}a_{22}.$$
    Across all four partials, each of the eight terms is picked up exactly once.

!!! steps "Step 4, arrange in the shape of $X$"
    $$\frac{\partial g}{\partial X} = \begin{pmatrix}
    b_{11}a_{11} + b_{12}a_{21} & b_{21}a_{11} + b_{22}a_{21}\\
    b_{11}a_{12} + b_{12}a_{22} & b_{21}a_{12} + b_{22}a_{22}
    \end{pmatrix}.$$

!!! answer "Part b answer"
    The four partials arranged in the shape of $X$ are a complete and correct answer. Written compactly,
    $$\frac{\partial g}{\partial X} = (BA)^\top \;\in\; \mathbb{R}^{E\times F}.$$
    Each entry is a row of $B$ dotted with a column of $A$, exactly an entry of $BA$, with the index positions coming out transposed. Recognising this compact form is a convenience rather than a requirement: the expanded four-entry matrix is the same object.

---

## 5.7 · Chain rule with dimensions

*Calculus III · multivariable derivatives*

Compute $df/dx$ for the following functions using the chain rule, giving the dimensions of every partial derivative.

**(a)** $f(z) = \log(1+z)$, where $z = x^\top x$ and $x \in \mathbb{R}^D$.

**(b)** $f(z) = \sin(z)$, where $z = Ax + b$, with $A \in \mathbb{R}^{E \times D}$, $x \in \mathbb{R}^D$, $b \in \mathbb{R}^E$.

!!! theory "Topics & Definitions"
    - **The chain rule in this form** — when $f$ depends on $x$ through an intermediate $z$, $\dfrac{df}{dx} = \dfrac{df}{dz}\cdot\dfrac{dz}{dx}$. Compute each factor separately, then multiply. The factors are matrices in general, so the order matters.
    - **Dimensions of a matrix product** — the inner dimensions must match and cancel, the outer ones survive: $(m\times k)(k\times n) = m\times n$. Inner must match because multiplication dots a row against a column (same length required); outer survive because there is one entry per (row, column) pair.
    - **Overall dimension check** — for $f$ with output in $\mathbb{R}^m$ and input $x \in \mathbb{R}^n$, the final $df/dx$ must be $m\times n$. Verifying this confirms the chain was assembled in the right order.

!!! note "What transforms, and what carries over"
    The layer being differentiated **transforms into its derivative**; whatever sits **inside** it **carries over unchanged**. So differentiating $\log(u)$ turns the log into $1/u$ (it does not survive, being the layer differentiated), while $u$ is untouched. In Exercise 5.6 the log *did* survive inside $\cos(\log(t^\top t))$, but only because it was nested one level below the sine being differentiated: same rule, different position in the stack. Quick check: $\tfrac{d}{dx}\log(x^2) = \tfrac{1}{x^2}\cdot 2x = \tfrac{2}{x}$, agreeing with $\log(x^2) = 2\log x$.

**Part a**

!!! steps "Step 1, outer layer $df/dz$"
    With $f(z) = \log(1+z)$ and inside $u = 1+z$,
    $$\frac{df}{dz} = \frac{1}{1+z} = \frac{1}{1+x^\top x}.$$
    Both $f$ and $z$ are scalars, so this partial is $1\times1$. No logarithm appears: it was the layer being differentiated, so it became a reciprocal.

!!! steps "Step 2, inner layer $dz/dx$"
    Write the dot product in components, $z = x^\top x = x_1^2 + \dots + x_D^2$. Differentiating with respect to $x_i$ leaves $2x_i$, so
    $$\frac{dz}{dx} = \begin{pmatrix}2x_1 & 2x_2 & \cdots & 2x_D\end{pmatrix} = 2x^\top.$$
    A scalar output with $D$ inputs gives dimension $1\times D$.

!!! steps "Step 3, multiply"
    $$\frac{df}{dx} = \frac{df}{dz}\cdot\frac{dz}{dx} = \frac{1}{1+x^\top x}\cdot 2x^\top.$$
    Dimensions: $(1\times1)(1\times D) = 1\times D$.

!!! answer "Part a answer"
    $$\frac{df}{dx} = \frac{2x^\top}{1+x^\top x} \;\in\; \mathbb{R}^{1\times D}.$$

    Dimensions of each partial:
    $$\frac{df}{dz} \in \mathbb{R}^{1\times1}, \qquad \frac{dz}{dx} \in \mathbb{R}^{1\times D}, \qquad \frac{df}{dx} \in \mathbb{R}^{1\times D}.$$
    The final shape is $1\times D$ because $f$ is scalar-valued and $x$ has $D$ components.

**Part b**

!!! steps "Step 1, outer layer $df/dz$"
    Here $z = Ax+b \in \mathbb{R}^E$, so $f = \sin(z) \in \mathbb{R}^E$ with the sine applied elementwise, and the Jacobian is $E\times E$ with entry $(i,j) = \partial f_i/\partial z_j$. Since $f_i = \sin(z_i)$ depends on $z_i$ **only**, every off-diagonal entry is zero and the matrix is diagonal:
    $$\frac{df}{dz} = \begin{pmatrix}\cos(z_1) & 0 & \cdots & 0\\ 0 & \cos(z_2) & \cdots & 0\\ \vdots & & \ddots & \vdots\\ 0 & 0 & \cdots & \cos(z_E)\end{pmatrix} = \operatorname{diag}\big(\cos(Ax+b)\big).$$

!!! note "Why diag(...) and not just cos(Ax+b)"
    $\cos(Ax+b)$ is a **vector** of $E$ entries, and a vector cannot be multiplied by the $E\times D$ matrix that follows. The genuine derivative is the $E\times E$ diagonal matrix above; $\operatorname{diag}(\cdot)$ is shorthand for placing those values on the diagonal with zeros elsewhere, which is what makes the next matrix product valid.

!!! steps "Step 2, inner layer $dz/dx$"
    With $z = Ax+b$, the term $b$ is constant and $Ax$ is linear in $x$, so
    $$\frac{dz}{dx} = A \;\in\; \mathbb{R}^{E\times D}.$$

!!! steps "Step 3, multiply"
    $$\frac{df}{dx} = \frac{df}{dz}\cdot\frac{dz}{dx} = \operatorname{diag}\big(\cos(Ax+b)\big)\,A.$$
    Dimensions: $(E\times E)(E\times D) = E\times D$. The inner $E$s match and cancel; the outer $E$ and $D$ survive.

!!! note "Keep the factors separate"
    The $A$ from the inner layer multiplies from **outside**; it does not move into the argument of the cosine, which stays exactly $Ax+b$. Writing something like $\cos(A^2x+b)$ merges two separate chain-rule factors into one and is wrong, in the same way that $\tfrac{d}{dx}\sin(x^3) = 3x^2\cos(x^3)$ keeps $x^3$ inside and puts $3x^2$ outside.

!!! answer "Part b answer"
    $$\frac{df}{dx} = \operatorname{diag}\big(\cos(Ax+b)\big)\,A \;\in\; \mathbb{R}^{E\times D}.$$

    Dimensions of each partial:
    $$\frac{df}{dz} \in \mathbb{R}^{E\times E}, \qquad \frac{dz}{dx} \in \mathbb{R}^{E\times D}, \qquad \frac{df}{dx} \in \mathbb{R}^{E\times D}.$$
    The final shape $E\times D$ matches (output dimension) by (input dimension), since $f \in \mathbb{R}^E$ and $x \in \mathbb{R}^D$.
