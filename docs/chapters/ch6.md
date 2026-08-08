# Chapter 6 · Probability & Distributions

End-of-chapter exercises. Each has a definitions box, explanation, worked steps, and the answer.

---

## 6.1 · Marginal and conditional distributions

Consider the following bivariate distribution $p(x,y)$ of two discrete random variables $X$ and $Y$.

|  | $x_1$ | $x_2$ | $x_3$ | $x_4$ | $x_5$ |
|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
| $y_1$ | 0.01 | 0.02 | 0.03 | 0.1 | 0.1 |
| $y_2$ | 0.05 | 0.1 | 0.05 | 0.07 | 0.2 |
| $y_3$ | 0.1 | 0.05 | 0.03 | 0.05 | 0.04 |

Compute **(a)** the marginal distributions $p(x)$ and $p(y)$, and **(b)** the conditional distributions $p(x \mid Y = y_1)$ and $p(y \mid X = x_3)$.

!!! theory "Topics & Definitions"
    - **Joint distribution** — $p(x_i, y_j)$ gives the probability that $X = x_i$ and $Y = y_j$ occur together. Every cell of the table is one joint probability, and all fifteen cells sum to $1$.
    - **Marginal distribution (sum rule)** — to recover the distribution of one variable alone, sum the joint over every value of the other:

    $$p(x_i) = \sum_{j} p(x_i, y_j), \qquad p(y_j) = \sum_{i} p(x_i, y_j)$$

    Summing over $y$ collapses the table to a single row of $x$ probabilities, and summing over $x$ collapses it to a single column of $y$ probabilities. The table here is already normalised, so a column or row total is the probability directly, with no further division.

    - **Conditional distribution** — conditioning fixes one variable and renormalises the surviving slice so it is a valid distribution again:

    $$p(x \mid Y = y_1) = \frac{p(x, y_1)}{p(y_1)}, \qquad p(y \mid X = x_3) = \frac{p(x_3, y)}{p(x_3)}$$

    Because the divisor is the exact total of the slice, each conditional sums to $1$ by construction. This gives a free correctness check on every conditional computed.

!!! steps "Marginals of $X$ (column sums)"

    $$\begin{aligned}
    p(x_1) &= 0.01 + 0.05 + 0.1 = 0.16\\
    p(x_2) &= 0.02 + 0.1 + 0.05 = 0.17\\
    p(x_3) &= 0.03 + 0.05 + 0.03 = 0.11\\
    p(x_4) &= 0.1 + 0.07 + 0.05 = 0.22\\
    p(x_5) &= 0.1 + 0.2 + 0.04 = 0.34
    \end{aligned}$$

    Check: $0.16 + 0.17 + 0.11 + 0.22 + 0.34 = 1$.

!!! steps "Marginals of $Y$ (row sums)"

    $$\begin{aligned}
    p(y_1) &= 0.01 + 0.02 + 0.03 + 0.1 + 0.1 = 0.26\\
    p(y_2) &= 0.05 + 0.1 + 0.05 + 0.07 + 0.2 = 0.47\\
    p(y_3) &= 0.1 + 0.05 + 0.03 + 0.05 + 0.04 = 0.27
    \end{aligned}$$

    Check: $0.26 + 0.47 + 0.27 = 1$. Both marginals summing to $1$ confirms the joint table is normalised and the arithmetic holds in both directions.

!!! steps "Conditional $p(x \mid Y = y_1)$"
    Fix $Y = y_1$, take that row, divide every entry by $p(y_1) = 0.26$:

    $$\begin{aligned}
    p(x_1 \mid y_1) &= \tfrac{0.01}{0.26} = \tfrac{1}{26} \approx 0.038\\
    p(x_2 \mid y_1) &= \tfrac{0.02}{0.26} = \tfrac{2}{26} = \tfrac{1}{13} \approx 0.077\\
    p(x_3 \mid y_1) &= \tfrac{0.03}{0.26} = \tfrac{3}{26} \approx 0.115\\
    p(x_4 \mid y_1) &= \tfrac{0.1}{0.26} = \tfrac{10}{26} = \tfrac{5}{13} \approx 0.385\\
    p(x_5 \mid y_1) &= \tfrac{0.1}{0.26} = \tfrac{10}{26} = \tfrac{5}{13} \approx 0.385
    \end{aligned}$$

    Check: numerators over the common denominator $26$ give $1 + 2 + 3 + 10 + 10 = 26$, so the conditional sums to $1$.

!!! steps "Conditional $p(y \mid X = x_3)$"
    Fix $X = x_3$, take that column, divide every entry by $p(x_3) = 0.11$:

    $$\begin{aligned}
    p(y_1 \mid x_3) &= \tfrac{0.03}{0.11} = \tfrac{3}{11} \approx 0.273\\
    p(y_2 \mid x_3) &= \tfrac{0.05}{0.11} = \tfrac{5}{11} \approx 0.455\\
    p(y_3 \mid x_3) &= \tfrac{0.03}{0.11} = \tfrac{3}{11} \approx 0.273
    \end{aligned}$$

    Check: $3 + 5 + 3 = 11$, so the conditional sums to $1$.

!!! answer "Answer"
    **a)** Marginal of $X$: $p(x) = (0.16,\ 0.17,\ 0.11,\ 0.22,\ 0.34)$ for $x_1$ through $x_5$.

    Marginal of $Y$: $p(y) = (0.26,\ 0.47,\ 0.27)$ for $y_1$ through $y_3$.

    **b)** $p(x \mid Y = y_1) = \left(\tfrac{1}{26},\ \tfrac{1}{13},\ \tfrac{3}{26},\ \tfrac{5}{13},\ \tfrac{5}{13}\right)$

    $p(y \mid X = x_3) = \left(\tfrac{3}{11},\ \tfrac{5}{11},\ \tfrac{3}{11}\right)$
