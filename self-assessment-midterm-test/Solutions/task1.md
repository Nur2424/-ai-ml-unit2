# Phase 2 — Full Worked Solution

Let me solve each sub-question completely, with every calculation shown.

Our matrix to reference throughout:

$$\mathbf{X} = \begin{bmatrix} 0 & -5 & -2 \\ -2 & 2 & 4 \\ -2 & 0 & -3 \end{bmatrix}, \quad n = 3 \text{ samples}, \quad d = 3 \text{ features}$$

---

## Sub-question 1-1 | Dimensionality

Each row is one sample: $\mathbf{x}^{(1)} = [0, -5, -2]$, $\mathbf{x}^{(2)} = [-2, 2, 4]$, $\mathbf{x}^{(3)} = [-2, 0, -3]$

Each sample has **3 components** → it lives in $\mathbb{R}^3$ → dimensionality = **number of columns = 3**

### ✅ Answer: A. 3

**Why each option is wrong/right:**

| Option | Value | Verdict |
|--------|-------|---------|
| A. 3 | = number of columns = $d$ | ✅ Correct |
| B. 5 | no relation to this matrix | ❌ |
| C. 10 | no relation to this matrix | ❌ |
| D. 1 | would mean scalar samples | ❌ |
| E. 2 | would mean 2D samples | ❌ |

---

## Sub-question 1-2 | Empirical Mean $\boldsymbol{\mu}$

$$\boldsymbol{\mu} = \frac{1}{n}\sum_{i=1}^{n} \mathbf{x}^{(i)} = \frac{1}{3}\left(\mathbf{x}^{(1)} + \mathbf{x}^{(2)} + \mathbf{x}^{(3)}\right)$$

Average **each column separately:**

$$\mu_1 = \frac{0 + (-2) + (-2)}{3} = \frac{-4}{3} \approx -1.33$$

$$\mu_2 = \frac{-5 + 2 + 0}{3} = \frac{-3}{3} = -1.00$$

$$\mu_3 = \frac{-2 + 4 + (-3)}{3} = \frac{-1}{3} \approx -0.33$$

$$\boxed{\boldsymbol{\mu} = [-1.33,\ -1.00,\ -0.33]}$$

### ✅ Answer: A. [-1.33, -1., -0.33]

**Why each option is wrong/right:**

| Option | Verdict | Reason |
|--------|---------|--------|
| A. [-1.33, -1., -0.33] | ✅ Correct | Exact column-wise average |
| B. [-2.33, -1.66, 1] | ❌ | Wrong arithmetic |
| C. [1.33, 1., 1.33] | ❌ | Signs flipped, wrong $\mu_3$ |
| D. [1.33, -1., 1.33] | ❌ | $\mu_1$ and $\mu_3$ signs flipped |
| E. [-1, -1.33, 1.33] | ❌ | Values shuffled and wrong signs |

---

## Sub-question 1-3 | Sum of $\boldsymbol{\Sigma}$ minus Trace of $\boldsymbol{\Sigma}$

This requires 3 steps: **center the data → compute $\boldsymbol{\Sigma}$ → compute the answer.**

---

### Step 1 — Center the data (compute $\tilde{\mathbf{X}} = \mathbf{X} - \boldsymbol{\mu}$)

Subtract $\boldsymbol{\mu} = [-1.33,\ -1.00,\ -0.33]$ from every row:

$$\tilde{\mathbf{x}}^{(1)} = [0 - (-1.33),\ \ -5 - (-1),\ \ -2 - (-0.33)] = [1.33,\ -4,\ -1.67]$$

$$\tilde{\mathbf{x}}^{(2)} = [-2 - (-1.33),\ \ 2 - (-1),\ \ 4 - (-0.33)] = [-0.67,\ 3,\ 4.33]$$

$$\tilde{\mathbf{x}}^{(3)} = [-2 - (-1.33),\ \ 0 - (-1),\ \ -3 - (-0.33)] = [-0.67,\ 1,\ -2.67]$$

So the centered matrix is:

$$\tilde{\mathbf{X}} = \begin{bmatrix} 1.33 & -4 & -1.67 \\ -0.67 & 3 & 4.33 \\ -0.67 & 1 & -2.67 \end{bmatrix}$$

---

### Step 2 — Compute $\boldsymbol{\Sigma} = \frac{1}{n}\tilde{\mathbf{X}}^\top \tilde{\mathbf{X}}$

Each entry $\Sigma_{jk} = \frac{1}{3}\sum_{i=1}^{3} \tilde{x}_j^{(i)} \cdot \tilde{x}_k^{(i)}$

**Diagonal entries (variances):**

$$\Sigma_{11} = \frac{1}{3}\left[(1.33)^2 + (-0.67)^2 + (-0.67)^2\right] = \frac{1.77 + 0.44 + 0.44}{3} = \frac{2.66}{3} \approx 0.89$$

$$\Sigma_{22} = \frac{1}{3}\left[(-4)^2 + 3^2 + 1^2\right] = \frac{16 + 9 + 1}{3} = \frac{26}{3} \approx 8.67$$

$$\Sigma_{33} = \frac{1}{3}\left[(-1.67)^2 + (4.33)^2 + (-2.67)^2\right] = \frac{2.78 + 18.74 + 7.11}{3} = \frac{28.63}{3} \approx 9.54$$

**Off-diagonal entries (covariances):**

$$\Sigma_{12} = \frac{1}{3}\left[(1.33)(-4) + (-0.67)(3) + (-0.67)(1)\right] = \frac{-5.33 - 2 - 0.67}{3} = \frac{-8}{3} \approx -2.67$$

$$\Sigma_{13} = \frac{1}{3}\left[(1.33)(-1.67) + (-0.67)(4.33) + (-0.67)(-2.67)\right] = \frac{-2.22 - 2.89 + 1.78}{3} = \frac{-3.33}{3} \approx -1.11$$

$$\Sigma_{23} = \frac{1}{3}\left[(-4)(-1.67) + (3)(4.33) + (1)(-2.67)\right] = \frac{6.67 + 13 - 2.67}{3} = \frac{17}{3} \approx 5.67$$

The full covariance matrix (symmetric, so $\Sigma_{jk} = \Sigma_{kj}$):

$$\boldsymbol{\Sigma} \approx \begin{bmatrix} 0.89 & -2.67 & -1.11 \\ -2.67 & 8.67 & 5.67 \\ -1.11 & 5.67 & 9.54 \end{bmatrix}$$

---

### Step 3 — Compute the answer

**Sum of ALL elements:**

$$\text{sum} = 0.89 + 8.67 + 9.54 + 2(-2.67) + 2(-1.11) + 2(5.67)$$
$$= 19.1 + (-5.33) + (-2.22) + 11.33 = 22.89$$

**Trace** (sum of diagonal only):

$$\text{tr}(\boldsymbol{\Sigma}) = 0.89 + 8.67 + 9.54 = 19.10$$

**Final answer:**

$$\text{sum}(\boldsymbol{\Sigma}) - \text{tr}(\boldsymbol{\Sigma}) = 22.89 - 19.10 = \boxed{3.77}$$

> 💡 Notice this equals the **sum of all off-diagonal elements** — exactly the conceptual shortcut from Phase 1!

### ✅ Answer: E. 3.77

**Why each option is wrong/right:**

| Option | Verdict | Reason |
|--------|---------|--------|
| A. 5.11 | ❌ | Likely arithmetic error in covariance entries |
| B. 6.11 | ❌ | Likely used wrong centering |
| C. -16.44 | ❌ | Sign error, possibly subtracted in wrong order |
| D. 16.44 | ❌ | Absolute value of C — double sign mistake |
| E. 3.77 | ✅ Correct | Sum of all off-diagonal elements |

---
---

Rebuild Step 2 from scratch, much more clearly. The key issue is understanding **what operation produces each cell** of $\boldsymbol{\Sigma}$.

---

## The Core Idea: How $\boldsymbol{\Sigma}$ is built

$$\boldsymbol{\Sigma} = \frac{1}{n}\tilde{\mathbf{X}}^\top \tilde{\mathbf{X}}$$

This means **each entry** $\Sigma_{jk}$ = the **dot product of column $j$ and column $k$** of $\tilde{\mathbf{X}}$, divided by $n=3$.

$$\boxed{\Sigma_{jk} = \frac{1}{3}\sum_{i=1}^{3} \tilde{x}_j^{(i)} \cdot \tilde{x}_k^{(i)}}$$

Think of it as: *"pair up the two columns, multiply element by element, sum, divide by 3."*

---

## Our centered matrix $\tilde{\mathbf{X}}$ (using exact fractions)

Using $\boldsymbol{\mu} = [-\frac{4}{3},\ -1,\ -\frac{1}{3}]$:

$$\tilde{\mathbf{X}} = \begin{bmatrix} \frac{4}{3} & -4 & -\frac{5}{3} \\[6pt] -\frac{2}{3} & 3 & \frac{13}{3} \\[6pt] -\frac{2}{3} & 1 & -\frac{8}{3} \end{bmatrix}$$

Label the columns:

$$\mathbf{c}_1 = \begin{bmatrix}\frac{4}{3} \\ -\frac{2}{3} \\ -\frac{2}{3}\end{bmatrix}, \quad \mathbf{c}_2 = \begin{bmatrix}-4 \\ 3 \\ 1\end{bmatrix}, \quad \mathbf{c}_3 = \begin{bmatrix}-\frac{5}{3} \\ \frac{13}{3} \\ -\frac{8}{3}\end{bmatrix}$$

---

## Computing every entry of $\boldsymbol{\Sigma}$ — one by one

Since $\boldsymbol{\Sigma}$ is **symmetric** ($\Sigma_{jk} = \Sigma_{kj}$), we only need 6 unique entries.

---

**$\Sigma_{11}$ — dot $\mathbf{c}_1$ with itself:**

$$\Sigma_{11} = \frac{1}{3}\left[\left(\tfrac{4}{3}\right)^2 + \left(-\tfrac{2}{3}\right)^2 + \left(-\tfrac{2}{3}\right)^2\right] = \frac{1}{3}\left[\frac{16}{9} + \frac{4}{9} + \frac{4}{9}\right] = \frac{1}{3} \cdot \frac{24}{9} = \frac{8}{9} \approx 0.89$$

---

**$\Sigma_{22}$ — dot $\mathbf{c}_2$ with itself:**

$$\Sigma_{22} = \frac{1}{3}\left[(-4)^2 + 3^2 + 1^2\right] = \frac{1}{3}\left[16 + 9 + 1\right] = \frac{26}{3} \approx 8.67$$

---

**$\Sigma_{33}$ — dot $\mathbf{c}_3$ with itself:**

$$\Sigma_{33} = \frac{1}{3}\left[\left(-\tfrac{5}{3}\right)^2 + \left(\tfrac{13}{3}\right)^2 + \left(-\tfrac{8}{3}\right)^2\right] = \frac{1}{3}\left[\frac{25}{9} + \frac{169}{9} + \frac{64}{9}\right] = \frac{1}{3} \cdot \frac{258}{9} = \frac{86}{9} \approx 9.56$$

---

**$\Sigma_{12}$ — dot $\mathbf{c}_1$ with $\mathbf{c}_2$:**

$$\Sigma_{12} = \frac{1}{3}\left[\tfrac{4}{3} \cdot (-4) + \left(-\tfrac{2}{3}\right) \cdot 3 + \left(-\tfrac{2}{3}\right) \cdot 1\right] = \frac{1}{3}\left[-\frac{16}{3} - \frac{6}{3} - \frac{2}{3}\right] = \frac{1}{3} \cdot \left(-\frac{24}{3}\right) = -\frac{8}{3} \approx -2.67$$

---

**$\Sigma_{13}$ — dot $\mathbf{c}_1$ with $\mathbf{c}_3$:**

$$\Sigma_{13} = \frac{1}{3}\left[\tfrac{4}{3} \cdot \left(-\tfrac{5}{3}\right) + \left(-\tfrac{2}{3}\right) \cdot \tfrac{13}{3} + \left(-\tfrac{2}{3}\right) \cdot \left(-\tfrac{8}{3}\right)\right] = \frac{1}{3}\left[-\frac{20}{9} - \frac{26}{9} + \frac{16}{9}\right] = \frac{1}{3} \cdot \left(-\frac{30}{9}\right) = -\frac{10}{9} \approx -1.11$$

---

**$\Sigma_{23}$ — dot $\mathbf{c}_2$ with $\mathbf{c}_3$:**

$$\Sigma_{23} = \frac{1}{3}\left[(-4)\cdot\left(-\tfrac{5}{3}\right) + 3 \cdot \tfrac{13}{3} + 1 \cdot \left(-\tfrac{8}{3}\right)\right] = \frac{1}{3}\left[\frac{20}{3} + \frac{39}{3} - \frac{8}{3}\right] = \frac{1}{3} \cdot \frac{51}{3} = \frac{17}{3} \approx 5.67$$

---

## The full $\boldsymbol{\Sigma}$ matrix

$$\boldsymbol{\Sigma} = \begin{bmatrix} 0.89 & -2.67 & -1.11 \\ -2.67 & 8.67 & 5.67 \\ -1.11 & 5.67 & 9.56 \end{bmatrix}$$

> 🔑 Notice it's **perfectly symmetric** — this is always your sanity check!

---

## Then the final calculation:

$$\text{tr}(\boldsymbol{\Sigma}) = 0.89 + 8.67 + 9.56 = 19.12$$

$$\text{sum of all elements} = 19.12 + 2(-2.67) + 2(-1.11) + 2(5.67) = 19.12 + 3.78 = 22.90$$

$$22.90 - 19.12 = \boxed{3.78 \approx 3.77} \checkmark$$

---
