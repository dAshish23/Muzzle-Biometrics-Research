# Cattle Muzzle Biometrics Research Internship

> **Fingerprint-Inspired Cattle Muzzle Biometrics for Open-Set Identification and Verification**  
> Investigating bovine nasolabial plate morphological minutiae, geometric feature graphs, and robust partial-matching verification.

---

## 📌 Repository Overview

This repository houses the research codebase, datasets, models, literature, and evaluation benchmarks for the Cattle Muzzle Biometrics Research Internship.

The core objective is to develop a robust biometric identification framework inspired by human fingerprint minutiae—extracting invariant structural landmarks (beads, groove intersections, pore configurations) from bovine muzzle prints to achieve reliable animal identification under real-world conditions (occlusion, debris, head pose, lighting variations).

---

## 🗂️ Systematic Project Layout

The repository is organized following clean research and data science conventions:

```
Internship/
├── docs/                                  # Research literature, papers, and internship briefs
│   ├── brief/
│   │   └── Cattle_Muzzle_Biometrics_Research.pdf  # Formal problem brief & requirements
│   ├── literature/
│   │   ├── DP_xsimun04.pdf                        # Reference thesis on biometric patterns
│   │   └── Veterinary Medicine - 2025 - Spoljaric - ... # Špoljarić et al. (2025) foundational paper
│   └── README.md                          # Literature catalog & summaries
│
├── notebooks/                             # Jupyter notebooks for audits and experimentation
│   ├── muzzle_dataset_audit.ipynb         # Milestone 1: Data audit, dHash check & disjoint splits
│   └── README.md                          # Notebook index and execution notes
│
├── outputs/                               # Frozen manifests, splits, and protocol artifacts
│   ├── manifest.csv                       # Master image manifest (4,923 images, 268 cows)
│   ├── splits.json                        # Locked train/dev/test cow allocations
│   ├── splits.sha256                      # SHA-256 integrity verification hash
│   ├── pairs_dev.csv                      # Dev set genuine & impostor pairs (threshold tuning)
│   ├── pairs_test.csv                     # Test set genuine & impostor pairs (7,735 pairs)
│   ├── protocol.md                        # Formal verification & distortion testing protocol
│   ├── archive/
│   │   └── muzzle_audit_outputs.zip       # Preserved backup archive of milestone 1 outputs
│   └── README.md                          # Data loading instructions & field definitions
│
├── models/                                # Trained model weights and checkpoints
│   ├── cow_muzzle_resnet18.pth            # Deep metric learning ResNet-18 baseline checkpoint
│   └── README.md                          # Architecture and checkpoint details
│
├── results/                               # Benchmark performance metrics and reports
│   ├── cow_muzzle_evaluation.csv          # Quantitative metrics on frozen test pairs
│   └── README.md                          # Detailed performance analysis & error rates
│
├── .gitignore                             # Clean VCS exclusion rules (Python, PyTorch, OS files)
└── README.md                              # Master project documentation
```

---

## 🔬 Research Work Packages

The internship roadmap is structured into three primary technical work packages:

1. **Work A | Anatomical Minutiae Feature Extraction**
   - Extract intrinsic features: bead boundaries, groove ridge flow, ridge endings, bifurcation minutiae, and sweat pore locations.
   - Address image quality variations (motion blur, lighting, specular highlights, mud/debris).

2. **Work B | Geometric Representation & Invariant Descriptors**
   - Model extracted minutiae as spatial graphs (Delaunay triangulation, relative distance/angle invariants).
   - Formulate deformation-tolerant descriptors resistant to snout curvature and capture angle changes.

3. **Work C | Visibility-Aware Verification & Robustness Benchmark**
   - Open-set pairwise matching (1:1 verification and 1:N identification).
   - Visibility masks and confidence weighting for partial matching under occlusion.
   - Comprehensive robustness stress-testing against synthetic and real-world degradations.

---

## 📊 Baseline Benchmark Results

The deep learning baseline model (`models/cow_muzzle_resnet18.pth`) was evaluated on the **7,735 frozen test pairs** (`outputs/pairs_test.csv`):

| Evaluation Metric | Score | Remarks |
| :--- | :--- | :--- |
| **ROC-AUC** | **98.94%** | Excellent ranking and discriminative capacity |
| **Accuracy** | **96.12%** | High overall verification accuracy |
| **Precision** | **89.68%** | Ratio of true positive matches among all accepted pairs |
| **Recall / TAR** | **94.01%** | True Acceptance Rate (correctly accepted genuine cows) |
| **F1-Score** | **91.79%** | Harmonic mean of precision and recall |
| **FAR (False Accept Rate)** | **3.24%** | False acceptance on impostor pairs |
| **FRR (False Reject Rate)** | **5.99%** | False rejection on genuine pairs |

---

## 🔒 Evaluation Protocol & Integrity

To ensure scientific rigor and eliminate leakage risks:
- **Identity-Disjoint Splitting:** Splits are partitioned strictly at the cow identity level (no animal appears in more than one partition).
- **Leakage Controls:** Query frames are guarded by temporal distance and filtered via perceptual 256-bit `dHash` (Hamming distance $\le 16$) to eliminate duplicate burst frames.
- **Frozen Benchmark:** The test set allocation is cryptographically locked with SHA-256 (`outputs/splits.sha256`: `9f3559722045e421ba15450971ab9619a08449b5a9676a54946a33e2b75b11ba`).

---

## 🚀 Getting Started

### 1. Environment Setup
Install core dependencies for data handling and modeling:
```bash
pip install torch torchvision pandas numpy matplotlib pillow tqdm datasets
```

### 2. Loading Frozen Splits in Code
```python
import json
import pandas as pd

# Load manifest and splits
manifest = pd.read_csv("outputs/manifest.csv")
with open("outputs/splits.json", "r") as f:
    splits = json.load(f)

# Load test evaluation pairs
test_pairs = pd.read_csv("outputs/pairs_test.csv")
print(f"Total test evaluation pairs: {len(test_pairs)}")
```

### 3. Running Analysis Notebooks
Launch Jupyter or VS Code and open [`notebooks/muzzle_dataset_audit.ipynb`](file:///e:/Internship/notebooks/muzzle_dataset_audit.ipynb).

