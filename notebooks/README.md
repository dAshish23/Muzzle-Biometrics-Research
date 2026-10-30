# Analysis & Research Notebooks

This directory contains Jupyter notebooks documenting exploratory analysis, data audits, and feature extraction experiments.

## Notebook Inventory

### `muzzle_dataset_audit.ipynb`
- **Milestone 1:** Cattle muzzle dataset audit, near-duplicate detection, and identity-disjoint splits.
- **Key Steps Performed:**
  1. Loads dataset from Hugging Face (`casperhuggingface/gaaibastu-muzzles`) or local high-res Zenodo originals (`10.5281/zenodo.6324361`).
  2. Builds comprehensive image manifest (dimensions, brightness, contrast, Laplacian blur score).
  3. Computes 256-bit perceptual difference hash (`dHash`) to detect and audit near-duplicate capture frames.
  4. Generates identity-disjoint splits (`train: 60%`, `dev: 20%`, `test: 20%` of unique cows, stratified by camera source prefix).
  5. Enforces enrolment and query protocol (guards against temporal proximity and duplicate leakage).
  6. Exports frozen outputs: `manifest.csv`, `splits.json`, `splits.sha256`, `pairs_dev.csv`, `pairs_test.csv`, and `protocol.md` into `outputs/`.

