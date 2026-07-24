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
    expressing the derivative purely in terms of the sigmoid's own output. This form is used constantly in machine learning: during backpropagation the forward pass has already computed $f(x)$, so the gradient comes for free with no new exponentials to evaluate.
