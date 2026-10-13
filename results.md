# Results record

Dataset: LandCover.ai v1 aerial imagery  
Patch size: 256 × 256  
Patch count: 700  
Split: 489 training, 105 validation, 106 test patches  
U-Net: compact PyTorch U-Net, class-weighted cross-entropy, early stopping  
Random Forest: scikit-learn, RGB pixel features, up to 30,000 training pixels per class

## Held-out test metrics

| Metric | U-Net | Random Forest |
|---|---:|---:|
| mIoU | 0.2774 | 0.2263 |
| Mean Dice | 0.3516 | 0.3355 |

## Class-level F1

| Class | U-Net | Random Forest |
|---|---:|---:|
| Background | 0.80 | 0.59 |
| Building | 0.00 | 0.06 |
| Woodland | 0.77 | 0.60 |
| Water | 0.08 | 0.35 |
| Road | 0.11 | 0.08 |

## Interpretation

U-Net achieved higher aggregate mIoU and mean Dice. Random Forest achieved higher recall for building, water and road pixels but with low precision, indicating many false-positive predictions. Neither model produced strong results across all classes.

## Evaluation caveat

Patches were randomly split after patch extraction. Neighbouring patches from the same original source image may therefore occur across train, validation and test sets. A source-image-level split is needed for a stronger generalisation estimate.
