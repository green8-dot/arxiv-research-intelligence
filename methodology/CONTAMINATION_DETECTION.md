# Contamination Detection

Label contamination = mislabeled training samples degrading model performance.

**Insight:** Train on noisy data → model learns signal despite noise → use model to identify noise.

## Process

### 1. Train Baseline

Input: Raw dataset (20-60% label noise)
Output: Baseline classifier (50-75% F1)
Method: Fine-tune SciBERT on noisy data

### 2. Extract Disagreements

```
For each sample:
    if confidence > 0.8 AND prediction != assigned_label:
        mark as contamination_candidate
```

### 3. Remove Contamination

```
cleaned_dataset = raw_dataset - contamination_candidates
```

Removal: 20-60% of original data

### 4. Retrain

Input: Cleaned dataset (40-80% of original)
Output: High-performance classifier (85-95% F1)
Improvement: +8-15 points F1

## Threshold Selection

0.8 confidence optimal (96% precision on manual inspection)

## Results

| Domain | Contamination | Baseline F1 | Cleaned F1 | Improvement |
|--------|--------------|-------------|------------|-------------|
| Math | 45% | 65% | 93.97% | +28.97 |
| Physics | 55% | 58% | 88.88% | +30.88 |
| Stats | 30% | 78% | 92.26% | +14.26 |
| Qbio | 60% | 52% | 88.04% | +36.04 |
| Econ | 40% | 68% | 92.43% | +24.43 |

## Validation

cs.DC example: 182 mislabels detected (3.5% error rate), 96% precision (175/182 correct)
