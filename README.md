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

## Results

| Phase | Model | Preprocessing | Precision | Recall | F1 | False Alarms |
|-------|-------|---------------|-----------|--------|----|--------------|
| Baseline | 1D-CNN | Standardization only | 0.01 | 1.00 | 0.02 | 565 |
| Improved | 1D-CNN + Augmentation | Standardization + 15x weight | 0.03 | 0.80 | 0.05 | 143 |
| Uniform Detrend | 1D-CNN + Augmentation | Uniform filter detrending | 0.00 | 0.00 | 0.00 | 0 |
| SavGol Detrend | 1D-CNN + Augmentation | Savitzky-Golay detrending | 0.11 | 0.20 | 0.14 | 8 |

**Best result:** Phase 4b — F1=0.143, false alarms reduced 
from 565 to just 8.

## Key Findings
- Class imbalance (37 planet stars vs 5050 non-planet) 
  is the dominant challenge in exoplanet detection
- Aggressive class weighting (136x) causes the model to 
  predict everything as planet — reduces to 15x
- Naive uniform filter detrending removes transit signals 
  along with stellar noise — F1 drops to 0
- Savitzky-Golay detrending preserves transit signals 
  while removing stellar trends — F1 improves 3x to 0.143
- Preprocessing quality dominates model performance in 
  rare event detection tasks

## What This Means
With only 37 positive examples, even after augmentation 
to 481, exoplanet detection remains extremely challenging. 
Proper domain-specific preprocessing (SavGol vs uniform 
filter) produces a 3x improvement in F1 score and 94% 
reduction in false alarms, highlighting the critical 
importance of signal processing before ML model training.

## Future Work
- Longer window SavGol filtering for better trend removal
- LSTM or attention-based architecture for periodic 
  pattern detection
- Cross-validation for more robust evaluation
- Fold-and-bin phase folding to amplify transit signal
