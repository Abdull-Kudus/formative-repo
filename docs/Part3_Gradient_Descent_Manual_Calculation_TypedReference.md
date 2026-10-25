---
title: "Part 3 — Gradient Descent Manual Calculation (typed reference)"
geometry: margin=2cm
---

> **What this is.** Part 3 is gradient descent worked out by hand on paper. Part 4 (*Gradient Descent in Code*) runs the same problem in Python and must give the same numbers.
>
> **How to use this file.** This is the typed answer key. The graded submission must be **handwritten**: it is written by **two people**: **Writer 1** copies Pages 1–2 (setup, chain-rule derivation, update 1); **Writer 2** continues from the values Writer 1 ends with and copies Pages 3–5 (updates 2 and 3, summary and trend). Each writer signs their pages, and the pages are scanned into one PDF (see `Team_Plan.md`, section 3). Write every line, including the "small" ones — the rubric penalises skipped arithmetic.

# Page 1 — Setup and Chain-Rule derivation (Writer 1)

## 1. The model in matrix form

$$\hat y = m_1x_1 + m_2x_2 + b \quad\Longrightarrow\quad \hat{\mathbf y} = X\mathbf m + \mathbf b$$

$$X=\begin{bmatrix}1&3\\4&10\end{bmatrix},\quad
\mathbf y=\begin{bmatrix}5\\6\end{bmatrix},\quad
\mathbf m^{(0)}=\begin{bmatrix}-1\\2\end{bmatrix},\quad
\mathbf b^{(0)}=\begin{bmatrix}1\\1\end{bmatrix}$$

* Row 1 of $X$ is data point 1: $(x_1,x_2)=(1,3)$; row 2 is data point 2: $(4,10)$.
* $n = 2$ data points.
* **Bias:** the equation has *one* bias $b$. It is written as the vector $\mathbf b=[b,b]^T$ only so it can be added to $X\mathbf m$ (one entry per data point). Both entries therefore always stay equal.
* **Learning rate:** not given in the brief, so we chose $\alpha = 0.01$. Reason: the steepest direction of this cost has curvature $\approx 127.5$, and gradient descent is only stable when $\alpha < 2/127.5 \approx 0.0157$. With $\alpha = 0.1$ the cost jumps from 61 to 8089.7 after one step (diverges).

## 2. Cost function (Mean Squared Error)

$$J(\mathbf m,b)=\frac1n\sum_{i=1}^{n}(\hat y_i-y_i)^2=\frac1n\,\mathbf e^T\mathbf e,\qquad \mathbf e=\hat{\mathbf y}-\mathbf y$$

With $n=2$: $J=\frac12\big[(\hat y_1-y_1)^2+(\hat y_2-y_2)^2\big]$.

## 3. Derivatives with the Chain Rule

$J$ depends on $\mathbf m$ and $b$ **through** $\hat{\mathbf y}$, so: $\dfrac{\partial J}{\partial \text{parameter}}=\dfrac{\partial J}{\partial \hat y}\cdot\dfrac{\partial \hat y}{\partial \text{parameter}}$.

**Link 1 (outer):** $\dfrac{\partial J}{\partial \hat y_i}=\dfrac1n\cdot 2(\hat y_i-y_i)\cdot 1=\dfrac2n e_i$  (power rule: derivative of $u^2$ is $2u$; derivative of $\hat y_i - y_i$ w.r.t. $\hat y_i$ is 1).

**Link 2 (inner):** from $\hat y_i = x_{i1}m_1 + x_{i2}m_2 + b$:
$\dfrac{\partial \hat y_i}{\partial m_1}=x_{i1}$, $\dfrac{\partial \hat y_i}{\partial m_2}=x_{i2}$, $\dfrac{\partial \hat y_i}{\partial b}=1$.

**Multiply the links and add over both data points:**

$$\frac{\partial J}{\partial m_1}=\sum_i\frac2n e_i\,x_{i1}=\frac22\big(e_1\cdot1+e_2\cdot4\big)$$
$$\frac{\partial J}{\partial m_2}=\sum_i\frac2n e_i\,x_{i2}=\frac22\big(e_1\cdot3+e_2\cdot10\big)$$
$$\frac{\partial J}{\partial b}=\sum_i\frac2n e_i\cdot1=\frac22\big(e_1+e_2\big)$$

**Matrix form (what we use below):**

$$\boxed{\frac{\partial J}{\partial \mathbf m}=\frac2n X^T\mathbf e}\qquad
\boxed{\frac{\partial J}{\partial b}=\frac2n \mathbf 1^T\mathbf e}\qquad
X^T=\begin{bmatrix}1&4\\3&10\end{bmatrix},\ \ \frac2n=\frac22=1$$

**Update rule:** $\mathbf m \leftarrow \mathbf m-\alpha\dfrac{\partial J}{\partial \mathbf m}$, $\;b \leftarrow b-\alpha\dfrac{\partial J}{\partial b}$.

\newpage

# Page 2 — Update 1 (Writer 1)

Start: $\mathbf m=[-1,\ 2]^T$, $b=1$.

**Step 1 – Matrix product $X\mathbf m$**
$$X\mathbf m=\begin{bmatrix}1&3\\4&10\end{bmatrix}\begin{bmatrix}-1\\2\end{bmatrix}
=\begin{bmatrix}(1)(-1)+(3)(2)\\(4)(-1)+(10)(2)\end{bmatrix}
=\begin{bmatrix}-1+6\\-4+20\end{bmatrix}=\begin{bmatrix}5\\16\end{bmatrix}$$

**Step 2 – Predictions** $\hat{\mathbf y}=X\mathbf m+\mathbf b=\begin{bmatrix}5+1\\16+1\end{bmatrix}=\begin{bmatrix}6\\17\end{bmatrix}$

**Step 3 – Error** $\mathbf e=\hat{\mathbf y}-\mathbf y=\begin{bmatrix}6-5\\17-6\end{bmatrix}=\begin{bmatrix}1\\11\end{bmatrix}$

**Step 4 – Cost** $J=\frac12\big(1^2+11^2\big)=\frac12(1+121)=\frac{122}{2}=61$

**Step 5 – Gradient w.r.t. m**
$$X^T\mathbf e=\begin{bmatrix}1&4\\3&10\end{bmatrix}\begin{bmatrix}1\\11\end{bmatrix}
=\begin{bmatrix}(1)(1)+(4)(11)\\(3)(1)+(10)(11)\end{bmatrix}
=\begin{bmatrix}1+44\\3+110\end{bmatrix}=\begin{bmatrix}45\\113\end{bmatrix},\qquad
\frac{\partial J}{\partial \mathbf m}=1\times\begin{bmatrix}45\\113\end{bmatrix}=\begin{bmatrix}45\\113\end{bmatrix}$$

**Step 6 – Gradient w.r.t. b** $\dfrac{\partial J}{\partial b}=1\times(1+11)=12$

**Step 7 – Update**
$$m_1=-1-0.01(45)=-1-0.45=-1.45$$
$$m_2=2-0.01(113)=2-1.13=0.87$$
$$b=1-0.01(12)=1-0.12=0.88\quad\Rightarrow\quad \mathbf b=[0.88,\ 0.88]^T$$

**After update 1:** $\mathbf m=[-1.45,\ 0.87]^T$, $b=0.88$.

\newpage

# Page 3 — Update 2 (Writer 2 continues from Writer 1's result)

Start: $\mathbf m=[-1.45,\ 0.87]^T$, $b=0.88$.

**Step 1 – Matrix product**
$$X\mathbf m=\begin{bmatrix}(1)(-1.45)+(3)(0.87)\\(4)(-1.45)+(10)(0.87)\end{bmatrix}
=\begin{bmatrix}-1.45+2.61\\-5.80+8.70\end{bmatrix}=\begin{bmatrix}1.16\\2.90\end{bmatrix}$$

**Step 2 – Predictions** $\hat{\mathbf y}=\begin{bmatrix}1.16+0.88\\2.90+0.88\end{bmatrix}=\begin{bmatrix}2.04\\3.78\end{bmatrix}$

**Step 3 – Error** $\mathbf e=\begin{bmatrix}2.04-5\\3.78-6\end{bmatrix}=\begin{bmatrix}-2.96\\-2.22\end{bmatrix}$

**Step 4 – Cost** $J=\frac12\big((-2.96)^2+(-2.22)^2\big)=\frac12(8.7616+4.9284)=\frac12(13.69)=6.845$

**Step 5 – Gradient w.r.t. m**
$$X^T\mathbf e=\begin{bmatrix}(1)(-2.96)+(4)(-2.22)\\(3)(-2.96)+(10)(-2.22)\end{bmatrix}
=\begin{bmatrix}-2.96-8.88\\-8.88-22.20\end{bmatrix}=\begin{bmatrix}-11.84\\-31.08\end{bmatrix},\qquad
\frac{\partial J}{\partial \mathbf m}=\begin{bmatrix}-11.84\\-31.08\end{bmatrix}$$

**Step 6 – Gradient w.r.t. b** $\dfrac{\partial J}{\partial b}=1\times(-2.96-2.22)=-5.18$

**Step 7 – Update** (minus a negative = plus)
$$m_1=-1.45-0.01(-11.84)=-1.45+0.1184=-1.3316$$
$$m_2=0.87-0.01(-31.08)=0.87+0.3108=1.1808$$
$$b=0.88-0.01(-5.18)=0.88+0.0518=0.9318$$

**After update 2:** $\mathbf m=[-1.3316,\ 1.1808]^T$, $b=0.9318$.

\newpage

# Page 4 — Update 3 (Writer 2)

Start: $\mathbf m=[-1.3316,\ 1.1808]^T$, $b=0.9318$.

**Step 1 – Matrix product**
$$X\mathbf m=\begin{bmatrix}(1)(-1.3316)+(3)(1.1808)\\(4)(-1.3316)+(10)(1.1808)\end{bmatrix}
=\begin{bmatrix}-1.3316+3.5424\\-5.3264+11.808\end{bmatrix}=\begin{bmatrix}2.2108\\6.4816\end{bmatrix}$$

**Step 2 – Predictions** $\hat{\mathbf y}=\begin{bmatrix}2.2108+0.9318\\6.4816+0.9318\end{bmatrix}=\begin{bmatrix}3.1426\\7.4134\end{bmatrix}$

**Step 3 – Error** $\mathbf e=\begin{bmatrix}3.1426-5\\7.4134-6\end{bmatrix}=\begin{bmatrix}-1.8574\\1.4134\end{bmatrix}$

**Step 4 – Cost** $J=\frac12\big((-1.8574)^2+(1.4134)^2\big)=\frac12(3.44993476+1.99769956)=\frac12(5.44763432)=2.72381716$

**Step 5 – Gradient w.r.t. m**
$$X^T\mathbf e=\begin{bmatrix}(1)(-1.8574)+(4)(1.4134)\\(3)(-1.8574)+(10)(1.4134)\end{bmatrix}
=\begin{bmatrix}-1.8574+5.6536\\-5.5722+14.134\end{bmatrix}=\begin{bmatrix}3.7962\\8.5618\end{bmatrix},\qquad
\frac{\partial J}{\partial \mathbf m}=\begin{bmatrix}3.7962\\8.5618\end{bmatrix}$$

**Step 6 – Gradient w.r.t. b** $\dfrac{\partial J}{\partial b}=1\times(-1.8574+1.4134)=-0.444$

**Step 7 – Update**
$$m_1=-1.3316-0.01(3.7962)=-1.3316-0.037962=-1.369562$$
$$m_2=1.1808-0.01(8.5618)=1.1808-0.085618=1.095182$$
$$b=0.9318-0.01(-0.444)=0.9318+0.00444=0.93624$$

**After update 3:** $\mathbf m=[-1.369562,\ 1.095182]^T$, $b=0.93624$.

**Check of the final values:**
$\hat{\mathbf y}=\begin{bmatrix}-1.369562+3.285546+0.93624\\-5.478248+10.95182+0.93624\end{bmatrix}=\begin{bmatrix}2.852224\\6.409812\end{bmatrix}$,
$\mathbf e=\begin{bmatrix}-2.147776\\0.409812\end{bmatrix}$,
$J=\frac12(4.612941746176+0.167945875344)=\frac12(4.78088762152)=2.39044381$

\newpage

# Page 5 — Summary and trend (Writer 2)

| Update | $\mathbf m$ before | $b$ before | $\hat{\mathbf y}$ | $\mathbf e$ | $J$ before | $\partial J/\partial\mathbf m$ | $\partial J/\partial b$ | $\mathbf m$ after | $b$ after |
|---|---|---|---|---|---|---|---|---|---|
| 1 | [−1, 2] | 1 | [6, 17] | [1, 11] | 61 | [45, 113] | 12 | [−1.45, 0.87] | 0.88 |
| 2 | [−1.45, 0.87] | 0.88 | [2.04, 3.78] | [−2.96, −2.22] | 6.845 | [−11.84, −31.08] | −5.18 | [−1.3316, 1.1808] | 0.9318 |
| 3 | [−1.3316, 1.1808] | 0.9318 | [3.1426, 7.4134] | [−1.8574, 1.4134] | 2.72381716 | [3.7962, 8.5618] | −0.444 | [−1.369562, 1.095182] | 0.93624 |

Cost after the 3rd update: $J = 2.39044381$.

**Trend — are m and b moving in a direction that reduces the error? Yes.**

1. $J$ falls after every update: $61 \to 6.845 \to 2.7238 \to 2.3904$ (a 96% drop in total).
2. Each parameter moves *against the sign of its gradient*: positive gradient → value decreases (update 1: $m_1, m_2, b$ all fall); negative gradient → value increases (update 2: all rise). That is exactly "downhill".
3. The first step is the largest because the first error was the largest ($\hat y_2 = 17$ vs $6$). As errors shrink, gradients shrink, and steps shrink ($|\Delta m_2|$: 1.13 → 0.3108 → 0.0856).
4. $m_2$ zig-zags ($2 \to 0.87 \to 1.1808 \to 1.0952$) and the error of point 2 changes sign ($+11 \to -2.22 \to +1.41$): $x_2 = 10$ makes the cost very steep along $m_2$, so $\alpha=0.01$ slightly overshoots, but each overshoot is smaller than the last — the zig-zag is damping, not growing.
5. The Python version (Part 4) reproduces every number above and, continued to 2000 updates, reaches $\mathbf m\approx[-2.2258,\ 1.0968]$, $b\approx3.9353$, $J\approx 0$, predictions $\approx[5, 6]$.
