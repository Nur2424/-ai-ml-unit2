# Phase 2 — Full Worked Solutions

One sub-question at a time. Every calculation shown.

---

# Sub-question 5-1
## "How many bits to transmit the original image without compression?"

**Options:**
- A. $H \times W \times 8$
- B. $H \times W \times 24$
- C. $H \times W \times 3$
- D. $(H + W) \times 24$
- E. $H \times W \times 2^8$

---

### Step 1 — Count the pixels

The image is a grid of $H$ rows and $W$ columns:

$$\text{total pixels} = H \times W$$

**Concrete example:** a $100 \times 200$ image has $100 \times 200 = 20{,}000$ pixels.

---

### Step 2 — Count the bits per pixel

Each pixel has 3 color channels — R, G, B. Each channel is quantized with **8 bits**:

$$\text{bits per pixel} = 8_R + 8_G + 8_B = 24 \text{ bits}$$

---

### Step 3 — Multiply

$$\text{total bits} = \underbrace{H \times W}_{\text{pixels}} \times \underbrace{24}_{\text{bits per pixel}} = H \times W \times 24$$

**Concrete example:**

$$100 \times 200 \times 24 = 480{,}000 \text{ bits}$$

---

### Step 4 — Check every option

<img width="1440" height="736" alt="image" src="https://github.com/user-attachments/assets/63f868bf-fae2-4eec-8008-172bfdcb4d09" />


### ✅ Answer: B

> 🔑 **One line:** 3 channels × 8 bits = 24 bits per pixel. Total = $H \times W \times 24$.

---

# Sub-question 5-2
## "After K=4 clustering, what must be transmitted to reconstruct while maximizing bandwidth savings?"

**Options:**
- A. Only the $H \times W$ assignment matrix, each entry = 2-bit index
- B. The 4 centroids ($4 \times 24$ bits) + $H \times W$ assignment matrix (2 bits each)
- C. The 4 centroids ($4 \times 24$ bits) + original 24-bit values for pixels closest to each centroid
- D. None of the above
- E. Both B and C are correct

---

### Step 1 — What does the receiver need to reconstruct the image?

Think carefully. Your friend receives some data and needs to reproduce every pixel's color. They need to answer two questions for every pixel position:

> 1. **Which cluster does this pixel belong to?** → needs the assignment map
> 2. **What color is that cluster?** → needs the codebook (centroids)

Without both pieces, reconstruction is impossible.

---

### Step 2 — Calculate the bit cost of each component

**Component 1 — The codebook (4 centroids):**

Each centroid is one RGB color = 24 bits. We have 4 centroids:

$$\text{codebook cost} = 4 \times 24 = 96 \text{ bits}$$

**Component 2 — The assignment map:**

Each pixel gets assigned to one of $K=4$ clusters. We need enough bits to index 4 options:

$$\log_2(4) = 2 \text{ bits per pixel}$$

Total for assignment map:

$$\text{assignment cost} = H \times W \times 2 \text{ bits}$$

**Total for Option B:**

$$\text{total} = \underbrace{96}_{\text{codebook}} + \underbrace{H \times W \times 2}_{\text{assignment map}} \text{ bits}$$

---

### Step 3 — Compare to the original

$$\text{original} = H \times W \times 24 \text{ bits}$$

$$\text{compressed (B)} = 96 + H \times W \times 2 \text{ bits}$$

The saving per pixel: $24 - 2 = 22$ bits per pixel. That is a massive reduction.

**Concrete example** with $H=100$, $W=200$:

$$\text{original} = 100 \times 200 \times 24 = 480{,}000 \text{ bits}$$
$$\text{compressed} = 96 + 100 \times 200 \times 2 = 96 + 40{,}000 = 40{,}096 \text{ bits}$$
$$\text{saving} \approx 92\%$$

---

### Step 4 — Check every option

<img width="1440" height="890" alt="image" src="https://github.com/user-attachments/assets/ba21ac7b-0861-4f49-9f9b-0393a8747933" />


### ✅ Answer: B

---

### Visual summary — what gets sent and why

<img width="1440" height="550" alt="image" src="https://github.com/user-attachments/assets/41654162-c923-4cdb-920a-8630a766d52f" />

---

## Full Answer Key — Question 5

| Sub-Q | Answer | Core reason |
|-------|--------|-------------|
| 5-1 | B | $H \times W$ pixels × 24 bits/pixel = $H \times W \times 24$ |
| 5-2 | B | Codebook ($4 \times 24$ bits) + assignment map ($H \times W \times 2$ bits) — both required, minimum possible |

> 🔑 **The two rules to memorize:**
> 1. Uncompressed RGB = $H \times W \times 24$ bits always.
> 2. K-means compressed = codebook ($K \times 24$ bits) + assignment map ($H \times W \times \log_2 K$ bits).

---

Say **"Phase 3"** when ready for practice problems!
