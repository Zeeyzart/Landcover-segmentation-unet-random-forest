# Results record

## Experiment setup
- Dataset: LandCover.ai v1 aerial imagery
- Patch size: 256 × 256 pixels; 700 patches total
- Split: 489 training, 105 validation, 106 test patches
- U-Net: compact PyTorch U-Net, class-weighted cross-entropy, early stopping
- Random Forest: scikit-learn RGB pixel classifier, up to 30,000 sampled training pixels per class
- Test support: 6,946,816 pixels across five classes

## Aggregate held-out test metrics

| Metric | U-Net | Random Forest |
|---|---:|---:|
| mIoU | 0.2774 | 0.2263 |
| Mean Dice | 0.3516 | 0.3355 |
| Accuracy | 0.74 | 0.52 |
| Macro precision | 0.36 | 0.34 |
| Macro recall | 0.36 | 0.51 |
| Macro F1 | 0.35 | 0.34 |
| Weighted precision | 0.72 | 0.67 |
| Weighted recall | 0.74 | 0.52 |
| Weighted F1 | 0.73 | 0.57 |

## Class-level classification report

| Class | U-Net precision | U-Net recall | U-Net F1 | U-Net support | RF precision | RF recall | RF F1 | RF support |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Background | 0.77 | 0.82 | 0.80 | 3,699,218 | 0.75 | 0.49 | 0.59 | 3,699,218 |
| Building | 0.01 | 0.00 | 0.00 | 25,259 | 0.03 | 0.57 | 0.06 | 25,259 |
| Woodland | 0.77 | 0.77 | 0.77 | 2,733,621 | 0.64 | 0.56 | 0.60 | 2,733,621 |
| Water | 0.15 | 0.05 | 0.08 | 397,767 | 0.26 | 0.54 | 0.35 | 397,767 |
| Road | 0.09 | 0.16 | 0.11 | 90,951 | 0.04 | 0.39 | 0.08 | 90,951 |
| **Macro average** | **0.36** | **0.36** | **0.35** | **6,946,816** | **0.34** | **0.51** | **0.34** | **6,946,816** |
| **Weighted average** | **0.72** | **0.74** | **0.73** | **6,946,816** | **0.67** | **0.52** | **0.57** | **6,946,816** |

## Interpretation
U-Net had a higher aggregate mIoU and mean Dice. The balanced Random Forest improved from the earlier unbalanced run (mIoU 0.0787, mean Dice 0.1130) to mIoU 0.2263 and mean Dice 0.3355. Random Forest had higher recall for building, water and road pixels, but low precision indicates many false positives. Building detection remained weak for both models.

## Evaluation issues
Patches were randomly split after patch extraction. Neighbouring patches from the same original source image may occur across train, validation and test sets. A source-image-level split is needed for a stronger generalisation estimate. Results are exploratory, not a rigorous benchmark.
