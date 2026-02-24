# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Research paper: **"Bernoulli sets: a model for sets with random errors and corresponding random binary classification measures"** by Alexander Towell. Formalizes *random approximate sets* (Bernoulli sets) — probabilistic sets that approximate an objective set with quantifiable false positive/negative rates. Applications include Bloom filters, perfect hash filters, and encrypted search with Boolean query algebras.

This paper absorbed content from the former `bernoulli_sets_higher_order` paper. Original files preserved in `archive.zip`.

## Build

```bash
pdflatex main.tex && bibtex main && pdflatex main.tex && pdflatex main.tex
```

`alex.sty` (in project root) provides all notation macros. Loaded as `\usepackage[fancy,section]{alex}`.

## Structure

- `main.tex` — Document root, uses `\input{}` includes
- `sections/` — 13 active section files (1:1 with main.tex includes)
- `alex.sty` — Unified notation package
- `img/` — TikZ figures
- `data/` — CSV datasets (17 files)
- `code/` — C++ Monte Carlo simulations (`ppv.cpp`, `bin_class_measures_sim.cpp`)
- `research/` — Mathematica notebooks, Maxima scripts, R source, figure SVGs
- `archive.zip` — Old section files and drafts preserved from cleanup

## Section Order

1. intro → 2. algebra_of_sets → 3. bernoulli_model →
4. distributions → 5. set_theory → 6. relational →
7. uncertain_rates → 8. entropy → 9. algebraic_structure →
10. bool_search → appendix

## Key Notation (from alex.sty)

- Sets: `\Set{A}`, approximate: `\ASet{A}`, positive: `\PASet{A}`, negative: `\NASet{A}`
- Rates: `\fprate` (FPR ε), `\fnrate` (FNR ω), `\tprate` (TPR τ), `\tnrate` (TNR η)
- Functions: `\APFun{f}[\fprate][\tprate]` — approximate function with error rates
- Cardinality: `\Card{A}`, random variables: `\RV{X}`
- Set ops: `\SetUnion`, `\SetIntersection`, `\SetComplement`, `\SetDiff`

## Conceptual Layers

1. **Set algebra** → 2. **Bernoulli model** (FPR/FNR axioms, model order = block count) → 3. **Derived distributions** (PPV, NPV) → 4. **Higher-order models and k-fold composition** → 5. **Set theory** (error propagation through operations) → 6. **Extensions** (relational algebra, interval-valued rates, entropy, ADT, Boolean search)

## Scope Boundaries

This paper covers the **set-level** Bernoulli model. Content that belongs elsewhere:

- **Approximate Boolean functions** (AND, OR, NOT as maps): `bernoulli_maps/`
- **Algebraic types** (Bool as a type, sum/product types, computational basis): `bernoulli_data_type/`
- **Relational operators** (join, project over approximate relations): `bernoulli_relations/`

**What stays here**: The Boolean universe example ($U = \{\top, \bot\}$) as a minimal worked example for the PMF, and the observation that membership queries on any Bernoulli set return Bernoulli Booleans. These are set-level results that motivate the type-theoretic generalizations in other papers.
