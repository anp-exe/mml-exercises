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
