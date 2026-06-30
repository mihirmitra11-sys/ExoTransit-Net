# ExoTransit-Net — Model Performance Metrics

## Phase 2 — Baseline
- Precision: 0.01, Recall: 1.00, F1: 0.02
- False alarms: 565
- Class weight: 136x (too aggressive)

## Phase 3 — Augmentation
- Precision: 0.03, Recall: 0.80, F1: 0.05
- False alarms: 143
- Class weight: 15x + augmentation (37→407 planet examples)

## Phase 4 — Uniform Detrending
- Precision: 0.00, Recall: 0.00, F1: 0.00
- False alarms: 0
- Uniform filter removed transit signals along with noise

## Phase 4b — SavGol Detrending (Best)
- Precision: 0.11, Recall: 0.20, F1: 0.143
- False alarms: 8
- SavGol preserves transit signals, removes stellar trends
- 3x F1 improvement over Phase 3
- 94% reduction in false alarms vs baseline
