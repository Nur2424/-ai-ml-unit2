# Phase 1 — Theory Background

---

## 1-1 | Dimensionality of Samples

**Field:** Linear Algebra / Data Representation

**What is a Design Matrix?**

The **design matrix** $\mathbf{X}$ is a standard way to organize a dataset. The convention is:

$$\mathbf{X} \in \mathbb{R}^{n \times d}$$

| Symbol | Meaning |
|--------|---------|
| $n$ | number of **samples** (rows) |
| $d$ | number of **features / dimensions** (columns) |

So each **row** $\mathbf{x}^{(i)} \in \mathbb{R}^d$ is one data point living in $d$-dimensional space.

**Key formula to memorize:**
$$\text{dimensionality of samples} = \text{number of columns of } \mathbf{X} = d$$

> ⚠️ Common trap: students confuse the number of *samples* $n$ with the *dimensionality* $d$. They are completely different things.

---

## 1-2 | Empirical Average (Mean Vector)

**Field:** Statistics / Descriptive Statistics

**What is the Empirical Mean $\boldsymbol{\mu}$?**

The **empirical average** $\boldsymbol{\mu}$ (Greek letter *mu*) is the **column-wise average** across all $n$ samples. It is itself a vector of length $d$.

$$\boldsymbol{\mu} = \frac{1}{n} \sum_{i=1}^{n} \mathbf{x}^{(i)}$$

In plain words: **average each feature independently** across all rows. The result is one number per column.

**Component-wise**, for feature $j$:
$$\mu_j = \frac{1}{n} \sum_{i=1}^{n} x_j^{(i)}$$

> ⚠️ Common trap: averaging row-wise instead of column-wise. The mean vector always has the same length as the number of **features**, not the number of samples.

---

## 1-3 | Empirical Covariance Matrix & Trace

**Field:** Statistics / Multivariate Analysis

**What is the Empirical Covariance Matrix $\boldsymbol{\Sigma}$?**

The **empirical covariance matrix** $\boldsymbol{\Sigma}$ (capital Greek *sigma*) captures how features vary *together*. It is a $d \times d$ symmetric matrix.

$$\boldsymbol{\Sigma} = \frac{1}{n} \sum_{i=1}^{n} (\mathbf{x}^{(i)} - \boldsymbol{\mu})(\mathbf{x}^{(i)} - \boldsymbol{\mu})^\top$$

Or equivalently in matrix form:
$$\boldsymbol{\Sigma} = \frac{1}{n} \tilde{\mathbf{X}}^\top \tilde{\mathbf{X}}, \quad \text{where } \tilde{\mathbf{X}} = \mathbf{X} - \mathbf{1}\boldsymbol{\mu}^\top \text{ (mean-centered matrix)}$$

| Entry | Meaning |
|-------|---------|
| $\Sigma_{jj}$ (diagonal) | **Variance** of feature $j$ |
| $\Sigma_{jk}$ (off-diagonal) | **Covariance** between features $j$ and $k$ |

**What is the Trace?**

The **trace** of a square matrix $\mathbf{A}$, written $\text{tr}(\mathbf{A})$, is the **sum of its diagonal elements**:

$$\text{tr}(\boldsymbol{\Sigma}) = \sum_{j=1}^{d} \Sigma_{jj}$$

So the question asks you to compute:
$$\left(\sum_{\text{all } j,k} \Sigma_{jk}\right) - \text{tr}(\boldsymbol{\Sigma}) = \text{sum of ALL elements} - \text{sum of DIAGONAL elements} = \text{sum of OFF-DIAGONAL elements only}$$

> ⚠️ Common trap: forgetting that "sum of all elements minus trace" = sum of all **off-diagonal** entries. This is a conceptual shortcut worth memorizing.

---
