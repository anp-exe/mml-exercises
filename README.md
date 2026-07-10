# MML Exercise Answers

Worked solutions to the end-of-chapter exercises in *Mathematics for Machine Learning* (Deisenroth, Faisal & Ong), published as a static site built with MkDocs and Material.

**Live site:** https://anp-exe.github.io/mml-excerises/

Every question follows the same layout: a Topics & Definitions box, a plain-English explanation, the worked steps with real matrices, then the boxed answer. Math is written in LaTeX and rendered with KaTeX.

## Progress

| Chapter | Exercises answered |
|:------:|:------------------:|
| 2 · Linear Algebra | 2.1 to 2.20 complete |
| 3 · Analytic Geometry | 3.1 to 3.6 |
| 4 · Matrix Decompositions | placeholder |
| 5 · Vector Calculus | placeholder |
| 6 · Probability and Distributions | placeholder |
| 7 · Continuous Optimization | placeholder |
| 8 · When Models Meet Data | placeholder |
| 9 · Linear Regression | placeholder |
| 10 · Dimensionality Reduction (PCA) | placeholder |
| 11 · Density Estimation (GMM) | placeholder |
| 12 · Classification (SVM) | placeholder |

## Run it locally

You need Python 3.9 or newer.

```bash
pip install -r requirements.txt
mkdocs serve
```

Then open http://127.0.0.1:8000. Edits to any `.md` file reload automatically. To build the static site into a `site/` folder without serving, run `mkdocs build`.

## Deploy

The repo includes a GitHub Actions workflow at `.github/workflows/deploy.yml`. On every push to `main` it builds the site and publishes it to the `gh-pages` branch. Pages then serves from that branch at the live URL above.

## Project structure

```
mml-excerises/
├── mkdocs.yml                 site config, nav, theme, extensions
├── requirements.txt           python dependencies
├── .github/workflows/
│   └── deploy.yml             auto-deploy to GitHub Pages on push
└── docs/
    ├── index.md               home page, progress table, resources
    ├── stylesheets/extra.css  pastel theme and admonition colours
    ├── javascripts/katex.js   KaTeX auto-render hook
    └── chapters/
        ├── ch2.md             filled in
        └── ch3.md … ch12.md   placeholders
```

## Adding a chapter's answers

Open the relevant `docs/chapters/chN.md` and use the three custom boxes styled in the CSS:

```markdown
!!! theory "Topics & Definitions"
    - **Term** definition.

!!! steps "Elimination"
    $$\begin{bmatrix}1&0\\0&1\end{bmatrix}$$

!!! answer "Answer"
    $$\mathbf{x} = (\tfrac38, \tfrac38, \tfrac14)$$
```

Write math in LaTeX between `$ … $` (inline) or `$$ … $$` (display), then update the progress table in `docs/index.md`.

## Helpful resources

Stuck reducing a matrix to RREF? The [emathhelp RREF calculator](https://www.emathhelp.net/calculators/linear-algebra/reduced-row-echelon-form-rref-calculator/) shows every elimination step, which is handy for checking your work. For visual intuition on vectors, transformations, and matrices, 3Blue1Brown's [Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) series is excellent.

## Conventions

Pastel aesthetic (lilac, sage, pink). Each question runs definitions to explanation to worked steps to boxed answer. Math in LaTeX rendered by KaTeX.
