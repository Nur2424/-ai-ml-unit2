# Phase 2 — Worked Solutions

Let's go one sub-question at a time. No rushing. Every step explained.

---

# Sub-question 2-1
## "What is the formula for the orthogonal projection $\mathbf{z}_{\text{prj}}$?"

**Options:**
- A. $\mathbf{X}(\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top$
- B. $\mathbf{X}^\top(\mathbf{X}\mathbf{X}^\top)^{-1}\mathbf{X}$
- C. $(\mathbf{X}^\top\mathbf{X})\mathbf{X}^{-1}\mathbf{X}^\top$
- D. $\mathbf{X}(\mathbf{X}^\top\mathbf{X})\mathbf{X}^\top$
- E. $(\mathbf{X}\mathbf{X}^\top)^{-1}\mathbf{X}\mathbf{X}^\top$

---

### Step 1 — What are we actually looking for?

We want a matrix $\mathbf{P}$ such that when we multiply it by any $\mathbf{z}$, we get the projection:

$$\mathbf{z}_{\text{prj}} = \mathbf{P} \cdot \mathbf{z}$$

This matrix $\mathbf{P}$ must satisfy two things:

> 1. $\mathbf{z}_{\text{prj}}$ must be **inside** $\text{Col}(\mathbf{X})$ — a combination of columns of $\mathbf{X}$
> 2. The error $(\mathbf{z} - \mathbf{z}_{\text{prj}})$ must be **perpendicular** to every column of $\mathbf{X}$

---

### Step 2 — Build the formula from scratch

**Condition 1** tells us $\mathbf{z}_{\text{prj}} = \mathbf{X}\boldsymbol{\alpha}$ for some unknown weights $\boldsymbol{\alpha}$.

**Condition 2** says the error is perpendicular to all columns. Using the dot product (F5):

$$\mathbf{X}^\top(\mathbf{z} - \mathbf{z}_{\text{prj}}) = \mathbf{0}$$

Substitute $\mathbf{z}_{\text{prj}} = \mathbf{X}\boldsymbol{\alpha}$:

$$\mathbf{X}^\top(\mathbf{z} - \mathbf{X}\boldsymbol{\alpha}) = \mathbf{0}$$

Expand:

$$\mathbf{X}^\top\mathbf{z} - \mathbf{X}^\top\mathbf{X}\boldsymbol{\alpha} = \mathbf{0}$$

Move $\mathbf{X}^\top\mathbf{X}\boldsymbol{\alpha}$ to the right:

$$\mathbf{X}^\top\mathbf{X}\boldsymbol{\alpha} = \mathbf{X}^\top\mathbf{z}$$

Multiply both sides by $(\mathbf{X}^\top\mathbf{X})^{-1}$ (F6 — the inverse):

$$\boldsymbol{\alpha} = (\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top\mathbf{z}$$

Now substitute back into $\mathbf{z}_{\text{prj}} = \mathbf{X}\boldsymbol{\alpha}$:

$$\boxed{\mathbf{z}_{\text{prj}} = \mathbf{X}(\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top \cdot \mathbf{z}}$$

So the projection matrix is $\mathbf{P} = \mathbf{X}(\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top$.

---

### Step 3 — Check every option with a shape/logic test

Before checking shapes, remember our matrix sizes:

$$\mathbf{X} \in \mathbb{R}^{d \times N}, \quad \mathbf{X}^\top \in \mathbb{R}^{N \times d}$$

The result $\mathbf{P}$ must be $d \times d$ so that $\mathbf{P}\mathbf{z}$ gives a $d$-dimensional vector.

<img width="1440" height="804" alt="image" src="https://github.com/user-attachments/assets/b2346e19-c875-4021-995b-3fa4f013eefe" />


### ✅ Answer: A

> 🔑 **Exam trick:** If you see a projection formula and you're unsure, check two things: (1) does the shape give $d \times d$? (2) is there an inverse $(\cdot)^{-1}$? If either is missing, eliminate it.

---
---

# Sub-question 2-2
## "What is the dimensionality of $\mathbf{z}_{\text{prj}}$ after the projection?"

**Options:**
- A. $d - N$
- B. $N$
- C. $d + N$
- D. $d$
- E. $N - 1$

---

### Step 1 — Understand exactly what the question is asking

The question asks: **how many components does the vector $\mathbf{z}_{\text{prj}}$ have?**

This sounds simple, but there is one trap that catches almost every student. Let me show you the trap first.

---

### Step 2 — The trap: two meanings of "dimension"
When you project z\mathbf{z}
z onto the subspace, two things exist simultaneously:

<img width="1440" height="592" alt="image" src="https://github.com/user-attachments/assets/8b4d2264-c39f-4560-b9de-6abaf9c58861" />


Projecting onto a subspace = projecting onto all the directions spanned by the columns of X simultaneously.
🔑 One line: "onto the subspace" = "onto the flat surface built by all the columns of X\mathbf{X}
X together." The result is the closest point on that surface to z\mathbf{z}z.

"We have N directions. We build one surface using all of them together. Then we drop z\mathbf{z}
z perpendicularly onto that surface. Where it lands is zprj\mathbf{z}_{\text{prj}}
zprj​.

Columns of X = the directions → Col(X) = the surface built from those directions → zprj\mathbf{z}_{\text{prj}}
zprj​ = where z\mathbf{z}
z lands on that surface


---

### Step 3 — Prove it with the matrix shapes

The cleanest way to see this is through the matrix multiplication from 2-1.

$$\mathbf{z}_{\text{prj}} = \underbrace{\mathbf{P}}_{d \times d} \cdot \underbrace{\mathbf{z}}_{d \times 1} = \underbrace{\mathbf{z}_{\text{prj}}}_{d \times 1}$$

<img width="1440" height="432" alt="image" src="https://github.com/user-attachments/assets/723ce32d-baf1-4280-9dfc-6a41e4f51762" />

---

### Step 4 — Check every option

<img width="1440" height="718" alt="image" src="https://github.com/user-attachments/assets/6b66294d-4098-4dd2-8678-01b0aee71fb6" />

---

### ✅ Answer: D

> 🔑 **The one thing to lock in:** Projection does not change the space the vector lives in. $\mathbf{z} \in \mathbb{R}^d$ before projection, $\mathbf{z}_{\text{prj}} \in \mathbb{R}^d$ after projection. It is constrained to a smaller surface inside that space, but it is still described by $d$ numbers.

---
---
# Sub-question 2-3
 
## "What is the reconstruction error when z = 100x₁ + 5x₅₀ − x₁₀₀?"
 
**Options:**
 
- A. It is equal to the norm of z
- B. We cannot compute the reconstruction error
- C. The reconstruction error is zero
- D. The reconstruction error is infinite
- E. The reconstruction error is 1
 
---
 
## Step 1 — Read the question carefully
 
The question tells us something very specific about **z**:
 
$$\mathbf{z} = 100\mathbf{x}_1 + 5\mathbf{x}_{50} - \mathbf{x}_{100}$$
 
Where **x₁**, **x₅₀**, **x₁₀₀** are **training samples** — meaning they are **columns of X**.
 
Before doing any math, ask yourself one question:
 
> **What kind of thing is 100x₁ + 5x₅₀ − x₁₀₀?**
 
It is a **linear combination of columns of X** — with weights α₁ = 100, α₅₀ = 5, α₁₀₀ = −1.
 
---
 
## Step 2 — Connect to what Col(X) means
 
Col(X) is exactly the set of all linear combinations of the columns of X:
 
**Col(X)={Xα ∣ α∈RN}**

So z = 100x₁ + 5x₅₀ − x₁₀₀ means:
 
**z∈Col(X)**

**z is already sitting on the surface.**
 
---
 
## Step 3 — What does projection do to a point already on the surface?
 
| Situation | What happens |
|-----------|-------------|
| z is **outside** Col(X) | Projection moves z onto the nearest point on the surface → error > 0 |
| z is **inside** Col(X) | Projection does not move z at all → z_prj = z → error = 0 |
 
In this question, z is inside Col(X) — so projection returns z unchanged.
 
---
 
## Step 4 — The logical chain
 
$$\mathbf{z} = 100\mathbf{x}_1 + 5\mathbf{x}_{50} - \mathbf{x}_{100}$$
 
$$\downarrow$$
 
$$\mathbf{z} \text{ is a linear combination of columns of } \mathbf{X}$$
 
$$\downarrow$$
 
$$\mathbf{z} \in \text{Col}(\mathbf{X}) \quad \text{(z is already on the surface)}$$
 
$$\downarrow$$
 
$$\mathbf{z}_{\text{prj}} = \mathbf{z} \quad \text{(projection does not move it)}$$
 
$$\downarrow$$
 
$$\|\mathbf{z}_{\text{prj}} - \mathbf{z}\| = \|\mathbf{z} - \mathbf{z}\| = \|\mathbf{0}\| = 0$$
 
---
 
## Step 5 — Check every option
 
| Option | Statement | Verdict | Reason |
|--------|-----------|---------|--------|
| A | Error = ‖z‖ | ✗ | This would mean z_prj = 0, which only happens when z is perpendicular to all of Col(X). Not the case here. |
| B | Cannot compute | ✗ | We absolutely can. z is explicitly given as a combination of training samples. Nothing is missing. |
| C | Error = 0 | ✓ | z ∈ Col(X) → z_prj = z → ‖z_prj − z‖ = 0 |
| D | Error = infinite | ✗ | Impossible. Projection always gives a finite result. |
| E | Error = 1 | ✗ | No basis for this. The norm is not a fixed constant here. Pure distractor. |
 
---
 
## ✅ Answer: C
 
> **The one rule to memorize:** If z is a linear combination of the columns of X, the reconstruction error is always zero. No calculation needed — just recognize that z ∈ Col(X).
 
---
 
## Key Concept — The Surface is NOT Built by One Specific Combination
 
Here is the common misunderstanding:
 
> ❌ "The surface is built by 100x₁ + 5x₅₀ − x₁₀₀"
 
That is **wrong**. The surface is built by **all possible combinations** of the columns — every possible choice of weights simultaneously.
 
---
 
## What Col(X) Actually Is
 
The columns of X are like **rulers pointing in fixed directions**. Col(X) is everything you can reach by stretching those rulers any amount you want:
 
$$\text{Col}(\mathbf{X}) = \bigl\{\, \alpha_1\mathbf{x}_1 + \alpha_2\mathbf{x}_2 + \cdots + \alpha_N\mathbf{x}_N \mid \alpha_i \in \mathbb{R} \bigr\}$$
 
Every single point you can reach by any combination of those rulers is already part of the surface.
 
---
 
## The Analogy That Makes It Click
 
Think of Col(X) like a **swimming pool**.
 
The pool already exists the moment you define the columns of X.
 
Now someone asks: *"Is the point 100x₁ + 5x₅₀ − x₁₀₀ inside the pool?"*
 
You do not need to check. The moment you see it is a combination of columns of X, it is **by definition already in the pool**. That is literally what the pool contains — all combinations.
 
---
 
## One Line to Lock It In
 
> **Col(X) is the home of every linear combination of the columns of X. Any vector written as a combination of those columns is automatically home.**
 
z = 100x₁ + 5x₅₀ − x₁₀₀ is written as a combination of columns → it is home → **error = 0**.

---
---

# Sub-question 2-4
## "When columns of X are orthogonal to each other and $\|\mathbf{x}_i\| = 1$, how does the projection formula change?"

**Options:**
- A. $\mathbf{X}(\mathbf{X}^\top\mathbf{X})^{-1}$
- B. $\mathbf{X}^\top\mathbf{X}$
- C. $(\mathbf{X}^\top\mathbf{X})\mathbf{X}^\top$
- D. $\mathbf{X}(\mathbf{X}^\top\mathbf{X})\mathbf{X}^\top$
- E. $\mathbf{X}\mathbf{X}^\top$

---

### Step 1 — What are the two conditions being given?

The question gives us two conditions simultaneously:

| Condition | Written as | Meaning |
|-----------|-----------|---------|
| Columns orthogonal | $\mathbf{x}_i^\top\mathbf{x}_j = 0$ for $i \neq j$ | any two different columns have dot product zero — they are perpendicular to each other |
| Unit norm | $\|\mathbf{x}_i\| = 1$ | every column has length exactly 1 |

Together these two conditions have a special name: **orthonormal columns**.

---

### Step 2 — What does this do to $\mathbf{X}^\top\mathbf{X}$?

Remember from Foundation 5 — the dot product between two vectors tells us how much they agree. The $(i,j)$ entry of $\mathbf{X}^\top\mathbf{X}$ is exactly the dot product between column $i$ and column $j$:

$$(\mathbf{X}^\top\mathbf{X})_{ij} = \mathbf{x}_i^\top\mathbf{x}_j$$

Now apply our two conditions to every possible entry:

<img width="1440" height="636" alt="image" src="https://github.com/user-attachments/assets/9f9cd5a4-23c6-44d3-92dd-289a64421051" />

---

### Step 3 — Substitute into the projection formula

We start from the formula we found in 2-1:

$$\mathbf{P} = \mathbf{X}(\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top$$

Now substitute $\mathbf{X}^\top\mathbf{X} = \mathbf{I}$:

$$\mathbf{P} = \mathbf{X} \underbrace{(\mathbf{I})^{-1}}_{\text{= I}} \mathbf{X}^\top$$

Since $\mathbf{I}^{-1} = \mathbf{I}$:

$$\mathbf{P} = \mathbf{X} \cdot \mathbf{I} \cdot \mathbf{X}^\top$$

And multiplying by $\mathbf{I}$ changes nothing — like multiplying a number by 1:

$$\boxed{\mathbf{P} = \mathbf{X}\mathbf{X}^\top}$$

<img width="1440" height="350" alt="image" src="https://github.com/user-attachments/assets/9ba47def-0b3f-43fe-abe8-7b24dba5b389" />

---

### Step 4 — Check every option

<img width="1440" height="718" alt="image" src="https://github.com/user-attachments/assets/f1d568b0-13a2-412f-95e8-8142950d724b" />

---

### ✅ Answer: E

> 🔑 **The one thing to lock in:** Orthonormal columns → $\mathbf{X}^\top\mathbf{X} = \mathbf{I}$ → inverse disappears → $\mathbf{P} = \mathbf{X}\mathbf{X}^\top$. This simplification is one of the most important results in all of linear algebra for ML.

---

$$\mathbf{P} = \mathbf{X}(\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top$$

This is the **master projection formula**. Everything else in this task is just a special case of it.

Think of it as the **default** — the formula you use when you know nothing special about $\mathbf{X}$.

---

The whole task is really just asking:

> **"What happens to this master formula under different conditions?"**

| Condition | What changes | Result |
|-----------|-------------|--------|
| Nothing special | use as is | $\mathbf{X}(\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top$ |
| Columns orthonormal | $\mathbf{X}^\top\mathbf{X} = \mathbf{I}$, inverse disappears | $\mathbf{X}\mathbf{X}^\top$ |
| $d = N$ and orthonormal | $\mathbf{X}\mathbf{X}^\top = \mathbf{I}$, everything disappears | $\mathbf{I}$ |

So the whole story of sub-questions 2-1 through 2-5 is:

> **Start with the master formula → apply conditions → watch it simplify.**

Ready for the last sub-question 2-5?

---
---

# Sub-question 2-5
## "When $d = N$ and columns are orthonormal, what happens when you project $\mathbf{z}$?"

**Options:**
- A. The projection is zero
- B. The projection is $\mathbf{z}$
- C. The projection is $\mathbf{z}$ is equal to $\mathbf{X}$
- D. The projection is not defined
- E. The projection is $\mathbf{z}$ but centered at the origin

---

### Step 1 — What do we already know coming in?

From 2-4 we established:

> When columns are orthonormal → $\mathbf{X}^\top\mathbf{X} = \mathbf{I}$ → projection simplifies to $\mathbf{P} = \mathbf{X}\mathbf{X}^\top$

Now 2-5 adds **one extra condition** on top of that:

$$d = N$$

This means $\mathbf{X}$ is now a **square matrix** — same number of rows and columns.

---

### Step 2 — What does $d = N$ do to $\mathbf{X}\mathbf{X}^\top$?

Let's think about the shapes carefully.

When $d > N$ (the general case from before):

$$\mathbf{X} \in \mathbb{R}^{d \times N} \implies \mathbf{X}\mathbf{X}^\top \in \mathbb{R}^{d \times d}$$

But $\mathbf{X}\mathbf{X}^\top \neq \mathbf{I}_d$ in general — because $\mathbf{X}$ is tall and thin, not square.

When $d = N$ AND columns are orthonormal:

$$\mathbf{X} \in \mathbb{R}^{d \times d} \implies \mathbf{X} \text{ is square}$$

For a square matrix with orthonormal columns, a special extra rule kicks in:

$$\mathbf{X}^\top\mathbf{X} = \mathbf{I} \implies \mathbf{X}\mathbf{X}^\top = \mathbf{I} \text{ too}$$

> 🔑 This only works when $\mathbf{X}$ is **square**. For non-square $\mathbf{X}$, $\mathbf{X}^\top\mathbf{X} = \mathbf{I}$ does NOT mean $\mathbf{X}\mathbf{X}^\top = \mathbf{I}$.

<img width="1440" height="550" alt="image" src="https://github.com/user-attachments/assets/77b716b8-f991-4536-9c5e-64ec57285f63" />

---

### Step 3 — What does $\mathbf{P} = \mathbf{I}$ mean geometrically?

When $\mathbf{P} = \mathbf{I}$, the projection matrix is the identity. So:

$$\mathbf{z}_{\text{prj}} = \mathbf{P}\mathbf{z} = \mathbf{I}\mathbf{z} = \mathbf{z}$$

The projection returns $\mathbf{z}$ completely unchanged.

**Why does this make sense geometrically?**

<img width="1440" height="532" alt="image" src="https://github.com/user-attachments/assets/d3a907ef-ca4d-46a0-8cf6-e00d372ae846" />

**The geometric reason is simple:**

When $d = N$ and columns are orthonormal, the $N$ columns span **all of** $\mathbb{R}^d$. There is no "outside" anymore. Every possible $\mathbf{z}$ is already on the surface. So projection has nothing to do — it returns $\mathbf{z}$ as it is.

---

### Step 4 — The full chain from master formula to final answer

$$\underbrace{\mathbf{P} = \mathbf{X}(\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top}_{\text{master formula (2-1)}}$$

$$\downarrow \quad \mathbf{X}^\top\mathbf{X} = \mathbf{I} \text{ (orthonormal cols)}$$

$$\mathbf{P} = \mathbf{X}\mathbf{X}^\top \quad \text{(result from 2-4)}$$

$$\downarrow \quad d = N \text{ (square matrix)}$$

$$\mathbf{X}\mathbf{X}^\top = \mathbf{I}_d$$

$$\downarrow$$

$$\mathbf{z}_{\text{prj}} = \mathbf{I}_d \cdot \mathbf{z} = \mathbf{z}$$

---

### Step 5 — Check every option

<img width="1440" height="718" alt="image" src="https://github.com/user-attachments/assets/9fb290e3-bc70-4c68-8bbe-3039bbc0142a" />

---

### ✅ Answer: B

> 🔑 **The one thing to lock in:** $d = N$ with orthonormal columns means the subspace becomes the entire space. Nothing is "outside" anymore. So every $\mathbf{z}$ projects to itself.

---

## Phase 2 Complete — All 5 Sub-questions Solved

Here is the full answer key:

| Sub-Q | Answer | Core reason |
|-------|--------|-------------|
| 2-1 | A | Master projection formula derived from perpendicularity condition |
| 2-2 | D | $\mathbf{P}$ is $d \times d$, so $\mathbf{Pz}$ is always $d$-dimensional |
| 2-3 | C | $\mathbf{z}$ is a combination of columns → already in Col($\mathbf{X}$) → error = 0 |
| 2-4 | E | Orthonormal → $\mathbf{X}^\top\mathbf{X} = \mathbf{I}$ → inverse disappears → $\mathbf{X}\mathbf{X}^\top$ |
| 2-5 | B | $d = N$ + orthonormal → $\mathbf{X}\mathbf{X}^\top = \mathbf{I}$ → $\mathbf{z}_{\text{prj}} = \mathbf{z}$ |

---
---



