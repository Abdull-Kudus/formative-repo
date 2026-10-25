# Team Project Plan & Workflow Guide

## 1. Member Ownership Breakdown

| Member | Assigned Part(s) | Deliverable Files | Presentation Role |
|---|---|---|---|
| **Member 1** — *Name* | **Part 1** — Probability Distributions (EM) | `notebooks/Part1_Probability_Distributions_EM_Algorithm.ipynb` | Part 1 Overview & Demo |
| **Member 2** — *Name* | **Part 2** — Bayesian Probability | `notebooks/Part2_Bayesian_Probability_IMDb_Reviews.ipynb` | Part 2 Overview & Findings |
| **Member 3** — *Name* | **Part 3** (Manual Calculation) & **Part 4** (Code) | `docs/Part3_Gradient_Descent_Manual_Calculation_Handwritten.pdf`<br>`notebooks/Part4_Gradient_Descent_in_Code.ipynb` | Parts 3 & 4 Walkthrough |

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
1. `Part 3: complete manual derivations and step-by-step updates`
2. `Part 3: add scanned handwritten calculations to docs/`
3. `Part 4: implement linear model and MSE cost function`
4. `Part 4: implement SciPy derivative and chain-rule validation`
5. `Part 4: implement gradient descent loop with printed step values and plots`

---

## 3. Part 3 Manual Calculation Guidelines (Member 3)

- **Owner:** Member 3 completes the manual calculations for Part 3 in full.
- **Format:** Handwritten on plain white A4 paper with dark ink. Full name and date at the top of each page.
- **Step-by-Step Breakdown:**
  1. **Setup & Derivation:** Formulate the linear model ($\hat{y} = Xm + b$, $J = \frac{1}{n}\sum(\hat{y}-y)^2$), and derive the partial gradients $\frac{\partial J}{\partial m}$ and $\frac{\partial J}{\partial b}$ via chain rule.
  2. **Update 1:** Compute initial predictions, residuals, gradients, and update parameters with $\alpha = 0.01$ ($m = [-1.45, 0.87]$, $b = 0.88$).
  3. **Update 2:** Recompute residuals, gradients, and update ($m = [-1.3316, 1.1808]$, $b = 0.9318$).
  4. **Update 3 & Trend:** Execute third update ($J = 2.7238 \to 2.3904$) and write a brief summary on error decrease and parameter behavior.
- **Scanning:** Scan all pages and merge into a single PDF: `docs/Part3_Gradient_Descent_Manual_Calculation_Handwritten.pdf`.
