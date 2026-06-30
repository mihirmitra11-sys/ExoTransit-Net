# ExoTransit-Net 🪐

Automated exoplanet transit detection from Kepler space 
telescope light curves using 1D-CNN.

## Results

| Phase | Preprocessing | Precision | Recall | F1 | False Alarms |
|-------|---------------|-----------|--------|----|--------------|
| Baseline | Standardization + 136x weight | 0.01 | 1.00 | 0.02 | 565 |
| Improved | Augmentation + 15x weight | 0.03 | 0.80 | 0.05 | 143 |
| Uniform Detrend | Uniform filter + augmentation | 0.00 | 0.00 | 0.00 | 0 |
| **SavGol Detrend** | **Savitzky-Golay + augmentation** | **0.11** | **0.20** | **0.14** | **8** |

**Best result:** SavGol detrending — F1=0.143, false alarms 
reduced 94% (565→8) compared to baseline.

## Key Finding

Preprocessing quality dominates model performance in rare 
astronomical event detection. Savitzky-Golay detrending 
preserves short-duration transit signals while removing slow 
stellar variability, producing a 3× improvement in F1 over 
augmentation alone and a 94% reduction in false alarms.

Naive uniform filter detrending removes transit signals along 
with stellar noise — demonstrating that preprocessing method 
choice is more impactful than model architecture in this domain.

## Problem Statement

The Kepler dataset contains 5,087 stars with only 37 confirmed 
exoplanet hosts (0.7%) — severe class imbalance that makes 
standard training ineffective. A model predicting "no planet" 
for every star achieves 99.3% accuracy while finding zero planets. 
We use recall and F1 as primary metrics instead.

## Dataset

- **Source:** Kepler Labelled Time Series Data (Kaggle)
- **Stars:** 5,087 training, 570 test
- **Features:** 3,197 flux measurements per star
- **Labels:** 1 = no planet (5,050 stars), 2 = planet (37 stars)
- **Imbalance ratio:** 1:136

## Installation

```bash
pip install numpy pandas matplotlib tensorflow scikit-learn scipy
```

## Notebooks

| Notebook | Description |
|----------|-------------|
| `Exoplanet_detection.ipynb` | Complete pipeline — all phases |

## Methodology

1D-CNN with three convolutional blocks (491,073 parameters).
Four preprocessing strategies evaluated systematically:
1. Standardization only
2. Class weighting (15×) + augmentation (37→407 planet examples)
3. Uniform filter detrending (window=200)
4. Savitzky-Golay detrending (window=201, polyorder=2)

## Future Work

- Phase folding to amplify transit signal periodicity
- LSTM or attention-based architecture for periodic patterns
- Cross-validation for more robust evaluation  
- TESS mission data for larger positive class

## Paper

See `ExoTransit_Net_Paper.pdf` for the full 3-page research paper.

## References

- Shallue & Vanderburg (2018). Identifying Exoplanets with 
  Deep Learning. *The Astronomical Journal*, 155(2), 94.
- Borucki et al. (2010). Kepler Planet-Detection Mission. 
  *Science*, 327(5968), 977-980.
