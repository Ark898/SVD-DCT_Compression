# Image Compression Lab: SVD vs. DCT

An interactive web-based playground for exploring transform-based image compression. This tool implements both **Singular Value Decomposition (SVD)** and **Discrete Cosine Transform (DCT)** directly in JavaScript to demonstrate how different mathematical approaches handle visual data reduction.

## 🚀 Live Demo Features

* **Real-time Processing:** Performs SVD (randomized) and DCT (8x8 blocks) on client-side images.
* **Metric Comparison:** Calculates and displays **PSNR** (Peak Signal-to-Noise Ratio) and **MSE** (Mean Squared Error) to quantify quality loss.
* **Compression Ratios:** Shows the theoretical storage savings for both methods.
* **Interactive Controls:**
    * Adjust the **Rank ($k$)** for SVD to see how low-rank approximation affects smooth surfaces.
    * Adjust the **Coefficient Keep %** for DCT to observe "blocking" artifacts similar to JPEG.
* **Built-in Samples:** Includes procedurally generated "Portrait," "Cityscape," and "Spectrum" samples to test sharp edges vs. smooth gradients.

---

## 🧪 The Algorithms

### 1. Singular Value Decomposition (SVD)
The SVD decomposes an image matrix $A$ into $U \Sigma V^T$. For compression, we keep only the top $k$ singular values.
* **Best for:** Images with global structures or soft gradients.
* **Artifacts:** High compression results in a "blurry" or "ghosting" effect as high-frequency details are lost.

### 2. Discrete Cosine Transform (DCT)
This method mimics the core of the JPEG standard. The image is divided into $8 \times 8$ blocks, transformed into frequency space, and truncated using a zig-zag scan pattern.
* **Best for:** General photography with local details.
* **Artifacts:** High compression results in "blockiness" (discontinuities at the 8x8 boundaries) and "ringing" near sharp edges.

---

## 🛠️ Implementation Details

* **Randomized SVD:** To maintain performance in the browser, a randomized algorithm (sketching + power iteration) is used to find the top $k$ singular values rather than computing the full decomposition.
* **Zig-Zag Masking:** The DCT implementation uses a classic zig-zag scan order to prioritize low-frequency coefficients, which contain the most visual information for human eyes.
* **Vanilla JS:** No external heavy math libraries are used; the linear algebra and matrix transformations are implemented from scratch in the `<script>` tag.

---

## 📦 How to Run

1.  Save the provided code as an `index.html` file.
2.  Open the file in any modern web browser (Chrome, Firefox, or Edge recommended).
3.  Upload your own image or click a **Sample** button to begin.
4.  Adjust the sliders and click **Run Compression**.

---

## 📊 Evaluation Metrics

| Metric | Description | Goal |
| :--- | :--- | :--- |
| **PSNR** | Measures the ratio between the max possible power of a signal and the power of corrupting noise. | **Higher** is better quality. |
| **MSE** | The average squared difference between the original and compressed pixels. | **Lower** is better. |
| **Ratio** | The size of the original data divided by the size of the compressed representation. | **Higher** is more efficient. |
