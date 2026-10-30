# Models & Checkpoints

This directory houses trained neural network weights and feature extractors.

## Checkpoints

### `cow_muzzle_resnet18.pth`
- **Architecture:** PyTorch ResNet-18 backbone (`torchvision.models.resnet18`)
- **File Size:** ~45 MB (45,051,339 bytes)
- **Role:** Deep metric learning baseline for cattle muzzle verification
- **Target Task:** Open-set verification and pairwise comparison on bovine muzzle images
- **Evaluation Performance (Frozen Test Set, 7,735 pairs):**
  - **ROC-AUC:** 98.94%
  - **Accuracy:** 96.12%
  - **Precision:** 89.68%
  - **Recall / TAR:** 94.01%
  - **F1-Score:** 91.79%
  - **False Acceptance Rate (FAR):** 3.24%
  - **False Rejection Rate (FRR):** 5.99%

See [`results/cow_muzzle_evaluation.csv`](file:///e:/Internship/results/cow_muzzle_evaluation.csv) and [`results/README.md`](file:///e:/Internship/results/README.md) for full benchmark figures.

