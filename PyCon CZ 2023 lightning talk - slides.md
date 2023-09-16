---
title: Static Analysis Tools
author: Jiří Bajer
format: revealjs
theme: league
highlight-style: base16-tomorrow
defaultTiming: 140
width: 1024
height: 768
---

## Static Analysis Using Ruff and Radon

<!-- .slide: data-background-image="pyconcz23.svg" data-background-size=contain data-background-opacity=0.2 -->

Jiří Bajer

[rossum.ai](https://rossum.ai)

---

## 🎖️ Ruff - Code Quality

- **Replaces `isort`, `pylint` and `flake8` + plugins**
  - Fast (Rust)
  - Automatic fixes
  - Monorepo-friendly
  - Actively maintained
  - No PIP dependencies

- **Gradual adoption**
  - Subset of rules/skip rules/skip autofixes
  - Pre-commit hook
  - Reformat on save in VS Code

note: [Ruff](https://docs.astral.sh/ruff/rules/)

---

## 📐 Radon - Code Size

- Overall size of the codebase (SLOC)

- Number of lines per module

- Ratio of code vs. comments+docstrings

- Which modules to split soon

## 👇

`radon raw`

note: `radon raw -s . | tail -n 11 | grep SLOC`
[Radon](https://radon.readthedocs.io/en/latest/index.html)


---

## 🤯 Radon - Cyclomatic Complexity

- Which functions/methods should be split

  - Number of code paths/branches (`if`/`try`)

  - Number of testcases for 100% coverage

## 👇

`radon cc`

Ruff: `C901` rule + `max-complexity`

note: `radon cc -n D -s -a .` (Ruff avoids complexity creep over time, Radon shows static state)

---

## 🔍 Code Churn vs. Cyclomatic Complexity

- How often a module changes

- Refactor only code that is:

  **complicated** AND **often changed**

  📖 Sandi Metz: [Breaking Up the Behemoth](https://sandimetz.com/blog/2017/9/13/breaking-up-the-behemoth)

## 👇

`git log --name-only`

note: `git log --pretty='' --name-only | sort | uniq -c | sort -n` -- anyone aware of a Python-aware tool? [github.com/sarimak/static_analysis_lt](https://github.com/sarimak/static_analysis_lt)
