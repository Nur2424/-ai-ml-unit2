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
## "What is the reconstruction error $\|\mathbf{z}_{\text{prj}} - \mathbf{z}\|$ when $\mathbf{z} = 100\mathbf{x}_1 + 5\mathbf{x}_{50} - \mathbf{x}_{100}$?"

**Options:**
- A. It is equal to the norm of $\mathbf{z}$
- B. We cannot compute the reconstruction error
- C. The reconstruction error is zero
- D. The reconstruction error is infinite
- E. The reconstruction error is 1

---

### Step 1 — Read the question carefully

The question tells us something very specific about $\mathbf{z}$:

$$\mathbf{z} = 100\mathbf{x}_1 + 5\mathbf{x}_{50} - \mathbf{x}_{100}$$

Where $\mathbf{x}_1$, $\mathbf{x}_{50}$, $\mathbf{x}_{100}$ are **training samples** — meaning they are **columns of $\mathbf{X}$**.

Before doing any math, ask yourself one question:

> **What kind of thing is $100\mathbf{x}_1 + 5\mathbf{x}_{50} - \mathbf{x}_{100}$?**

It is a **linear combination of columns of $\mathbf{X}$** — with weights $\alpha_1 = 100$, $\alpha_{50} = 5$, $\alpha_{100} = -1$.

---

### Step 2 — Connect to what Col(X) means

From our discussion just now — Col(X) is exactly the set of all linear combinations of the columns of $\mathbf{X}$.

$$\text{Col}(\mathbf{X}) = \{\mathbf{X}\boldsymbol{\alpha} \ | \ \boldsymbol{\alpha} \in \mathbb{R}^N\}$$

So $\mathbf{z} = 100\mathbf{x}_1 + 5\mathbf{x}_{50} - \mathbf{x}_{100}$ means:

$$\mathbf{z} \in \text{Col}(\mathbf{X})$$

**$\mathbf{z}$ is already sitting on the surface.**

---

### Step 3 — What does projection do to a point already on the surface?

<img width="1440" height="550" alt="image" src="https://github.com/user-attachments/assets/fbd8070a-8eaa-47fe-b929-248ce203b1f0" />


### Step 4 — The logical chain, written cleanly

$$\mathbf{z} = 100\mathbf{x}_1 + 5\mathbf{x}_{50} - \mathbf{x}_{100}$$

$$\downarrow$$

$$\mathbf{z} \text{ is a linear combination of columns of } \mathbf{X}$$

$$\downarrow$$

$$\mathbf{z} \in \text{Col}(\mathbf{X}) \quad \text{(z is already on the surface)}$$

$$\downarrow$$

$$\mathbf{z}_{\text{prj}} = \mathbf{z} \quad \text{(projection doesn't move it)}$$

$$\downarrow$$

$$\|\mathbf{z}_{\text{prj}} - \mathbf{z}\| = \|\mathbf{z} - \mathbf{z}\| = \|\mathbf{0}\| = 0$$

---

### Step 5 — Check every option

<img width="1440" height="718" alt="image" src="https://github.com/user-attachments/assets/ebfc5f18-4320-455e-a5d9-7cc97836bb79" />

---

### ✅ Answer: C

> 🔑 **The one rule to memorize:** If $\mathbf{z}$ is a linear combination of the columns of $\mathbf{X}$, the reconstruction error is always zero. No calculation needed — just recognize that $\mathbf{z} \in \text{Col}(\mathbf{X})$.

---
---

















