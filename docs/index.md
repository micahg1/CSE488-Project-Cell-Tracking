# Team Siam – Cell Segmentation & Tracking Showcase

> CSE 488 / 588 – Cell Segmentation & Tracking  
> Dataset: **Fluo-N2DH-GOWT1 (Tracks 01 & 02)**

---

## Project Overview

We implement and compare **classical machine learning** and **deep learning** approaches for cell segmentation, followed by tracking using IoU-based matching.

### Team Roles

| Member | Role |
|---|---|
| **K M Ashfak Alam Siam** | Segmentation Lead |
| **Micah Granadino** | Tracking Lead |
| **Sudhir Yadav** | Evaluation & Integration |

### Goals

- Improve segmentation accuracy  
- Keep the pipeline **lightweight and reproducible**
- Perform a **rigorous comparison** of classical vs. learned methods

---

## Segmentation Results

We evaluate models using **Mean Jaccard Index (IoU)**.

| Method | Track | Mean IoU | Notes |
|---|:---:|:---:|---|
| **Patch MLP (Classical)** | 01 | **0.008** | Local 5×5 patches, no global context |
| **Patch MLP (Classical)** | 02 | **0.003** | Fails to generalize |
| **FCN-ResNet101 (Deep Learning)** | 01 | **≈ 0.48** | Strong segmentation performance |
| **FCN-ResNet101 (Deep Learning)** | 02 | **≈ 0.02** | Track 02 remains difficult |

### Key Observations

- Classical models based on local window features **perform near-random**.
- Deep CNN learns **shape, edges, texture**, producing realistic nuclei masks.
- Track 02 is challenging for **all methods** due to appearance shift and contrast.

---


