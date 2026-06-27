# ExoTransit-Net
Exoplanet transit detection from Kepler light curves using 1D-CNN
# ExoTransit-Net 🪐

Exoplanet transit detection from Kepler light curves 
using 1D-CNN.

## Results

| Model | Precision | Recall | F1 | Key change |
|-------|-----------|--------|----|------------|
| Baseline 1D-CNN | 0.01 | 1.00 | 0.02 | 136x class weight |
| Improved + Augmentation | 0.03 | 0.80 | 0.05 | Aug + 15x weight |

## Key Finding
Class imbalance (37 planet stars vs 5050 non-planet) 
is the dominant challenge. Data augmentation improves 
recall to 0.80 but precision remains low at 0.03.

## Dataset
Kepler labelled time series data — 5087 stars, 
3197 flux measurements each.

## Future Work
- Gaussian process detrending
- LSTM/attention architecture
- Cross-validation evaluation

## Results

| Phase | Model | Preprocessing | Precision | Recall | F1 | False Alarms |
|-------|-------|---------------|-----------|--------|----|--------------|
| Baseline | 1D-CNN | Standardization only | 0.01 | 1.00 | 0.02 | 565 |
| Improved | 1D-CNN + Augmentation | Standardization + 15x weight | 0.03 | 0.80 | 0.05 | 143 |
| Detrended | 1D-CNN + Augmentation | Detrending + Standardization | 0.00 | 0.00 | 0.00 | 0 |

**Best result:** Phase 3 — recall=0.80, finding 4 out of 5 planet stars in test set.

## Key Finding
Class imbalance (37 planet stars vs 5050 non-planet) is the 
dominant challenge. Aggressive class weighting (136x) causes 
the model to predict everything as planet. Moderate weighting 
(15x) with augmentation achieves recall=0.80 but precision=0.03.
Naive uniform filter detrending removes transit signals along 
with stellar noise, reducing performance to zero.

## What This Means
Proper exoplanet detection requires sophisticated preprocessing 
(Gaussian Process regression, Savitzky-Golay filtering) rather 
than simple smoothing. This motivates future work on 
domain-specific preprocessing pipelines.
