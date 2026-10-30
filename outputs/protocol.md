# Evaluation protocol (draft generated 2026-10-29)

**Dataset:** casperhuggingface/gaaibastu-muzzles, derived from Xiong, Li and Erickson (2022), Zenodo 10.5281/zenodo.6324361, CC BY 4.0.
4923 images of 268 animals. Capture sessions are not recorded, so every experiment is **single-session**.
Camera/source is only known through the filename prefix: DSCF (4875), DJI (48).

**Split (seed 42, whole animals, stratified by majority source prefix):**
- train: 160 cows, 2922 images
- dev: 54 cows, 1012 images
- test: 54 cows, 989 images

**Enrolment / query:** up to 3 enrolment images per held-out cow (non-duplicate, first in file order); queries are more than
2 frames from every enrolment frame and not near-duplicates (dHash <= 16/256 bits). Only the majority-source images are used;
the rest are held back for a separate cross-source test.

**Pairs:** genuine = enrolment x query of the same cow; impostor = query vs enrolment of a different cow with the same majority source.
Dev: 1878 genuine / 6260 impostor. Test: 1785 genuine / 5950 impostor.
Cross-source impostors are reported separately.

**Rules:** thresholds (accept / reject / recapture) are chosen on dev only. The test split is frozen (sha256 9f3559722045e421...) and used once.
Artificial distortions are applied to query images only after this split is frozen. Confidence intervals come from a bootstrap over cows.
Metrics: ROC/AUROC, EER, TAR at a stated FAR (only where the impostor count supports it), extraction failure rate, time per image and per match.
