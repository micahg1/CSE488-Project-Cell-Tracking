# CSE488 Project – Cell Segmentation & Tracking Starter

This repository replaces the shared Colab notebook with a reproducible Python project for the Cell Tracking Challenge inspired assignment. Use it as a GitHub **template repository** so every team starts from the same baseline while keeping their fork private and shared only with the instructional staff. Major goals:

- Provide scripts for downloading challenge data, evaluation tooling, and helper assets.
- Offer reusable modules for feature extraction, classical ML (SVM baseline), and evaluation (IoU + SEGMeasure wrapper).
- Encourage clean experiments tracked via version control instead of ad-hoc Colab sessions.

## Using This Template

1. On GitHub, click **Use this template → Create a new repository**. Keep the repo private and name it `<team>-cell-tracking` (or similar).
2. Add the instructor and TAs (John Femiani, Heather Merhout, Siddhant Karki) as collaborators so they can clone and grade your work.
3. Clone your newly created repo locally, then follow the quickstart below to set up the environment.
4. Customize the showcase page under `docs/index.md` (team name, metrics, media). Keep large artifacts under `docs/assets/`.
5. Update the README in your fork with experiment notes, checkpoints, and the Cloudflare Pages URL you will publish.

## Project Layout

```
CSE488-Project-Cell-Tracking/
├── README.md
├── pyproject.toml
├── environment.yml
├── scripts/
│   ├── setup_data.py
│   ├── train_svm.py
│   └── eval_seg.py
├── src/cell_tracking/
│   ├── __init__.py
│   ├── config.py
│   ├── data.py
│   ├── evaluation.py
│   ├── features.py
│   └── models/svm.py
├── notebooks/
│   └── 00_reference_colab.ipynb
└── tests/
    └── test_features.py
```

## Quickstart

```bash
# 1. Create environment
conda env create -f environment.yml
conda activate cse488-cell-tracking

# 2. Install repo in editable mode
pip install -e .

# 3. Download tools + datasets
python scripts/setup_data.py --dataset Fluo-N2DH-GOWT1 --splits training test

# 4. Train a toy SVM baseline
python scripts/train_svm.py --dataset Fluo-N2DH-GOWT1 --track 01 \
    --window 5 --samples 500 --model-path artifacts/models/svm_rbf.pkl

# 5. Evaluate with IoU + SEGMeasure
python scripts/eval_seg.py --gt artifacts/datasets/Fluo-N2DH-GOWT1/training/01_ST/SEG \
    --pred artifacts/results/Fluo-N2DH-GOWT1/01 --model-path artifacts/models/svm_rbf.pkl
```

Key environment variables:

- `CELL_TRACKING_BASE`: Root folder for datasets/results (defaults to `<repo>/artifacts`).
- `CELL_TRACKING_DATASETS`: Optional override for dataset cache.

## Notebooks

`notebooks/00_reference_colab.ipynb` mirrors the original Colab walkthrough but imports utilities from `src/cell_tracking`. Feel free to add exploratory notebooks; keep production code in `src/` and automation in `scripts/`.

## Next Steps for Students

1. Fork the repo (keep private) and invite John Femiani, Heather Merhout, and Siddhant Karki.
2. Use issues/projects to plan segmentation/tracking experiments.
3. Extend `scripts/` and `src/cell_tracking/` with custom methods (CNNs, trackers, etc.). For deep baselines, start with lightweight U-Nets from `segmentation_models_pytorch` (e.g., MobileNet or EfficientNet encoders) to keep training feasible.
4. Publish qualitative results and videos via GitHub Pages (or similar) linked from your README.

## Cloudflare Pages Showcase

Each team must host a lightweight public page that summarizes results and embeds demo videos. This repo includes the template at `docs/index.md`; Cloudflare Pages can publish the folder with zero build steps.

1. Edit `docs/index.md` (and any `/docs/assets/*` media) so it reflects your project. Preview locally with `python -m http.server 8000` and visit `http://localhost:8000/docs/`.
2. Commit and push to `main` in your fork.
3. Visit https://dash.cloudflare.com (create a free account if you do not already have one), then open **Workers & Pages → Create application → Pages → Connect to Git**. When prompted, authorize the Cloudflare Pages GitHub app for your fork.
4. Select your repo/branch, set **Framework preset** to `None`, leave the build command empty, and set the **Build output directory** to `docs`. Save to trigger the first deploy; Cloudflare provides `https://<project>.pages.dev`.
5. In your GitHub repo, go to **Settings → Pages** and set “Build and deployment” to **Disabled** so Cloudflare is the only publisher.
6. Update the README badge/link to point at the Cloudflare URL and include that URL in your Canvas submission. For a custom hostname, add it under **Pages → Custom domains** and create the suggested CNAME in Cloudflare DNS.
7. **Fallback option:** If Cloudflare Pages is unavailable, share the rendered `docs/index.md` directly by linking to the file in your private repo (grant graders read access) and ensure the README clearly states that temporary arrangement.

**For our Project, we rendered `docs/index.md` with read access. We will not be showcasing the Cloudflare Page.**

## License

MIT License – adjust to match your team preference if needed.
