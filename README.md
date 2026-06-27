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
