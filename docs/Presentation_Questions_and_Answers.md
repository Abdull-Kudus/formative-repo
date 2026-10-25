# Presentation Q&A preparation

Every answer uses numbers from *our* run. Each member should be able to answer every question, not only their own part. Practise saying them out loud.

---

## Part 1 - EM algorithm

**Q1. Should you just draw a line at the global mean, split into two piles, and average each pile?**
No, for five reasons we can prove from our run:
1. *Misclassification:* the cut at 67.21 in puts 44 of the 205 fathers in the "children" pile and 403 of the 934 children in the "fathers" pile. The two bell curves overlap, and a single line cannot separate overlapping groups.
2. *Biased estimates:* cutting removes each curve's tail, so the piles look narrower (sd 2.04 and 1.89 in) than EM's estimates (2.30 and 2.46 in).
3. *Wrong place:* the global mean depends on how many people are in each group. EM's 50/50 boundary is 66.54 in, not 67.21 in.
4. *No uncertainty:* a 66.71-in person is "100% child" for the cut, but EM gives 46.1% child / 53.9% father - essentially a coin flip, and EM says so.
5. *No improvement:* it is a one-shot guess. We used it as EM's starting point (log-likelihood −3071.12) and EM improved it to −3046.99.

**Q2. What is a "soft assignment" / responsibility?**
Instead of saying "this height IS a child", each height gets a share of belonging to each group, e.g. 70 in → 3.3% Children, 96.7% Fathers. The shares add up to 1. In the M-step a 66-in person contributes 0.62 of a point to the Children mean and 0.38 to the Fathers mean.

**Q3. What parameters does EM estimate?**
Six: two means (μ₁, μ₂), two variances (σ₁², σ₂²), two mixing coefficients (π₁, π₂), with π₁ + π₂ = 1. Final values: μ₁ = 64.18, μ₂ = 69.52, σ₁² = 5.30, σ₂² = 6.04, π₁ = 0.4325, π₂ = 0.5675.

**Q4. What are mixing coefficients?**
The share of the data each bell curve is responsible for - the prior probability that a random height comes from that group. π₂ = 0.5675 means 56.75% of the 1139 heights are attributed to the taller curve.

**Q5. How did you initialise?**
From the global-mean split: pile below 67.21 in → μ₁ = 64.26, σ₁² = 4.14, π₁ = 575/1139 = 0.5048; pile above → μ₂ = 70.21, σ₂² = 3.57, π₂ = 0.4952. We chose it so the table shows EM correcting the naive method.

**Q6. Explain the E-step with numbers.**
For height x, compute πₖ·N(x | μₖ, σₖ²) for both groups, then divide each by their sum (Bayes' theorem). For 70 in: Children 0.4325 × 0.007083 = 0.003063; Fathers 0.5675 × 0.159230 = 0.090365; sum = 0.093428; P(Children | 70) = 0.003063 / 0.093428 = 0.0328.

**Q7. Explain the M-step.**
Use responsibilities as weights. Nₖ = sum of responsibilities (effective group size); new μₖ = weighted average of heights; new σₖ² = weighted average squared distance from the new mean; new πₖ = Nₖ / 1139. Final: N₁ = 492.6, N₂ = 646.4.

**Q8. When does EM stop and why log-likelihood?**
When the log-likelihood improves by less than 10⁻⁶. The log-likelihood measures how well the current two bell curves explain all 1139 heights. EM is guaranteed never to decrease it (our run: it never decreased), so when it stops rising we are at a (local) maximum. Ours stopped after 309 iterations at −3046.9895.

**Q9. Why the log of the likelihood?**
The likelihood is a product of 1139 small numbers (≈0.09 each) - it underflows to 0 on a computer. The log turns the product into a sum and has the same maximum.

**Q10. Why did EM need 309 iterations when iteration 1 already gained 17.5?**
Most of the gain is early (−3071.12 → −3053.58 → −3049.71). After that the two curves overlap a lot, so each step only moves them slightly; π₁ drifts slowly from 0.50 to 0.43.

**Q11. Did EM really find Children vs Fathers?**
Partly - we checked with the hidden labels. Component 1 is 92% children (mostly daughters, mean 64.2 in). Component 2 holds 81% of the fathers (166 of 205) but most of its weight is sons. Galton's "children" are adults: sons average 69.2 in, fathers 69.3 in. EM is unsupervised; it found the strongest height structure, which is sex. So short = confidently a child; tall = father *or* adult son.

**Q12. Why one father per family?**
In the file each father is repeated on every row of his children (205 fathers, 934 rows). Keeping repeats would count the same man up to 15 times and inflate π₂.

**Q13. Why fathers, not mothers?**
Fathers (mean 69.3 in) are taller than the children's average (66.7 in), matching the template where component 1 is the shorter "Children" group.

**Q14. The brief says "Pros" / "Basketball Player". Why do you say Fathers?**
The table template was written for a children-vs-basketball-players example; our dataset is Galton's, so component 2 is Fathers. Same maths.

**Q15. Could EM get stuck or fail?**
Yes: it finds a *local* maximum, so a bad start can give a worse answer - in practice you run several starts and keep the highest log-likelihood. A variance can also collapse to 0 if one component locks onto a single repeated value; it did not happen here (smallest variance in our run 3.57).

**Q16. Is it "from scratch" if you use NumPy?**
Yes. NumPy only stores arrays and does arithmetic. Every formula (Gaussian density, E-step, M-step, log-likelihood, stopping rule) is written by us - no scikit-learn `GaussianMixture`, no SciPy distributions.

**Q17. Live test: how do you classify the coach's height?**
Type it into `TEST_HEIGHT` in the notebook (last cell of the Part 1 notebook). It prints both densities, both weighted densities, the evidence (their sum), and both posteriors.

---

## Part 2 - Bayesian probability

**Q18. Which conditional probability did you compute and why only one?**
P(Positive | keyword) for all six keywords - the brief says not to compute both. For a negative word a low value is the signal; P(Negative | keyword) = 1 − P(Positive | keyword) anyway.

**Q19. Define the four probabilities for "excellent".**
Prior P(Positive) = 25000/50000 = 0.5. Likelihood P(excellent | Positive) = 2868/25000 = 0.1147. Marginal P(excellent) = 3552/50000 = 0.0710. Posterior = 0.1147 × 0.5 / 0.0710 = 0.8074.

**Q20. What is the difference between likelihood and posterior?**
Likelihood: *among positive reviews*, how often the word appears (11.47% for "excellent"). Posterior: *among reviews with the word*, how often the review is positive (80.74%). Bayes' theorem converts one into the other.

**Q21. Why is the prior exactly 0.5?**
The dataset is balanced: 25,000 positive and 25,000 negative. So here the posterior equals the share of positive reviews among reviews containing the word (175/2534 = 0.0691 for "waste") - our code checks this for every keyword.

**Q22. Why these keywords?**
Strong *and* frequent: every positive keyword gives > 0.80, every negative one < 0.10, and each appears in 1,199-4,434 reviews, so the probabilities rest on big counts.

**Q23. Why not "great" or "bad"?**
"great" appears in 4,099 negative reviews (posterior 0.6741). "bad" appears in 2,960 positive reviews (posterior 0.2511) - e.g. "bad guy" is in 382 positive reviews.

**Q24. "masterpiece" sounds very positive - why rejected?**
Only 0.7274: 329 negative reviews use it, often for a *different* film ("the original was made to look like a flawless masterpiece") or sarcastically.

**Q25. How did you count a word?**
Lower-case, replace `<br />`, turn punctuation and digits into spaces, split, and check whether the word is in the set of words of the review - once per review. "Excellent!" counts; "excellently" does not.

**Q26. Why no pandas / NLTK / scikit-learn?**
The brief allows basic Python only. We used the standard library `csv` (read rows), `gzip` (the data file is compressed to fit GitHub) and `string` (punctuation list).

**Q27. Is a keyword alone a good classifier?**
No: 35,218 of the 50,000 reviews (70%) contain none of our six words. It shows how one word shifts belief. Combining many words gives Naive Bayes.

**Q28. What if a keyword never appeared in positive reviews?**
The likelihood would be 0 and the posterior 0 - too extreme. Laplace smoothing (add 1 to every count) fixes this. We did not need it: our smallest count is 175.

**Q29. The dataset has 418 duplicate reviews - does it matter?**
We used the dataset as published (50,000 rows). 418 is 0.8% of the data and cannot change our conclusions.

---

## Parts 3 & 4 - Gradient descent

**Q30. Why the minus sign in the update?**
The gradient points uphill (direction of increasing error). Subtracting it moves downhill. Update 1: gradient for m₂ was +113, so m₂ went down from 2 to 0.87.

**Q31. Explain the chain rule here.**
J depends on m only through ŷ. ∂J/∂m₁ = ∂J/∂ŷ · ∂ŷ/∂m₁ = (2/n)(ŷ − y) · x₁. For update 1: (1)(1) + (11)(4) = 45.

**Q32. Where does 2/n come from, and why does it vanish?**
2 from the power rule on the square, 1/n from the mean. n = 2, so 2/2 = 1.

**Q33. Why α = 0.01? It was not given.**
The cost's steepest curvature is ≈127.5, so steps are stable only if α < 2/127.5 ≈ 0.0157. α = 0.1 makes J jump from 61 to 8089.7 after one step. α = 0.01 is stable and gives clean decimals.

**Q34. Why does m₂ go down then up?**
x₂ values (3 and 10) are large, so J is steep along m₂ and the first step overshoots: point 2's error flips +11 → −2.22 → +1.41. Overshoots shrink, so it is damped zig-zag.

**Q35. Is the error reducing?**
Yes: J = 61 → 6.845 → 2.7238 → 2.3904 after three updates; 2000 updates give J ≈ 0 and predictions ≈ [5, 6].

**Q36. Why can J reach 0?**
Two data points and three parameters (m₁, m₂, b): there are infinitely many lines through both points. Gradient descent finds one of them.

**Q37. Why does b stay the same in both entries?**
The equation has one bias. ∂J/∂b = (2/n)(e₁ + e₂) is a single number, subtracted from both entries. (If b were two independent parameters, the gradient would be (2/n)e = [1, 11] in update 1 - but then the model would not be y = m₁x₁ + m₂x₂ + b.)

**Q38. How does SciPy compute the derivative?**
`scipy.differentiate.derivative` uses finite differences: it evaluates J at points slightly left and right of the current value, and refines the step until the estimate stops changing. We check it on f(x) = 3x² + 2x at x = 2 (answer 14) and against our chain-rule formula every iteration - they match (e.g. [45, 113], 12).

**Q39. Could gradient descent get stuck in a local minimum here?**
No. MSE for a linear model is convex (bowl-shaped), so every minimum is a global one.

**Q40. Why matrix multiplication instead of loops?**
The brief asks for it, and ŷ = Xm + b computes both predictions in one operation; Xᵀe computes both partial derivatives of m at once. It scales to any number of points or features.

---

## General

**Q41. Who did what?** Answer from the contribution table and Git log - each member names their own files and commits.

**Q42. How to run everything?** `pip install -r requirements.txt`, then open each notebook in `notebooks/` and choose Run All.
