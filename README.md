# A-note-on-some-tabulated-defining-equations-of-modular-curves
````markdown
# Verification programs for corrected entries in Yang's tables of modular curve equations

This repository contains Mathematica notebooks used to verify and search for corrected defining equations in Yifan Yang's tables of modular curves.

The computations concern the explicit equations in:

- Y. Yang, *Defining equations of modular curves*, Advances in Mathematics 204 (2006), 481–508.
- Y. Yang, *Transformation formulas for generalized Dedekind eta functions*, Bulletin of the London Mathematical Society 36 (2004), 671–682.

The purpose of the notebooks is to verify corrected entries in the tables for \(X_0(N)\) and \(X_1(N)\) by direct \(q\)-expansion computations.

## Files

### `verify_yang_corrections_one_by_one.nb`

This notebook verifies the corrected equations one by one.

It includes:

- ordinary Dedekind eta products;
- generalized Dedekind eta products \(E_g(\tau)\);
- trace sums of generalized eta products over coset representatives;
- direct substitution of the corrected \(X,Y\) functions into the proposed equations;
- coefficient-by-coefficient verification of the resulting \(q\)-series residuals.

The notebook currently checks corrected entries for:

\[
X_0(N),\quad N=23,26,27,30,31,34,39,42,46,50,
\]

and

\[
X_1(N),\quad N=13,22.
\]

Each case is placed in a separate section, so the user can run the verification case by case.

### `search_eta_products_for_yang_tables.nb`

This notebook is used for experimental searches of eta-products and generalized eta-products with prescribed cusp behavior.

It is intended for finding candidate modular functions \(X\) and \(Y\) with prescribed pole orders at infinity. The search is based on Yang's cusp-order formula for generalized Dedekind eta functions.

The notebook is exploratory and is mainly useful for:

- searching products of \(E_g\)'s of a fixed length;
- checking their orders at cusps;
- identifying candidates with poles only at the required cusp;
- comparing candidates with Yang's tabulated functions.

## Mathematical conventions

For the \(X_0(N)\) table, the notation

\[
a^r
\]

denotes the ordinary eta product

\[
\eta(a\tau)^r.
\]

For the \(X_1(N)\) table, the notation

\[
a^r
\]

denotes

\[
E_a(\tau)^r,
\]

where \(E_g\) is Yang's generalized Dedekind eta function

\[
E_g(\tau)
=
q^{N B(g/N)/2}
\prod_{m=1}^{\infty}
(1-q^{(m-1)N+g})(1-q^{mN-g}),
\]

with

\[
B(x)=x^2-x+\frac{1}{6},
\qquad q=e^{2\pi i\tau}.
\]

The notation

\[
\sum_k F
\]

means the trace of \(F\) over a set of \(k\) coset representatives, as in Yang's tables.

## How the verification works

For each corrected entry, the notebook computes the \(q\)-expansions of the functions \(X\) and \(Y\), substitutes them into the corrected equation, and expands the residual series

\[
R(q)=F(X(q),Y(q)).
\]

The case passes if all coefficients of \(R(q)\) vanish in the checked range.

For example, a successful verification prints a message of the form

```text
X0(50)   PASS   checked q^-12 through q^10
````

A failed verification prints the first nonzero coefficient, for example

```text
X0(50)   FAIL   checked q^-12 through q^10
First nonzero coefficient: {-11, -6}
```

This means that the coefficient of (q^{-11}) in the residual is (-6), so the tested equation or the tested implementation is not correct.

## How to run

Open the notebook in Wolfram Mathematica.

1. Evaluate the initialization section first.
2. Evaluate each verification section separately.
3. Confirm that every case returns `PASS`.

The default settings are:

```mathematica
Prec = 120;
VerifyTo = 10;
```

Here `Prec` controls the truncation length of the (q)-series, and `VerifyTo` controls how far beyond the constant term the residual is checked.

For stronger checks, increase `Prec` and `VerifyTo`, for example:

```mathematica
Prec = 200;
VerifyTo = 30;
```

Then re-run the initialization and all verification sections.

## Important implementation details

The implementation uses Yang's transformation formula for generalized Dedekind eta functions.

In particular, for

[
\gamma=
\begin{pmatrix}
a & b\
cN & d
\end{pmatrix}
\in \Gamma_0(N),
]

the program applies the transformation

[
E_g(\gamma\tau)
===============

\varepsilon(a,bN,c,d)
\exp\left(\pi i\left(\frac{g^2ab}{N}-gb\right)\right)
E_{ag}(\tau),
]

and uses the relations

[
E_{g+N}=E_{-g}=-E_g.
]

For the examples in the verification notebook, the common multiplier (\varepsilon) cancels in the products because the exponent sums satisfy the modularity conditions.


## Requirements

* Wolfram Mathematica 12.3 or later.
* No external Mathematica packages are required.

The notebooks use exact symbolic and rational computations whenever possible.

## Reproducibility

The corrected equations are verified by direct (q)-expansion substitution. The verification is not a formal proof assistant check, but it provides an explicit reproducible computation of the displayed identities to the chosen order.

Users can increase `Prec` and `VerifyTo` to check more terms.

## Citation

If you use this repository, please cite Yang's original papers:

```bibtex
@article{Yang2006,
  author  = {Yang, Yifan},
  title   = {Defining equations of modular curves},
  journal = {Advances in Mathematics},
  volume  = {204},
  year    = {2006},
  pages   = {481--508}
}

@article{Yang2004,
  author  = {Yang, Yifan},
  title   = {Transformation formulas for generalized Dedekind eta functions},
  journal = {Bulletin of the London Mathematical Society},
  volume  = {36},
  year    = {2004},
  pages   = {671--682}
}
```

If this repository accompanies a note or preprint, cite that note as well.

## License

Choose a license before making the repository public.

A common choice for research code is the MIT License. If you want users to cite the work but still freely use the code, MIT is usually appropriate.

## Disclaimer

These notebooks are research code. They are provided to make the computations reproducible and to help readers check the corrected equations. Users should independently verify the computations before relying on them in published work.

```
```
