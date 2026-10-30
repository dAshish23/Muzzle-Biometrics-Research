# Experimental Results & Benchmarks

This directory tracks evaluation metrics, baseline verification benchmarks, and comparative performance logs.

## ResNet-18 Baseline Evaluation

- **Source File:** [`cow_muzzle_evaluation.csv`](file:///e:/Internship/results/cow_muzzle_evaluation.csv)
- **Model:** `cow_muzzle_resnet18.pth` (ResNet-18)
- **Protocol:** Evaluated on the frozen test pairs partition (`outputs/pairs_test.csv`) defined in `outputs/protocol.md`.
- **Test Pairs:** 7,735 pairs (1,785 genuine pairs, 5,950 impostor pairs) across 54 held-out identity-disjoint cows.

### Metrics Summary

| Metric | Value | Percentage / Notes |
| :--- | :--- | :--- |
| **ROC-AUC** | `0.9894` | **98.94%** Area Under the ROC Curve |
| **Accuracy** | `0.9612` | **96.12%** Overall pair classification accuracy |
| **Precision** | `0.8968` | **89.68%** Positive predictive value |
| **Recall / TAR** | `0.9401` | **94.01%** True Acceptance Rate |
| **F1-Score** | `0.9179` | **91.79%** Harmonic mean of precision & recall |
| **FAR (False Acceptance Rate)** | `0.0324` | **3.24%** False match rate on impostors |
| **FRR (False Rejection Rate)** | `0.0599` | **5.99%** False non-match rate on genuine |

### Protocol Integrity
The test cows and test pairs are identity-disjoint from the training set and cryptographically locked with SHA-256 (`outputs/splits.sha256`) to guarantee zero data leakage between development and testing.

