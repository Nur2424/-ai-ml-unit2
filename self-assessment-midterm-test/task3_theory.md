# Phase 1 — Theory Background

Let me build everything from scratch, concept by concept, tied directly to the figures you uploaded.

---

## First — What Are We Looking At in the Figures?

Looking at the image:

- **(b)** — the original point cloud $\mathbf{X}$: a diagonal blob floating **off-center** (the cross mark × is not at the origin)
- **(c)** — the centered cloud $\bar{\mathbf{X}}$: same blob, same shape, but now the × sits **at the origin**
- **(d)** — after PCA rotation: the blob is now **axis-aligned** — it stretches vertically instead of diagonally

Each figure is one transformation step. This whole question is the story of those steps.

---

## Concept 1 — What is a Point Cloud?

A **point cloud** $\mathbf{X} \doteq \{\mathbf{x}_i\}_{i=1}^N$ is simply a **collection of $N$ data points**, each being a vector.

In this question each point is 2D:

$$\mathbf{x}_i = \begin{bmatrix} x_{i1} \\ x_{i2} \end{bmatrix} \in \mathbb{R}^2$$

And we stack all $N$ points into a matrix:

$$\mathbf{X} \in \mathbb{R}^{N \times 2} \quad \leftarrow \quad N \text{ rows (samples)}, \quad 2 \text{ columns (features)}$$

Each **row** is one point. Each **column** is one feature (coordinate axis).

> 🧠 Think of it as a spreadsheet: each row is one student, columns are their exam scores in two subjects.

---

## Concept 2 — What is Centering? (for 3-1 and 3-2)

**Field:** Statistics / Data Preprocessing

**What is the empirical mean $\boldsymbol{\mu}$?**

$$\boldsymbol{\mu} = \frac{1}{N}\sum_{i=1}^{N} \mathbf{x}_i$$

This is the **average point** — the center of mass of the cloud. In figure (b), this is where the × sits (off the origin).

**What is centering?**

$$\bar{\mathbf{X}} : \quad \bar{\mathbf{x}}_i = \mathbf{x}_i - \boldsymbol{\mu} \quad \text{for every point}$$

You subtract the mean from every single point. This **slides the entire cloud** so its center lands exactly at the origin.

**Why do we center?**

- PCA requires the data to be centered — otherwise the first "direction of variance" just points toward the mean, which is meaningless
- Covariance formulas assume zero mean
- It removes the irrelevant "where is the cloud" information and keeps only "what shape is the cloud"

> 🧠 Imagine a group of people. Centering doesn't change how spread out they are — it just teleports the whole group so their average position is the origin.

---

## Concept 3 — numpy `axis=0` vs `axis=1` (for 3-2)

This is one of the most confused topics in numpy. Let me be very concrete.

Say we have this matrix ($N=3$ rows, $2$ columns):

$$\mathbf{X} = \begin{bmatrix} 2 & 6 \\ 4 & 8 \\ 6 & 10 \end{bmatrix}$$> 

<img width="1440" height="678" alt="image" src="https://github.com/user-attachments/assets/ff21e879-6b8f-4a56-ae25-f4861e935338" />

🔑 **Rule to memorize:** `axis=0` = collapse **rows** = compute **one value per column** = what we want for centering. `axis=1` = collapse **columns** = one value per row = wrong for centering.

The centering code is therefore: `X - X.mean(axis=0)`

---

## Concept 4 — Eigenvalues and Eigenvectors (for 3-3 and 3-4)

**Field:** Linear Algebra / PCA

Before we talk about PCA, you need to understand these two objects.

**What is the covariance matrix $\boldsymbol{\Sigma}$?**

Given centered data $\bar{\mathbf{X}}$, the empirical covariance matrix is:

$$\boldsymbol{\Sigma} = \frac{1}{N}\bar{\mathbf{X}}^\top\bar{\mathbf{X}} \in \mathbb{R}^{2 \times 2}$$

For 2D data it looks like:

$$\boldsymbol{\Sigma} = \begin{bmatrix} \sigma_{11} & \sigma_{12} \\ \sigma_{21} & \sigma_{22} \end{bmatrix}$$

| Entry | Meaning |
|-------|---------|
| $\sigma_{11}$ | variance of feature 1 (how spread is $x_1$?) |
| $\sigma_{22}$ | variance of feature 2 (how spread is $x_2$?) |
| $\sigma_{12} = \sigma_{21}$ | covariance (do $x_1$ and $x_2$ move together?) |

**What are eigenvectors and eigenvalues?**

For any square matrix $\boldsymbol{\Sigma}$, an **eigenvector** $\mathbf{u}$ is a special direction that satisfies:

$$\boldsymbol{\Sigma}\mathbf{u} = \lambda\mathbf{u}$$

In plain words: when you multiply $\boldsymbol{\Sigma}$ by $\mathbf{u}$, the result is just $\mathbf{u}$ **scaled** by a number $\lambda$ — it doesn't rotate, only stretches.

- $\mathbf{u}$ = **eigenvector** = the special direction
- $\lambda$ = **eigenvalue** = how much that direction gets stretched

<img width="1440" height="550" alt="image" src="https://github.com/user-attachments/assets/8635a7f9-d8fc-4e75-9bff-755e9fb7cb92" />

---

## Concept 5 — What PCA Does: The Matrix $\mathbf{U}$ and $\mathbf{U}^\top$ (for 3-3)

**Field:** PCA / Dimensionality Reduction

We collect all eigenvectors as **columns** of a matrix $\mathbf{U}$:

$$\mathbf{U} = \begin{bmatrix} | & | \\ \mathbf{u}_1 & \mathbf{u}_2 \\ | & | \end{bmatrix} \in \mathbb{R}^{2 \times 2}$$

The **key rule:** eigenvectors are sorted by eigenvalue — **largest first**.

$$\lambda_1 \geq \lambda_2 \geq \cdots$$

So $\mathbf{u}_1$ (first column) = direction of most variance. $\mathbf{u}_2$ (second column) = direction of least variance.

**What does $\mathbf{U}^\top\mathbf{x}$ do geometrically?**

It **rotates** the data so that:
- The direction of most variance aligns with the $x_1$ axis
- The direction of least variance aligns with the $x_2$ axis

This is exactly what happens between figure (c) and figure (d) — the diagonal blob becomes a vertical blob, because the axes have been rotated to match the data's natural directions.

<img width="1440" height="530" alt="image" src="https://github.com/user-attachments/assets/2677caea-11d3-4a6f-b969-dbb91a3e48f8" />

---

## Concept 6 — What $\boldsymbol{\Sigma}^{-1/2}\mathbf{U}^\top\mathbf{x}$ Does (Whitening) vs $\mathbf{U}^\top\mathbf{x}$ (Rotation Only)

This distinction is critical for 3-3.

| Operation | Name | What it does geometrically |
|-----------|------|---------------------------|
| $\mathbf{U}^\top\mathbf{x}$ | **PCA rotation** | Rotates the cloud to align with axes. Shape preserved. Covariance becomes diagonal but values are $\lambda_1, \lambda_2$ |
| $\boldsymbol{\Sigma}^{-1/2}\mathbf{U}^\top\mathbf{x}$ | **Whitening** | Rotates AND rescales so that variance in every direction = 1. Covariance becomes identity $\mathbf{I}$ |

$\boldsymbol{\Sigma}^{-1/2}$ is a diagonal matrix:

$$\boldsymbol{\Sigma}^{-1/2} = \begin{bmatrix} \frac{1}{\sqrt{\lambda_1}} & 0 \\ 0 & \frac{1}{\sqrt{\lambda_2}} \end{bmatrix}$$

It divides each direction by the standard deviation in that direction — making the blob circular.

> 🧠 Think: $\mathbf{U}^\top\mathbf{x}$ rotates a tilted ellipse to be upright. $\boldsymbol{\Sigma}^{-1/2}\mathbf{U}^\top\mathbf{x}$ additionally squishes/stretches it into a circle.

---

## Concept 7 — What Happens to Covariance After PCA Rotation? (for 3-4)

After applying $\mathbf{U}^\top$, the new covariance matrix becomes:

$$\boldsymbol{\Sigma}_{\text{new}} = \mathbf{U}^\top \boldsymbol{\Sigma} \mathbf{U} = \begin{bmatrix} \lambda_1 & 0 \\ 0 & \lambda_2 \end{bmatrix}$$

This is a **diagonal matrix** — all off-diagonal entries are exactly zero.

**What does zero off-diagonal mean?**

The **Pearson correlation coefficient** between two features $i$ and $j$ is:

$$\rho_{ij} = \frac{\Sigma_{ij}}{\sqrt{\Sigma_{ii}\Sigma_{jj}}}$$

If $\Sigma_{ij} = 0$ (off-diagonal = 0), then $\rho_{ij} = 0$ — the features are **uncorrelated** after rotation.

> 🔑 PCA rotation removes correlations between features. This is one of its most important properties.

---

## Symbol Dictionary — Everything Defined

| Symbol | Name | Meaning |
|--------|------|---------|
| $\mathbf{X}$ | design matrix | $N \times 2$ matrix of all data points |
| $\boldsymbol{\mu}$ | empirical mean | average point $= \frac{1}{N}\sum \mathbf{x}_i$ |
| $\bar{\mathbf{X}}$ | centered data | $\mathbf{X}$ with mean subtracted |
| $\boldsymbol{\Sigma}$ | covariance matrix | $\frac{1}{N}\bar{\mathbf{X}}^\top\bar{\mathbf{X}}$, captures spread and correlation |
| $\mathbf{U}$ | eigenvector matrix | columns = eigenvectors sorted by $\lambda$ descending |
| $\mathbf{U}^\top$ | transpose of U | performs the PCA rotation |
| $\lambda_i$ | eigenvalue | variance of data along eigenvector $\mathbf{u}_i$ |
| $\boldsymbol{\Sigma}^{-1/2}$ | inverse square root | diagonal matrix with $1/\sqrt{\lambda_i}$ entries, used in whitening |
| $\rho_{ij}$ | Pearson correlation | normalized covariance between features $i$ and $j$ |
| `axis=0` | numpy parameter | compute along rows → one value per column |
| `axis=1` | numpy parameter | compute along columns → one value per row |

---
---

