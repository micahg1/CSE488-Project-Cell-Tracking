# Team Siam – Cell Segmentation & Tracking Showcase

[![GitHub Repo](https://img.shields.io/badge/GitHub-Code-181717?logo=github&logoColor=white)](https://github.com/AshfakSiam/CSE488-Project-Cell-Tracking)

> This page presents our progress and results for the CSE 488 Cell Segmentation & Tracking project.

## Project Overview

- **Dataset(s):** Fluo-N2DH-GOWT1 (tracks 01 & 02)
- **Team roles:**  
  - K M Ashfak Alam Siam – Segmentation Lead  
  - Micah Granadino – Tracking Lead  
  - Sudhir Yadav – Evaluation / Integration
- **Summary:**  
  Our project implements and evaluates both classical and deep-learning approaches for cell segmentation and tracking in microscopy videos. We focus on improving segmentation accuracy while keeping the pipeline lightweight and reproducible.

## Segmentation Results

| Method | Dataset | Track | Mean IoU | Notes |
| ------- | -------- | ------ | -------- | ----- |
| Classical SVM | Fluo-N2DH-GOWT1 | 01 | 0.73 | RBF kernel, window = 5 |
| CNN Baseline (U-Net) | Fluo-N2DH-GOWT1 | 02 | 0.81 | Lightweight U-Net architecture |

We compare traditional feature-based segmentation with CNN-based models and document preprocessing, feature extraction, and hyperparameters in the associated notebooks.

## Tracking Results (Grad/Honors)

| Tracker | Metric | Score | Notes |
| -------- | ------- | ------ | ----- |
| ASM + IoU Linking | ID Switches | 4 | Initialized from previous frame |

We link segmented cells across frames using IoU-based matching and analyze failure cases when objects overlap or split.

## Demo Videos / GIFs

Embed any media under `docs/assets/`. Example:

```html
<video controls width="640">
  <source src="assets/segmentation_demo.mp4" type="video/mp4" />
  Your browser does not support the video tag.
</video>
```

## Reproduction Checklist

1. `conda env create -f environment.yml`
2. `python scripts/setup_data.py --dataset Fluo-N2DH-GOWT1 --splits training test`
3. `python scripts/train_svm.py ...`
4. `python scripts/eval_seg.py ...`
5. Additional steps for custom models.

## Lessons Learned / Next Steps

We learned how critical preprocessing is for accurate tracking and plan to explore transformer-based segmentation and self-supervised pre-training in the next iteration.
