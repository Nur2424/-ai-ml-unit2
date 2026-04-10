# Linear Algebra — 8 Foundations, Rebuilt With ML Examples

Let me go one by one. Each foundation gets: a clear explanation, a concrete example, and exactly how it shows up in machine learning.

---

# 🧱 Foundation 1 — Vectors

A vector is an **ordered list of numbers**. Order matters — swapping two numbers gives a different vector.

$$\mathbf{z} = \begin{bmatrix} 3 \\ -1 \\ 2 \end{bmatrix}$$

Think of each number as answering one question about a data point. For example, describing a house:

$$\mathbf{x} = \begin{bmatrix} 120 \\ 3 \\ 2 \end{bmatrix} \leftarrow \begin{array}{l} \text{area (m²)} \\ \text{bedrooms} \\ \text{bathrooms} \end{array}$$

This vector **lives in $\mathbb{R}^3$** — 3-dimensional space — because it has 3 numbers.

<img width="887" height="300" alt="image" src="https://github.com/user-attachments/assets/9b61f4bb-792c-4025-a218-57ca89024b63" />


**ML connection:** Every single data point in any ML dataset is a vector. An image of 28×28 pixels = a vector in $\mathbb{R}^{784}$.

---

# 🧱 Foundation 2 — Matrices

A matrix is a **table of numbers** with rows and columns. It is written as $\mathbf{X} \in \mathbb{R}^{d \times N}$.

In ML, we stack all our data points into one matrix — that is the **design matrix**:

$$\mathbf{X} = \begin{bmatrix} | & | & | \\ \mathbf{x}_1 & \mathbf{x}_2 & \mathbf{x}_3 \\ | & | & | \end{bmatrix} = \begin{bmatrix} 50 & 100 & 150 \\ 1 & 2 & 3 \end{bmatrix} \in \mathbb{R}^{2 \times 3}$$

Here: $d = 2$ features (rows), $N = 3$ samples (columns).

<img width="823" height="292" alt="image" src="https://github.com/user-attachments/assets/26c1e649-2038-4a38-a085-bec4d254b7ed" />


**ML connection:** The design matrix $\mathbf{X}$ **is** your entire dataset in one object. Every ML algorithm reads it in this form.

---

# 🧱 Foundation 3 — Transpose

The transpose $\mathbf{X}^\top$ simply **flips** the matrix. Rows become columns, columns become rows.

$$\mathbf{X} = \begin{bmatrix} 50 & 100 & 150 \\ 1 & 2 & 3 \end{bmatrix} \in \mathbb{R}^{2 \times 3} \quad\xrightarrow{\text{transpose}}\quad \mathbf{X}^\top = \begin{bmatrix} 50 & 1 \\ 100 & 2 \\ 150 & 3 \end{bmatrix} \in \mathbb{R}^{3 \times 2}$$

The size notation flips too: $\mathbb{R}^{d \times N}$ becomes $\mathbb{R}^{N \times d}$.

<img width="887" height="262" alt="image" src="https://github.com/user-attachments/assets/0f49f57c-25d2-40f5-a749-05d033395a1c" />


**ML connection:** The transpose appears constantly — in the projection formula $\mathbf{X}^\top\mathbf{X}$, in computing covariance matrices, in gradient calculations. It is the most frequently used operation in all of ML math.

---

# 🧱 Foundation 4 — The Norm

The norm $\|\mathbf{v}\|$ is the **length of a vector** — measured like a ruler.

$$\|\mathbf{v}\| = \sqrt{v_1^2 + v_2^2 + \cdots + v_d^2}$$

This is just the Pythagorean theorem extended to $d$ dimensions.

**Example with two houses:**

$$\mathbf{a} = \begin{bmatrix}3\\4\end{bmatrix} \implies \|\mathbf{a}\| = \sqrt{3^2 + 4^2} = \sqrt{9+16} = \sqrt{25} = 5$$

<img width="875" height="297" alt="image" src="https://github.com/user-attachments/assets/33d70af0-41b8-403e-b07b-b11f98a28769" />


**ML connection:** The reconstruction error $\|\mathbf{z}_{\text{prj}} - \mathbf{z}\|$ directly uses the norm. Loss functions like mean squared error are norms squared. Whenever ML measures "how far off", it uses a norm.

---

# 🧱 Foundation 5 — Dot Product

The dot product multiplies two vectors **element by element, then sums everything** into one number.

$$\mathbf{a} \cdot \mathbf{b} = \mathbf{a}^\top\mathbf{b} = a_1 b_1 + a_2 b_2 + \cdots + a_d b_d$$

**Geometric meaning:** it measures **how much two vectors agree in direction**.

$$\mathbf{a}^\top\mathbf{b} = \|\mathbf{a}\| \cdot \|\mathbf{b}\| \cdot \cos(\theta)$$

where $\theta$ is the angle between them.

<img width="878" height="295" alt="image" src="https://github.com/user-attachments/assets/1a7217fc-54e9-4afe-b9df-e0282ba45b1f" />


**ML connection:** The dot product is the core computation of **every neuron** in a neural network ($\mathbf{w}^\top\mathbf{x}$). It also powers the covariance matrix and the projection formula. It is the single most important operation in ML.

> 🔑 **Zero dot product = perpendicular = orthogonal.** This is the condition used in projection: the error vector $(\mathbf{z} - \mathbf{z}_{\text{prj}})$ must be perpendicular to every column of $\mathbf{X}$, so $\mathbf{X}^\top(\mathbf{z} - \mathbf{z}_{\text{prj}}) = \mathbf{0}$.

---

# 🧱 Foundation 6 — Matrix Inverse

For regular numbers: inverse of $3$ is $\frac{1}{3}$, because $3 \times \frac{1}{3} = 1$.

For matrices: the inverse of $\mathbf{A}$ is written $\mathbf{A}^{-1}$, and it satisfies:

$$\mathbf{A} \cdot \mathbf{A}^{-1} = \mathbf{I}$$

where $\mathbf{I}$ is the **identity matrix** — the matrix version of the number $1$:

$$\mathbf{I}_3 = \begin{bmatrix}1&0&0\\0&1&0\\0&0&1\end{bmatrix}, \quad \text{and} \quad \mathbf{I}\mathbf{v} = \mathbf{v} \text{ always}$$

<img width="1440" height="424" alt="image" src="https://github.com/user-attachments/assets/c951be66-19e2-4444-9982-4aa41898cb7d" />


**Why does the inverse exist in our problem?**

In Task 2, we compute $(\mathbf{X}^\top\mathbf{X})^{-1}$. This inverse exists only because the problem states the training points are **linearly independent**. If they were not, the inverse would not exist and the formula would break.

**ML connection:** The inverse appears in the projection formula, in solving linear systems, and in the normal equations of linear regression: $\mathbf{w} = (\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top\mathbf{y}$.

---

# 🧱 Foundation 7 — Linear Independence and Span

**Linear combination:** you multiply each vector by a number and add them up.

$$\alpha_1 \mathbf{x}_1 + \alpha_2 \mathbf{x}_2 = \begin{bmatrix}?\\ ?\end{bmatrix}$$

**Span:** the set of all possible vectors you can reach by all possible linear combinations.

<img width="1440" height="508" alt="image" src="https://github.com/user-attachments/assets/0911220e-de08-4f2b-bbfb-c05e7f4e7447" />


**ML connection:** Independent columns are required for the inverse $(\mathbf{X}^\top\mathbf{X})^{-1}$ to exist. In Task 2, the problem explicitly states "training points are not linearly dependent" — this is what guarantees the projection formula works. If two training samples were identical, the formula would break down.

---

# 🧱 Foundation 8 — What $d > N$ Means Geometrically

This is the most important foundation for Task 2. Let's build up from the simplest case.

<img width="1440" height="656" alt="image" src="https://github.com/user-attachments/assets/40b13179-c880-46c7-bb1f-c59f26b8ca44" />

**The three cases summarized:**

| Setup | Subspace | What happens to $\mathbf{z}$? |
|-------|----------|-------------------------------|
| $d > N$ | Smaller than full space | $\mathbf{z}$ may float outside → projection needed |
| $d = N$, orthonormal | Equals full space $\mathbb{R}^d$ | $\mathbf{z}$ always inside → $\mathbf{z}_{\text{prj}} = \mathbf{z}$ |
| $N = 1$ | A single line | $\mathbf{z}$ projected onto that line |

**ML connection:** This is the setup of **PCA** (Principal Component Analysis). You have high-dimensional data ($d$ large) but only $N$ samples. The samples span a low-dimensional subspace. PCA finds that subspace and projects everything onto it to reduce dimensions.

---

## 🗺️ How All 8 Foundations Connect to Task 2

<img width="1440" height="856" alt="image" src="https://github.com/user-attachments/assets/410b62ba-0ca1-4083-bd88-5a7209062812" />


---

## Quick Cheatsheet — All 8 in One Table

| # | Concept | Formula | Used in Task 2 for |
|---|---------|---------|-------------------|
| F1 | Vector | $\mathbf{v} \in \mathbb{R}^d$ | each sample $\mathbf{x}_i$, the new point $\mathbf{z}$ |
| F2 | Matrix | $\mathbf{X} \in \mathbb{R}^{d \times N}$ | storing all training samples |
| F3 | Transpose | $\mathbf{X} \in \mathbb{R}^{d \times N} \to \mathbf{X}^\top \in \mathbb{R}^{N \times d}$ | building $\mathbf{X}^\top\mathbf{X}$ |
| F4 | Norm | $\|\mathbf{v}\| = \sqrt{\sum v_i^2}$ | measuring reconstruction error |
| F5 | Dot product | $\mathbf{a}^\top\mathbf{b} = \sum a_i b_i$ | orthogonality condition, covariance |
| F6 | Inverse | $\mathbf{A}\mathbf{A}^{-1} = \mathbf{I}$ | $(\mathbf{X}^\top\mathbf{X})^{-1}$ in projection formula |
| F7 | Span / independence | all combos of columns | subspace Col($\mathbf{X}$), why inverse exists |
| F8 | $d > N$ geometry | subspace smaller than $\mathbb{R}^d$ | why $\mathbf{z}$ may lie outside the subspace |

---
---

# Theory for Task 2 — Built on Your 8 Foundations

Every concept below will reference the foundations you just learned. No new math from scratch — only connections.

---

## Concept 1 — The Column Space (what "subspace spanned by X" means)

You know from **F7 (Span)** that the span is all possible linear combinations of the columns.

The **column space** of $\mathbf{X}$, written $\text{Col}(\mathbf{X})$, is exactly that:

$$\text{Col}(\mathbf{X}) = \left\{ \mathbf{X}\boldsymbol{\alpha} \ \Big| \ \boldsymbol{\alpha} \in \mathbb{R}^N \right\}$$

In plain words: every vector you can build by mixing the $N$ columns of $\mathbf{X}$ with any weights $\boldsymbol{\alpha} = [\alpha_1, \alpha_2, \dots, \alpha_N]$.> 🔑 

<img width="1440" height="550" alt="image" src="https://github.com/user-attachments/assets/90fca04c-c5df-41d9-8190-d8fc7f143adc" />

🔑 **The subspace spanned by X = Col(X) = all possible Xα.** This is what the problem means by "subspace spanned by X."

---

## Concept 2 — The Projection Formula (for 2-1)

**Foundations used: F2, F3, F5, F6, F7**

We want to find the closest point in $\text{Col}(\mathbf{X})$ to $\mathbf{z}$. Call it $\mathbf{z}_{\text{prj}}$.

Since $\mathbf{z}_{\text{prj}}$ must be inside $\text{Col}(\mathbf{X})$, we know it has the form:

$$\mathbf{z}_{\text{prj}} = \mathbf{X}\boldsymbol{\alpha} \quad \text{for some unknown } \boldsymbol{\alpha}$$

**How do we find $\boldsymbol{\alpha}$?** Using the perpendicularity condition from **F5 (dot product)**:

The error vector $(\mathbf{z} - \mathbf{z}_{\text{prj}})$ must be **perpendicular to every column of X**:

$$\mathbf{X}^\top \underbrace{(\mathbf{z} - \mathbf{X}\boldsymbol{\alpha})}_{\text{error vector}} = \mathbf{0}$$> 

<img width="1440" height="682" alt="image" src="https://github.com/user-attachments/assets/0aab92f1-690f-4c52-9bb9-5aa97671a9e7" />


🔑 **One line to remember:** $\mathbf{P} = \mathbf{X}(\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top$ is the projection matrix. Multiply any $\mathbf{z}$ by $\mathbf{P}$ to get its projection.

---

## Concept 3 — Dimensionality of $\mathbf{z}_{\text{prj}}$ (for 2-2)

**Foundations used: F1, F2, F8**

This is a tricky distinction many students get wrong. There are **two different meanings** of "dimension" here:> 

<img width="1440" height="530" alt="image" src="https://github.com/user-attachments/assets/7e52f05a-4e2f-4d85-a4cb-4d75423b755c" />


🔑 **Key insight:** $\mathbf{z}_{\text{prj}}$ lives on a small surface (the subspace), but it is still a vector with $d$ numbers. $\mathbf{P}$ is $d \times d$, $\mathbf{z}$ is in $\mathbb{R}^d$, so $\mathbf{P}\mathbf{z}$ is in $\mathbb{R}^d$. **Answer = $d$.**

---

## Concept 4 — Reconstruction Error = 0 When z is in the Subspace (for 2-3)

**Foundations used: F4, F5, F7**

The reconstruction error is $\|\mathbf{z}_{\text{prj}} - \mathbf{z}\|$ — the **norm** (F4) of the difference.

**The critical theorem:**

> If $\mathbf{z}$ is already a linear combination of the columns of $\mathbf{X}$, then projecting $\mathbf{z}$ does not move it at all.

**Why?** Because projection finds the closest point in $\text{Col}(\mathbf{X})$ to $\mathbf{z}$. If $\mathbf{z}$ is already there, the closest point is $\mathbf{z}$ itself.

$$\mathbf{z} \in \text{Col}(\mathbf{X}) \implies \mathbf{z}_{\text{prj}} = \mathbf{z} \implies \|\mathbf{z}_{\text{prj}} - \mathbf{z}\| = \|\mathbf{0}\| = 0$$

**In question 2-3:** $\mathbf{z} = 100\mathbf{x}_1 + 5\mathbf{x}_{50} - \mathbf{x}_{100}$ — this is exactly a linear combination of training samples (columns of $\mathbf{X}$), so $\mathbf{z} \in \text{Col}(\mathbf{X})$, so the error is zero. 
<img width="1440" height="488" alt="image" src="https://github.com/user-attachments/assets/e4875de5-a024-40eb-be19-65b78080bfb7" />


## Concept 5 — Orthonormal Columns Simplify Everything (for 2-4)

**Foundations used: F5, F6**

When columns of $\mathbf{X}$ are orthonormal, two conditions hold:

$$\|\mathbf{x}_i\| = 1 \quad \text{(unit length)} \qquad \mathbf{x}_i^\top\mathbf{x}_j = 0 \text{ for } i \neq j \quad \text{(perpendicular)}$$

Now look at what $\mathbf{X}^\top\mathbf{X}$ becomes. Each entry $(i,j)$ of this matrix is the dot product $\mathbf{x}_i^\top\mathbf{x}_j$:
<img width="1440" height="636" alt="image" src="https://github.com/user-attachments/assets/0322aa21-0780-4927-b2aa-69e38be3bbc2" />


## Concept 6 — When d = N and Orthonormal: Full Space (for 2-5)

**Foundations used: F6, F7, F8**

When $d = N$ AND columns are orthonormal, $\mathbf{X}$ becomes a **square orthogonal matrix**. Now one more magical thing happens:

$$\mathbf{X}\mathbf{X}^\top = \mathbf{I}_d \quad \text{(not just } \mathbf{X}^\top\mathbf{X} = \mathbf{I}_N\text{)}$$

This means the projection matrix becomes:

$$\mathbf{P} = \mathbf{X}\mathbf{X}^\top = \mathbf{I}_d$$

<img width="1440" height="592" alt="image" src="https://github.com/user-attachments/assets/fc6e2d77-203b-4b65-b98f-d54730be42fa" />


## Full Theory Summary — Task 2 at a Glance 

<img width="1440" height="720" alt="image" src="https://github.com/user-attachments/assets/9a84c1f2-d2b4-4669-a979-4a5405f5fbf3" />
