# Team plan (internal - not graded)

## 1. Who owns what (3 members, 4 parts)

Each member owns their assigned deliverable completely:

| | Member 1 | Member 2 | Member 3 |
|---|---|---|---|
| **Assignment** | **Part 1** - Probability Distributions (EM) | **Part 2** - Bayesian Probability | **Part 3** (Manual Calculation) & **Part 4** (Code) |
| **Deliverables** | `notebooks/Part1_Probability_Distributions_EM_Algorithm.ipynb` | `notebooks/Part2_Bayesian_Probability_IMDb_Reviews.ipynb` | `docs/Part3_Gradient_Descent_Manual_Calculation_Handwritten.pdf`<br>`notebooks/Part4_Gradient_Descent_in_Code.ipynb` |
| **README Ownership** | README Part 1 section | README Part 2 section, `requirements.txt` | README Parts 3 & 4 sections |

The rubric scores **equal speaking time in every part**, so everyone speaks in the presentation. Owning code/deliverables ≠ presenting it alone.

## 2. Moving this sample into the main repo (clean, real commits)

Each member builds **their own deliverable** in the main repo section by section, copying from this sample, running each section, and committing after each one **from their own GitHub account**:

### Member 1 (Part 1 notebook):
1. `Add Galton heights dataset`
2. `Part 1: load data and define the Gaussian model`
3. `Part 1: implement initialization, E-step, M-step and stopping rule`
4. `Part 1: add tracking table and log-likelihood plot`
5. `Part 1: add global-mean split analysis and test-height posterior`

### Member 2 (Part 2 notebook):
1. `Add project structure, requirements and .gitignore`
2. `Add compressed IMDb dataset`
3. `Part 2: add tokenizer and keyword counting in pure Python`
4. `Part 2: add Bayes posterior and probability tables`
5. `Part 2: add keyword justification and rejected candidates`

### Member 3 (Part 3 Handwritten PDF & Part 4 Notebook):
1. `Part 3: complete manual setup, chain-rule derivation, and updates 1-3`
2. `Part 3: add scanned handwritten manual calculation PDF to docs/`
3. `Part 4: add matrix model and MSE cost function`
4. `Part 4: add SciPy derivative function and chain-rule validation`
5. `Part 4: add gradient descent loop with printed steps and plots`

Then each member adds their README part in a separate commit. Do not paste everything in one commit - the Git log is a graded proof of contribution.

Before committing, each person must run their notebook and be able to explain every line (use `docs/Presentation_Questions_and_Answers.md`).

## 3. Part 3 on paper (Member 3)

- **Owner:** Member 3 completes the manual calculations for Part 3 in full.
- **Medium:** Use **paper, not a whiteboard.** The deliverable is a scanned PDF; during the presentation show the PDF on screen. Write on plain white A4 with a dark pen, with name and date at the top of each page.
- **What Member 3 calculates step-by-step:**
  1. **Setup & Derivation:** Matrix formulation ($\hat{y} = Xm + b$, $J = \frac{1}{n}\sum(\hat{y}-y)^2$), and partial derivative chain-rule derivations for $\frac{\partial J}{\partial m}$ and $\frac{\partial J}{\partial b}$.
  2. **Update 1:** Compute $\hat{y}$, residuals, gradients, and update $m$ and $b$ using $\alpha = 0.01$ (ending with $m = [-1.45, 0.87]$, $b = 0.88$, $J = 61$).
  3. **Update 2:** Recompute with new parameters (ending with $m = [-1.3316, 1.1808]$, $b = 0.9318$, $J = 6.845$).
  4. **Update 3 & Trend:** Third update ($J = 2.7238 \to 2.3904$) and summary explaining the steady decrease in loss and parameter oscillation/convergence.
- **Reference check:** Copy each step cleanly, referencing `docs/Part3_Gradient_Descent_Manual_Calculation_TypedReference.pdf` for exact arithmetic. Box each final parameter vector.
- **Scanning:** Use a phone scanner app (Google Drive Scan, Microsoft Lens, or Adobe Scan) to produce a crisp, high-contrast, multi-page PDF saved as: `docs/Part3_Gradient_Descent_Manual_Calculation_Handwritten.pdf`.
- *"Using SciPy"* applies to **Part 4 only**; Part 3 must be done purely by hand.

## 4. Presentation running order (adjust to your time slot)

| Part | Speaker | What to show |
|---|---|---|
| Intro | Member 1 | Team, repo layout, datasets (30 s) |
| 1 | Member 1 | Model, initialization, E-step, M-step (notebook cells) |
| 1 | Member 2 | "Split at the mean?" answer with our numbers + posterior plot |
| 1 | Member 3 | Tracking table, log-likelihood stopping, **live test height** |
| 2 | Member 2 | Dataset, counting rule, why P(Positive \| keyword) only |
| 2 | Member 3 | Walk through all four probabilities for one keyword (e.g. "waste") |
| 2 | Member 1 | Keyword justification + rejected candidates |
| 3 | Member 3 | Handwritten manual calculation PDF: setup, chain rule, updates 1-3, and trend |
| 4 | Member 3 | SciPy derivative function, code update loop matching Part 3 |
| 4 | Member 1 | Parameter and error plots |
| 4 | Member 2 | Learning-rate choice, final predictions, convergence after 2000 steps |
| Q&A | Everyone | Answer by part, but everyone must know Q1, Q6, Q8, Q19, Q31, Q33 |

## 5. Submission checklist

- [ ] GitHub repo link (commits from all three members)
- [ ] `README.md` with real names filled in
- [ ] All three notebooks run top to bottom (Kernel → Restart & Run All) so outputs and figures are saved
- [ ] `docs/Part3_Gradient_Descent_Manual_Calculation_Handwritten.pdf` - handwritten, scanned, one file
- [ ] Contribution PDF: fill in the contribution sheet linked in the brief → File → Download → PDF
- [ ] Rehearse the live test height with 3 random values (e.g. 62, 67, 73)

## 6. Gaps in the brief and how we handled them

| Gap | Our decision |
|---|---|
| Table says "Pros" / "Basketball Player" | Template leftover → component 2 = Fathers |
| No learning rate given in Part 3 | α = 0.01 (stable limit ≈ 0.0157; α = 0.1 diverges) |
| b given as [1, 1] | One shared bias written per data point; both entries stay equal |
| Fathers repeated per child in the file | One father per family (205) |
| "Implement in SciPy" vs "by hand" | SciPy only in Part 4; Part 3 handwritten |
| Kaggle needs login | Data copied into `data/` so the code runs immediately |
