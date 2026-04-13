# Phase 1 — Theory Background

Complete zero-knowledge build. Every concept from scratch.

---

## First — What is a Digital Image?

An image is just a **grid of pixels**. Each pixel is one tiny colored dot.

$$\text{image size} = H \text{ rows} \times W \text{ columns} = H \times W \text{ pixels total}$$

| Symbol | Meaning |
|--------|---------|
| $H$ | height — number of rows of pixels |
| $W$ | width — number of columns of pixels |
| pixel | one single colored dot in the image |

> 🧠 A 600×400 image has $600 \times 400 = 240{,}000$ pixels.

---

## Concept 1 — RGB Color and Bits (for 5-1)

**Field:** Digital Representation / Information Theory

**What is RGB?**

Every pixel's color is described by **three numbers** — one for each color channel:

$$\text{pixel} = \begin{bmatrix} R \\ G \\ B \end{bmatrix} = \begin{bmatrix} \text{Red} \\ \text{Green} \\ \text{Blue} \end{bmatrix}$$

Mix these three together and you get any color. For example:
- $[255, 0, 0]$ = pure red
- $[0, 0, 255]$ = pure blue
- $[255, 255, 0]$ = yellow
- $[0, 0, 0]$ = black
- $[255, 255, 255]$ = white

**What is a bit?**

A **bit** is the smallest unit of digital information — either $0$ or $1$.

With $n$ bits you can represent $2^n$ different values:

| Bits | Values possible |
|------|----------------|
| 1 bit | $2^1 = 2$ values |
| 2 bits | $2^2 = 4$ values |
| 8 bits | $2^8 = 256$ values |

**Why 8 bits per channel?**

Each R, G, B value is **quantized with 8 bits** — meaning each channel can take any of $2^8 = 256$ values (0 through 255).

$$\text{bits per pixel} = \underbrace{8}_R + \underbrace{8}_G + \underbrace{8}_B = 24 \text{ bits}$$

This is called **24-bit color** or **true color**.

**Total bits for the whole image:**

$$\text{total bits} = \underbrace{H \times W}_{\text{number of pixels}} \times \underbrace{24}_{\text{bits per pixel}}$$

<img width="1440" height="508" alt="image" src="https://github.com/user-attachments/assets/f83c03e3-0203-4b06-927b-e46949770e11" />

---

## Concept 2 — Image Compression Using K-means (for 5-2)

**Field:** Unsupervised Learning / Data Compression

**The core idea:**

Instead of storing 24 bits per pixel, we ask: can we represent the whole image using just a small number of representative colors?

K-means answers this by:
1. Treating every pixel as a **point in 3D RGB space**
2. Clustering all pixels into $K$ groups
3. Replacing every pixel with its cluster center color

<img width="1440" height="550" alt="image" src="https://github.com/user-attachments/assets/2bbd63c2-448d-45e1-9339-7d637fa16d27" />

---

## Concept 3 — Why $\log_2(K)$ Bits Per Pixel?

This is the key formula for 5-2. Let me explain it carefully.

With $K$ clusters, each pixel belongs to one of $K$ possible clusters. We need enough bits to represent $K$ different options.

With $n$ bits you can represent $2^n$ values. So to represent $K$ options:

$$2^n = K \implies n = \log_2(K)$$

**Concrete examples:**

| $K$ clusters | Bits needed per pixel | Why |
|-------------|----------------------|-----|
| $K=2$ | $\log_2(2) = 1$ bit | 0 or 1 |
| $K=4$ | $\log_2(4) = 2$ bits | 00, 01, 10, 11 |
| $K=8$ | $\log_2(8) = 3$ bits | 000 to 111 |
| $K=16$ | $\log_2(16) = 4$ bits | 0000 to 1111 |

In this question $K=4$, so each pixel needs only **2 bits** instead of 24. That is the compression.

---

## Concept 4 — What Must Be Transmitted and Why

To reconstruct the compressed image, your friend needs **two things**:

**Thing 1 — The codebook** (cluster centers):

The 4 RGB centroids. Without these, your friend has no idea what color each index refers to.

$$\text{cost} = K \times 24 = 4 \times 24 = 96 \text{ bits}$$

**Thing 2 — The assignment map**:

For every pixel position, which cluster does it belong to? This is an $H \times W$ matrix where each entry is a 2-bit index.

$$\text{cost} = H \times W \times \log_2(K) = H \times W \times 2 \text{ bits}$$

**Why can't you send just the assignment map (Option A)?**

Without the codebook, your friend knows that pixel $(i,j)$ belongs to cluster 2 — but has no idea what color cluster 2 is. The codebook is the **key** that maps index → color.

> 🔑 **Analogy:** The assignment map is like a treasure map saying "go to location 3." The codebook is the legend telling you "location 3 = green forest." Without the legend, the map is useless.

---

## Concept 5 — Maximizing Bandwidth Savings

**Bandwidth** = amount of data transmitted. Maximizing savings = minimizing bits sent.

Total bits for Option B:

$$\underbrace{4 \times 24}_{\text{codebook}} + \underbrace{H \times W \times 2}_{\text{assignment map}}$$

Compare to original:

$$H \times W \times 24 \text{ bits}$$

The saving comes from replacing $24$ bits per pixel with just $2$ bits per pixel. The codebook cost ($96$ bits) is tiny — just a one-time fixed overhead.

---

## Symbol Dictionary

| Symbol | Meaning |
|--------|---------|
| $H$ | image height in pixels |
| $W$ | image width in pixels |
| $K$ | number of clusters |
| RGB | Red, Green, Blue color channels |
| 8 bits | bits per channel ($2^8 = 256$ values) |
| 24 bits | bits per pixel ($3 \times 8$) |
| centroid | cluster center = representative color |
| codebook | the set of all $K$ centroids |
| assignment map | $H \times W$ matrix — which cluster each pixel belongs to |
| $\log_2(K)$ | bits needed to index $K$ clusters |

---

✅ **Phase 1 complete.** Every concept built from zero. Reply **"Phase 2"** when ready for the full worked solutions with all bit calculations!
