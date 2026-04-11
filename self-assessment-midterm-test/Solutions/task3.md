# Phase 2 — Full Worked Solutions

One sub-question at a time. No rushing.

---

# Sub-question 3-1
## "How do we center the point cloud X to get X̄?"

**Options:**
- A. We compute PCA
- B. We compute the average and subtract it from the point cloud
- C. We compute the average and divide the point cloud with it
- D. We compute the std. deviation and divide the point cloud
- E. We compute the average and sum to the point cloud

---

### Step 1 — What does centering mean visually?

Look at figure (b) vs figure (c) in your image. The shape of the blob is **identical** — same tilt, same spread. The only difference is **where it sits**. In (b) the cross × is off the origin. In (c) the × sits exactly at the origin.

This tells you centering = **sliding** the cloud, not reshaping it.

---

### Step 2 — The math

The mean (average point) is:

$$\boldsymbol{\mu} = \frac{1}{N}\sum_{i=1}^{N} \mathbf{x}_i$$

Centering means subtracting this from every point:

$$\bar{\mathbf{x}}_i = \mathbf{x}_i - \boldsymbol{\mu}$$

**Concrete example** with 3 points:

$$\mathbf{x}_1 = \begin{bmatrix}3\\5\end{bmatrix}, \quad \mathbf{x}_2 = \begin{bmatrix}5\\7\end{bmatrix}, \quad \mathbf{x}_3 = \begin{bmatrix}7\\9\end{bmatrix}$$

$$\boldsymbol{\mu} = \frac{1}{3}\left(\begin{bmatrix}3\\5\end{bmatrix} + \begin{bmatrix}5\\7\end{bmatrix} + \begin{bmatrix}7\\9\end{bmatrix}\right) = \begin{bmatrix}5\\7\end{bmatrix}$$

$$\bar{\mathbf{x}}_1 = \begin{bmatrix}3-5\\5-7\end{bmatrix} = \begin{bmatrix}-2\\-2\end{bmatrix}, \quad \bar{\mathbf{x}}_2 = \begin{bmatrix}0\\0\end{bmatrix}, \quad \bar{\mathbf{x}}_3 = \begin{bmatrix}2\\2\end{bmatrix}$$

The new mean of the centered cloud = $\mathbf{0}$. Always.

---

### Step 3 — Check every option

<img width="1440" height="736" alt="image" src="https://github.com/user-attachments/assets/9d2393db-4887-4365-a864-e086ef8b3b8d" />

### ✅ Answer: B

> 🔑 **One line:** Centering = subtract the mean. Nothing more. The cloud shape stays identical, only its position moves to the origin.

---
---


# Sub-question 3-2
## "Write the numpy one-liner for centering, given $\mathbf{X} \in \mathbb{R}^{N \times 2}$"

**Options:**
- A. `X - X.mean(axis=1)`
- B. `X + X.mean(axis=1)`
- C. `X - X.mean(axis=0)`
- D. `X + X.mean(axis=0)`
- E. `X / X.mean(axis=1)`

---

### Step 1 — Recall what we need

We need to subtract the **column-wise mean** from every row. The mean must be computed **per feature** (per column), not per sample.

From Phase 1 theory:
- `axis=0` → collapses rows → gives **one value per column** ✓
- `axis=1` → collapses columns → gives **one value per row** ✗

---

### Step 2 — Trace through with concrete numbers

$$\mathbf{X} = \begin{bmatrix} 2 & 6 \\ 4 & 8 \\ 6 & 10 \end{bmatrix}$$

`X.mean(axis=0)` = $[4, 8]$ — one mean per column. This is $\boldsymbol{\mu}$.

`X - X.mean(axis=0)`:

$$\begin{bmatrix} 2-4 & 6-8 \\ 4-4 & 8-8 \\ 6-4 & 10-8 \end{bmatrix} = \begin{bmatrix} -2 & -2 \\ 0 & 0 \\ 2 & 2 \end{bmatrix}$$

Check: column means of result = $[0, 0]$ ✓ — centered correctly.

Now check `X.mean(axis=1)` = $[4, 6, 8]$ — one mean per row. This mixes features together — meaningless for centering.

---

### Step 3 — Check every option

<img width="1440" height="736" alt="image" src="https://github.com/user-attachments/assets/7f0aa459-4996-4afb-8225-7b8100405513" />


### ✅ Answer: C

> 🔑 **Exam shortcut:** Whenever you center data, always `axis=0`. It gives one mean per feature column, which is exactly what gets subtracted.

---
---

# Sub-question 3-3
## "Which transformation turns figure (c) into figure (d)?"

This is the most important and subtle sub-question. Let me go very carefully.

**Options:**
- A. Apply $\mathbf{U}^\top\mathbf{x}$, putting eigenvectors with **highest** eigenvalues in the **second** column
- B. Apply $\boldsymbol{\Sigma}^{-1/2}\mathbf{U}^\top\mathbf{x}$
- C. Apply $\mathbf{U}^\top\mathbf{U}\mathbf{x}$
- D. Apply $\mathbf{U}\mathbf{U}\mathbf{x}$
- E. Apply $\mathbf{U}^\top\mathbf{x}$, putting eigenvectors with **highest** eigenvalues in the **first** column

---

### Step 1 — Look at the figures carefully

From figure (c) to figure (d):
- The blob was **diagonal** (tilted at ~45°)
- After transformation it is **vertical** (aligned with $x_2$ axis)
- The blob is **taller than wide** — meaning the direction of most variance is now along $x_2$

This tells us two things happened:
1. The data was **rotated** — the tilt is gone
2. The longest direction now points **upward** (along the vertical axis)

---

### Step 2 — What does $\mathbf{U}^\top\mathbf{x}$ do?

$\mathbf{U}^\top$ is a rotation matrix. It rotates the coordinate system so the eigenvectors become the new axes.

The result depends critically on **which column of $\mathbf{U}$ gets which eigenvector**.

<img width="1440" height="614" alt="image" src="https://github.com/user-attachments/assets/84546181-9396-464f-9617-52e552c29859" />

---

### Step 3 — Why does column ordering matter?

When you apply $\mathbf{U}^\top\mathbf{x}$:
- The **first row** of $\mathbf{U}^\top$ = first column of $\mathbf{U}$ → becomes the **new $x_1$ axis**
- The **second row** of $\mathbf{U}^\top$ = second column of $\mathbf{U}$ → becomes the **new $x_2$ axis**

Figure (d) shows the blob is **vertical** — most variance is along $x_2$. So the eigenvector with the **largest eigenvalue** must map to the **$x_2$ axis** = must be the **second column** of $\mathbf{U}$.

This is exactly what option **A** says.

---

### Step 4 — What does $\boldsymbol{\Sigma}^{-1/2}\mathbf{U}^\top\mathbf{x}$ do differently?

This is **whitening** — it goes one step further than option A:

$$\boldsymbol{\Sigma}^{-1/2} = \begin{bmatrix} \frac{1}{\sqrt{\lambda_1}} & 0 \\ 0 & \frac{1}{\sqrt{\lambda_2}} \end{bmatrix}$$

After rotating with $\mathbf{U}^\top$, the blob is still elongated (tall ellipse). Whitening then **rescales** each axis by $\frac{1}{\sqrt{\lambda}}$, squishing the blob into a **circle**. Figure (d) still looks like an elongated ellipse — not a circle. So whitening was NOT applied here.

---

### Step 5 — Check every option

<img width="1440" height="826" alt="image" src="https://github.com/user-attachments/assets/59f34cf7-3a05-4caa-8e1c-d9699978ef33" />


### ✅ Answer: A

> 🔑 **The subtle point:** A vs E is purely about column ordering. The transformation $\mathbf{U}^\top\mathbf{x}$ is the same in both — but which column of $\mathbf{U}$ holds the biggest eigenvector determines which axis the blob aligns with. Read the figure: vertical blob = largest variance on $x_2$ axis = largest eigenvector in **second** column.

---
---

# Sub-question 3-4
## "After the transformation in figure (d), what happens to the covariance matrix?"

**Options:**
- A. Identity
- B. Square and symmetric
- C. A diagonal matrix; consequently the off-diagonal Pearson correlation coefficients are zero
- D. Anti-diagonal and correlated
- E. Diagonal but still correlated

---

### Step 1 — Compute the new covariance mathematically

Before transformation, the covariance matrix is $\boldsymbol{\Sigma}$ with off-diagonal entries (correlation exists — the blob is tilted).

After applying $\mathbf{U}^\top$, the new covariance is:

$$\boldsymbol{\Sigma}_{\text{new}} = \mathbf{U}^\top \boldsymbol{\Sigma} \mathbf{U}$$

Since $\boldsymbol{\Sigma}\mathbf{U} = \mathbf{U}\boldsymbol{\Lambda}$ (definition of eigenvectors), this becomes:

$$\boldsymbol{\Sigma}_{\text{new}} = \mathbf{U}^\top \mathbf{U} \boldsymbol{\Lambda} = \mathbf{I}\boldsymbol{\Lambda} = \boldsymbol{\Lambda}$$

Where $\boldsymbol{\Lambda}$ is the **diagonal matrix of eigenvalues**:

$$\boldsymbol{\Lambda} = \begin{bmatrix} \lambda_1 & 0 \\ 0 & \lambda_2 \end{bmatrix}$$---

### Step 2 — Check every option

<img width="1440" height="826" alt="image" src="https://github.com/user-attachments/assets/3f3ed580-a386-4257-9d70-74cba00194d9" />

### ✅ Answer: C

> 🔑 **The key chain:** PCA rotation → covariance becomes $\boldsymbol{\Lambda}$ (diagonal) → off-diagonal = 0 → Pearson correlation = 0 → features decorrelated. This is the entire point of PCA.

---

## Full Answer Key — Question 3

| Sub-Q | Answer | Core reason |
|-------|--------|-------------|
| 3-1 | B | Centering = subtract the mean from every point |
| 3-2 | C | `X - X.mean(axis=0)` — axis=0 gives per-column mean |
| 3-3 | A | $\mathbf{U}^\top\mathbf{x}$ rotation, largest eigenvector in **second** column → vertical blob |
| 3-4 | C | New covariance = $\boldsymbol{\Lambda}$ (diagonal) → off-diagonal = 0 → zero Pearson correlations |

---
