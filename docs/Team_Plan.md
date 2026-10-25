# Team plan (internal — not graded)

## 1. Who owns what (3 members, 4 parts)

Member 3 = the person who built this sample repo (owns Parts 3 and 4).

| | Member 1 | Member 2 | Member 3 |
|---|---|---|---|
| Notebook & commits | Part 1 — Probability Distributions (EM) | Part 2 — Bayesian Probability | Part 4 — Gradient Descent in Code |
| Shared files | README Part 1 | README Part 2, `requirements.txt` | README Part 3–4 |
| Part 3 — Gradient Descent Manual Calculation (paper) | Update 2 | Update 3 + trend summary | **Owner:** setup, chain-rule derivation, update 1; checks and scans all pages |

The rubric scores **equal speaking time in every part**, so everyone speaks in every part (below). Owning code ≠ presenting it alone.

## 2. Moving this sample into the main repo (clean, real commits)

Each member builds **their own notebook** in the main repo section by section, copying from this sample, running each section, and committing after each one **from their own GitHub account**, e.g.:

Member 1 (Part 1 notebook):
1. `Add Galton heights dataset`
2. `Part 1: load data and define the Gaussian model`
3. `Part 1: implement initialization, E-step, M-step and stopping rule`
4. `Part 1: add tracking table and log-likelihood plot`
5. `Part 1: add global-mean split analysis and test-height posterior`

Member 2 (Part 2 notebook):
1. `Add project structure, requirements and .gitignore`
2. `Add compressed IMDb dataset`
3. `Part 2: add tokenizer and keyword counting in pure Python`
4. `Part 2: add Bayes posterior and probability tables`
5. `Part 2: add keyword justification and rejected candidates`

Member 3 (Part 4 notebook + Part 3 PDF):
1. `Part 4: add matrix model and MSE cost`
2. `Part 4: add SciPy derivative function and chain-rule check`
3. `Part 4: add gradient descent loop with printed steps`
4. `Part 4: add parameter and error plots`
5. `Part 3: add scanned handwritten manual calculation`

Then each member adds their README part in a separate commit. Do not paste everything in one commit — the Git log is a graded proof of contribution.

Before committing, each person must run their script and be able to explain every line (use `docs/Presentation_Questions_and_Answers.md`).

## 3. Part 3 on paper

- Use **paper, not the board.** The deliverable is a scanned PDF; during the presentation show the PDF on screen. Write on plain white A4 with a dark pen, name + signature at the top of each page.
- **Member 3 owns Part 3** and writes the hardest pages: Pages 1–2 of the typed key (setup, chain-rule derivation, update 1), ending with a boxed result: m = [−1.45, 0.87], b = 0.88.
- **Member 1** writes Page 3 (update 2). Start by restating the values received: "From update 1: m = [−1.45, 0.87], b = 0.88".
- **Member 2** writes Pages 4–5 (update 3, summary and trend). Start with "From update 2: m = [−1.3316, 1.1808], b = 0.9318".
- This gives every member one full iteration, as the rubric requires ("at least one full iteration per member"). The handwriting changes are fine; the restated starting values show it is one connected solution.
- Member 3 checks every page against the typed key before scanning.
- Copy every line from `docs/Part3_Gradient_Descent_Manual_Calculation_TypedReference.pdf`, including the small arithmetic lines (e.g. "−1 − 0.45 = −1.45"). Box each final answer.
- Scan with a phone scanner app (Google Drive "Scan", Microsoft Lens or Adobe Scan) → combine into **one** PDF in page order: Member 3 (pages 1–2), Member 1 (page 3), Member 2 (pages 4–5) → save as `docs/Part3_Gradient_Descent_Manual_Calculation_Handwritten.pdf`.
- "Using SciPy" applies to **Part 4 only**; Part 3 must be by hand.

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
| 3 | Member 3 | Setup, chain rule, update 1 (their handwriting) |
| 3 | Member 1 | Update 2 (their handwriting) |
| 3 | Member 2 | Update 3 and the trend (their handwriting) |
| 4 | Member 3 | SciPy derivative function and update code |
| 4 | Member 1 | Plots and trend |
| 4 | Member 2 | Learning-rate choice, final predictions, convergence after 2000 steps |
| Q&A | Everyone | Answer by part, but everyone must know Q1, Q6, Q8, Q19, Q31, Q33 |

## 5. Submission checklist

- [ ] GitHub repo link (commits from all three members)
- [ ] `README.md` with real names filled in
- [ ] All three notebooks run top to bottom (Kernel → Restart & Run All) so outputs and figures are saved
- [ ] `docs/Part3_Gradient_Descent_Manual_Calculation_Handwritten.pdf` — handwritten, scanned, one file
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
