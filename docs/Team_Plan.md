# Team Project Plan & Workflow Guide

## 1. Member Ownership Breakdown

| Member | Notebook & Commits | Part 3 Manual Calculation (Paper) | Presentation Role |
|---|---|---|---|
| **Member 1** — *Name* | Part 1 — Probability Distributions (EM) | Update 2 | Part 1 Overview & Demo |
| **Member 2** — *Name* | Part 2 — Bayesian Probability | Update 3 + Trend Summary | Part 2 Overview & Findings |
| **Member 3** — *Name* | Part 4 — Gradient Descent in Code | Setup, Derivations, Update 1 + Scan PDF | Parts 3 & 4 Walkthrough |

---

## 2. Commit Strategy for Teammates

Each member should make granular, meaningful commits from their own GitHub account so individual contributions are clearly reflected in Git history:

### Member 1 (Part 1):
1. `Add Galton heights dataset to data/`
2. `Part 1: load dataset and define Gaussian mixture model`
3. `Part 1: implement EM initialization, E-step, M-step, and convergence`
4. `Part 1: add tracking table and visualization plots`
5. `Part 1: add global-mean split analysis and test-height posterior`

### Member 2 (Part 2):
1. `Add project requirements and .gitignore`
2. `Add compressed IMDb dataset to data/`
3. `Part 2: add text tokenizer and keyword counting`
4. `Part 2: compute prior, likelihood, marginal, and posterior`
5. `Part 2: add keyword results table and justification`

### Member 3 (Parts 3 & 4):
1. `Part 4: implement linear model and MSE cost function`
2. `Part 4: implement SciPy derivative and chain-rule validation`
3. `Part 4: implement gradient descent loop with printed step values`
4. `Part 4: add parameter trajectory and loss visualization plots`
5. `Part 3: add scanned handwritten calculations to docs/`

---

## 3. Part 3 Manual Calculation Guidelines

- **Format:** Handwritten on plain paper with dark ink. Full names and signatures at the top of each page.
- **Contribution Requirement:** Every member completes at least one full iteration:
  - **Member 3:** Problem setup, chain rule derivation, and Update 1.
  - **Member 1:** Update 2 (using outputs from Update 1).
  - **Member 2:** Update 3 and convergence/trend discussion (using outputs from Update 2).
- **Scanning:** Scan all pages and merge into a single PDF: `docs/Part3_Gradient_Descent_Manual_Calculation_Handwritten.pdf`.
